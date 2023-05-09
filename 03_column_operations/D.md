# Useful functions across columns

There are a multitude of useful functions in `R` and it would unfortunately
take months to go over all of them. I encourage you to work through this
section on your own time to get a handle of some of these useful functions,
read their docs, and/or play around with them.


## Finding previous or next values with `shift`

Say you have a `VCF` file with a list of SNP positions, and you're
interested in finding how close any given SNP is to its nearest neighbor.
First, re-initialize the `vcf` table and subset to only include SNPs.

```R
# read in example vcf
vcf <- fread('short.vcf')

# define single nucleotide characters
nucleotides <- c('A','C','T','G')

# Subset to only contain SNPs
vcf <- vcf[REF %in% nucleotides][ALT %in% nucleotides]      
```

Now we can create a new column that shifts the `POS` column up or down
one, indicating the nearest SNP to the left or to the right. We specify
which direction to shift the vector with `typee`:
```R
vcf[, 'nearest_left' := shift(POS, n=1, type='lag')]
vcf[, 'nearest_right' := shift(POS, n=1, type='lead')]
```

Notice how `NA` values are added at the ends where there is no value
to look back or forward to.


We used `shift` above to find each SNP's nearest neighbor to the left
and the right. A reasonable next question might be, 
*"what is the ID of the nearest SNP"* (as in `rs######` within the `ID`
column). How might you generate a new column that contains the rsID of
the nearest SNP for every row?

<details><summary>Solution</summary>

First, we need to calculate (for every row) the distance from the SNP
in question to its left and
right neighbors. 

 solution is to take the minimum value of `distance_left` and `distance_right`
```R
vcf[, 'distance_left' := POS - nearest_left]
vcf[, 'distance_right' := nearest_right - POS]
vcf[, 'ID_left' := shift(ID, type='lag')]
vcf[, 'ID_right' := shift(ID, type='lead')]
vcf[, 'nearest_snp' := ifelse(distance_left < distance_right,
                              ID_left, ID_right)]
```
</details>

---

*Bonus*: the above `ifelse` command resulted in a problem with the
`nearest_snp` column. What is it?
How might you fix it?

<details><summary>Solution</summary>

The first and last rows of `nearest_snp` are `NA`! This results because
an inequality test using `>` or `<` with `NA` on either side produces
an `NA` result. It is, after all, nonsensical to ask if 3 is less than
`NA`.

One solution is to fix the missing rows specifically:
```R
# Fix rows where ID_left is NA
vcf[is.na(ID_left), 'nearest_snp' := ID_right]

# Counterpart to previous line
vcf[is.na(ID_right), 'nearest_snp' := ID_left]  
```

But many other solutions exist!

</details>

---
## Generating rank order column with `frank`

`frank` is an optimized version of `rank`. This function is useful for
generating a new column containing numbers specifying the ordered rank
of another column. E.g. If a table contains count data, you can easily
create a new column where `1` is the most abundant, `2` is the second
most abundant, etc.

```R
# Generate an example table
dat <- data.table('geneID'=paste('GENE', LETTERS, sep=''),
                  counts=sample(1e6, size=26))
```

```R
# Assign new column with rank in ascending order
dat[, 'rank' := frank(counts)]

# Same, but for descending order
dat[, 'rank_reverse' := frank(-counts)]     
```
---

## String split across columns

`tstrsplit` is a transposed version of `strsplit`. As you might suspect,
the purpose of these functions is to split strings. Splitting strings
is often useful when a file name or column value contains multiple fields
with special meaning.

```R
dat <- fread('example_data.tsv')
dat[, 'sample_id' := tstrsplit(sample_info, split='_')[1] ]
dat[, 'sex' := tstrsplit(sample_info, split='_')[2] ]
dat[, 'ARM' := tstrsplit(sample_info, split='_')[3] ]
```

It is also possible to assign all three at the same time:
```R
dat <- fread('example_data.tsv')
dat[, c('sample_id','sex','ARM') := tstrsplit(sample_info, split='_')]
```

Note that the new columns will also be strings themselves. You may
need to include `as.numeric` to convert values to numbers as necessary.

## Binning data
       
The function `cut` can automatically assign columns to a group, as
defined by bin sizes of your choice:
       
```R
dat <- data.table(
    'ID'=1:1e5,
    'measurement'=sample(1:1000, size=1e5, replace=T)
)

# Assign bins by powers of 10
dat[, 'bin' := cut(measurement, breaks=c(0, 10, 100, 1000))]

# convert the output from 'cut' into number
dat[, bin := as.numeric(bin)]

dat[bin==1]
dat[bin==2]
dat[bin==3]
---

[PREV](C.md) | [HOME](/README.md) | [NEXT](/04_exporting_data/README.md)

<details><summary>How sample data was generated</summary>

```R
library(data.table)
library(foreach)
set.seed(1)

dat <- foreach(i=1:200, .combine='rbind') %do% {
    data.table('sample_info'=paste(
        sample(1000:9999, size=1),
        sample(c('M','F'), size=1),
        sample(c('Case','Control'), size=1),
        sep='_'))
}
dat[, 'measurement1' := runif(nrow(dat))]
dat[, 'measurement2' := floor(runif(nrow(dat))*100)]

dat <- dat[order(sample_info)]
fwrite(dat, file='example_data.tsv', sep='\t')
```

</details>
