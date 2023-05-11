# Transforming to wide format

## Why use wide format?

In wide format, it's simple to perform calculations on individual rows,
which retain all of its values across separate columns. Wide format
data is often smaller in size (memory or disk size), when compared to
long format. To understand why, compare the wide and long data we've
been looking at.

```R
# If necessary to reload
dat.wide <- fread('rna_seq_sample.tsv')
dat.long <- fread('rna_seq_sample_long.tsv')
```

`dat.wide` includes the Gene symbols (`GENE_XXX`, etc) and Sample
names (`SampleA`, etc) only once in the entire table.

`dat.long`, on the other hand, repeats the gene symbols and sample
names for every row of the table. This results in the long format
taking up more space when written to the disk, even though all the
rows with a count of 0 have been excluded!

## Transform to wide with `dcast`
The following image illustrates the structure of a `dcast` formula:

![](/assets/dcast-illustration.png)

* Things that remain how they are (as columns) go to the left of `~`
* The column containing a group variable, each of which make a new
column, goes to the right of `~`
* The name of the value column is specified with `value.var=`

Using these rules, we'd structure our `dcast` formula to convert
`dat.long` as:

```R
# Convert dat.long from long to wide
dcast(dat.long, SYMBOL~SAMPLE, value.var='counts')
```

Note the structure that's printed out. It's similar to that of `dat.wide`,
but it ocntains `NA` values. This is because `dat.long` had those rows
filtered out, as they contained no additional information.

We can automatically repopulate these `NA` instead as `0` with `fill=0`:

```R
# Convert to wide and populate missing cells with 0 (instead of NA)
dcast(dat.long, SYMBOL~SAMPLE, value.var='counts', fill=0)
```

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](/07_aggregation_by_groups/README.md)
