# Transforming to long format

Long-format data is typically useful for calculating summary stats or plotting.
Generally, if you can represent the data with fewer columns, it's a more convenient data structure
for downstream analyses.

```R
# If necessary to reload
dat.wide <- fread('rna_seq_sample.tsv')
dat.long <- fread('rna_seq_sample_long.tsv')
```

## Transforming to long with `melt`

Structuring a `melt` command is relatively straightforward. Columns that are currently wide are
specified in `measure.vars`. 

```R
melt(dat.wide, measure.vars=c('SampleA','SampleB','SampleC','SampleD','SampleE'))
```

The new column names automatically default to `variable` and `value`, but we can specify them
within the `melt` command if desired:

```R
melt(dat.wide, measure.vars=c('SampleA','SampleB','SampleC','SampleD','SampleE'),
               variable.name='SAMPLE',
               value.name='counts')
```

---

[HOME](/README.md) | [NEXT](B.md)
