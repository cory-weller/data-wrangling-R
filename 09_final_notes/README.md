# Final Notes

## Learning to use `.SD` in `data.table`
In `data.table`, `.SD` stands for **S**ubset of **D**ata. It is an
alias for a variable. It is most often used in `j` to represent a
subset of columns (specified with `.SDcols=`) to include when performing
calculations.

```R
vcf <- fread('missing.vcf')
sample_names <- colnames(vcf[,-(1:9)])
info_cols <- colnames(vcf)[1:9]

vcf[, .SD, .SDcols=sample_names]
vcf[, .SD, .SDcols=info_cols]
```

`.SD` is particularly useful when performing the same operation across
multiple columns, and you don't want to include every column name in
your command. For example, calculating the number of columns with `.|.`
as the genotype.

```R
# Calculate sample genotype missingness for every row:
vcf[, apply(.SD, MARGIN=1, function(x) sum(x=='.|.')),
            .SDcols=sample_names]
```

Breaking apart the function into its pieces:
* `apply` is a function for applying a function across every value in a list.
* `.SD` is the data.table subset we specified (only sample genotype columns)
* `MARGIN` specifies the dimension to apply the function, 1=ROW, 2=COLUMN
Note what happens if we use `MARGIN=2`:

```R
vcf[, apply(.SD, MARGIN=2, function(x) sum(x=='.|.')), 
            .SDcols=sample_names]
```

Thus, the above code applies the `sum(x=='.|.')` function to every row
in the `data.table` subset containing *only* sample genotypes. That is,
it calculates the number of 'missing data' values per position.

The function called within `apply` can be specified as anything you want.
It can even be defined entirely outside the `apply` command:

```R
count_missing <- function(genotypes) {
    # Counts the number of missing genotypes,
    missing <- c('.|.', 'NA', '', NA)
    n_missing <- sum(genotypes %in% missing)
    return(n_missing)
}

vcf[, apply(.SD, 1, count_missing), .SDcols=sample_names]
```

For more examples (and detailed description) see this writeup hosted
[here](https://cran.r-project.org/web/packages/data.table/vignettes/datatable-sd-usage.html)

```R
# Import data
vcf <- fread('missing.vcf')

# Rename '#CHR' column because # is problematic symbol
setnames(vcf, '#CHROM', 'CHROM')

# Get sample names by calling colnames on everything except col 1:9
sample_names <- colnames(vcf[,-(1:9)])

nucleotides <- c('C','T','A','G')

# Subset to only include SNPs
vcf <- vcf[REF %in% nucleotides][ALT %in% nucleotides]

# Calculate missingness rate using .SD
vcf[, N_missing := apply(.SD, 1, function(x) sum(x=='.|.')), .SDcols=sample_names]
vcf[, N := length(sample_names) - N_missing]
vcf[, pct_missing := N_missing/N]


# Filter to missingness rate <= 10%
vcf <- vcf[pct_missing < 0.1]

# Calculate genotype frequencies
vcf[, observed_homref := apply(.SD, 1, function(x) sum(x=='0|0')),
        .SDcols=sample_names]

vcf[, observed_het := apply(.SD, 1, function(x) sum(x %in% c('0|1','1|0'))),
        .SDcols=sample_names]

vcf[, observed_homalt := apply(.SD, 1, function(x) sum(x=='1|1')),
        .SDcols=sample_names]

# Drop sample columns for ease of working with data
# Note the 'with=F' argument is required when using
# a variable that represents a vector of column names
vcf <- vcf[, ! sample_names, with=F]

# Total n ref alleles: 2 per homozygote, 1 per heterozygote
vcf[, nRef := 2*observed_homref + observed_het]

# Same, but for alternate alleles:
vcf[, nAlt := 2*observed_homalt + observed_het]

# Exclude 'fixed' alleles that do not vary in population
vcf <- vcf[nRef != 0][nAlt != 0]

# Calculate p and q (fraction of ref and alt alleles)
vcf[, p := nRef / (nRef + nAlt)]
vcf[, q := nAlt / (nRef + nAlt)]

# Calculate expected genotype frequencies based on p and q
vcf[, expected_homref := N*p**2]
vcf[, expected_het := N*p*q]
vcf[, expected_homalt := N*q**2]


# Collect vector of column names with 'observed' or 'expected' in name
mycols <- colnames(vcf)[colnames(vcf) %like% c('observed|expected')]

vcf.long <- melt(vcf, measure.vars=mycols,
                    variable.name='genotype_category',
                    value.name='genotype_frequency')

# Split 'genotype_category' column into two
vcf.long[, c('group','genotype') := tstrsplit(genotype_category, '_')]

# Cast the 'group' column from long to wide
vcf.wide <- dcast(vcf.long, 
                  CHROM+POS+ID+genotype~group,
                  value.var='genotype_frequency'
)

vcf.wide <- dcast(vcf.long, ID~variable, value.var='value')


# Calculate Chi-square statistic for every position,
# SUM of (Obs-Exp)^2 / Exp 
vcf.wide[, X := (observed-expected)**2]
vcf.wide[, X := X / expected]
vcf.stats <- vcf.wide[, list('X'=sum(X)), by=list(ID,genotype)]
vcf.stats[, 'p' := pchisq(X, df=1, lower.tail=FALSE)]

# Assign vector of significance
vcf.stats[, 'signif' := ifelse(p < 0.05, TRUE, FALSE)]

# Bin the data by megabase (1e6)
vcf.stats[, 'genomic_bin' := cut(POS, breaks=seq(0,50e6, 1e6))]

# Count the number of significant SNPs per megabase
vcf.stats[, list('N_signif'=sum(signif)), by=genomic_bin]
```



## setting up an `.Rprofile` 
I personally use some packages for every single project, such as
`ggplot2`  `data.table` and `foreach`. Instead of manually loading
each of these packages every time I start `R`, I can automate it using
a custom `.Rprofile`. The file lives in my home directory on Biowulf
(i.e. `~/.Rprofile`) and contains the following:

```R
library(data.table)
library(ggplot2)
library(foreach)
```


You can add these to your own `.Rprofile` by running the following
in the `bash` command-line (NOT within `R`).
```bash
echo 'library(data.table)' >> ~/.Rprofile
echo 'library(ggplot2)' >> ~/.Rprofile
echo 'library(foreach)' >> ~/.Rprofile
```
As a result, these packages load every thing I start up R.


## Running `R` on Biowulf, in `VS Code` or `Rstudio`
Your local machine just doesn't have the same compute power as the
Biowulf clusters. See instructions [here](https://hpc.nih.gov/apps/RStudio.html)
for setting up `Rstudio` to run on Biowulf.

For those who prefer to use `VScode`, there's a separate tutorial hosted
[here](https://hpc.nih.gov/apps/vscode.html). There are also instructions
for running Jupyter notebooks on Biowulf through `VS Code` in this manner.

## Brush up on `bash`
Becoming an `R` expert can only get you so far. Many computational tasks
require interfacing with the `bash` command-line in a Linux environment.

## Don't stop here!
These tutorials have gone over (most of) the basic necessities of
wrangling data in `R` using `data.table` and `foreach`. Practice makes
perfect, and you're encouraged to work through any yet-incompleted
practice problems. And continue practicing on your own!




[HOME](/README.md)
