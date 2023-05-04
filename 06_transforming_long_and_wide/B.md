# Transforming to wide format

## Why use wide format?

In wide format, it's simple to perform calculations on individual rows,
which retain all of its values across separate columns. Wide format data is often
smaller in size (memory or disk size), when compared to long format. To understand why, compare the wide and long data we've been looking at.

```R
# If necessary to reload
dat.wide <- fread('rna_seq_sample.tsv')
dat.long <- fread('rna_seq_sample_long.tsv')
```

`dat.wide` includes the Gene symbols (`GENE_XXX`, etc) and Sample names (`SampleA`, etc) only once in the entire table.

`dat.long`, on the other hand, repeats the gene symbols and sample names for every row of the table. This results in the long format taking up more space when written to the disk, even though all the rows with a count of 0 have been excluded!

## transform to wide with `dcast`




---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
