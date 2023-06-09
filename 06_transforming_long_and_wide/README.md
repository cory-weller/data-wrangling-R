# Transforming data between long and wide

Data is commonly referred to as being in *wide* or *long* formats, even if it contains the same
information. As expected, long-format data has many rows and few columns. Wide-format data contains
many columns.

The difference between long and wide is demonstrated here:

![](/assets/wide-v-long.png)


Examples of the same data, represented in wide and long formats:
```R
dat.wide <- fread('rna_seq_sample.tsv')
dat.long <- fread('rna_seq_sample_long.tsv')
```

The underlying data is the same, but its organization is different.

---

[HOME](/README.md) | [NEXT](A.md)

<details><summary>How wide and long format data was generated</summary>

```R
set.seed(1)
dat <- data.table(
    'SYMBOL'=paste0('GENE_', sapply(
        1:2000,
        function(x) paste0(sample(LETTERS, size=3), collapse='')
    ))
)
dat <- unique(dat)
dat <- dat[order(SYMBOL)]

samplenames <- paste0('Sample', LETTERS[1:5])
for(samplename in samplenames) {
    new_counts <- abs(floor(jitter(rpois(nrow(dat), lambda=1))**8))
    dat[[samplename]] <- new_counts
}

fwrite(dat, file='rna_seq_sample.tsv', sep='\t')

dat.long <- melt(
    dat,
    measure.vars=samplenames,
    variable.name='SAMPLE',
    value.name='counts'
)

setcolorder(dat.long, c('SAMPLE','SYMBOL','counts'))

fwrite(dat.long[counts != 0], file='rna_seq_sample_long.tsv', sep='\t')
```

</details>