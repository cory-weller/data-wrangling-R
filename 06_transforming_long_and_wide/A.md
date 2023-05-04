# Transforming to long format

Long-format data is typically useful for calculating summary stats or plotting.

```R
# If necessary to reload
dat.wide <- fread('rna_seq_sample.tsv')
dat.long <- fread('rna_seq_sample_long.tsv')
```

## Transforming to long with `melt`


---


[HOME](/README.md) | [NEXT](B.md)
