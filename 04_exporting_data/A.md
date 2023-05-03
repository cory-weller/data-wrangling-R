# Writing data tables to text with `fwrite`

The function `fwrite` is the workhorse of saving any table as text output such as tab-separated values (`.tsv`) or comma-separated values (`.csv`). It's essentially the counterpart to `fread` when it comes to exporting data.

```
fwrite(dat, file='filename.txt', sep=',')   # Write as csv
fwrite(dat, file='filename.txt')            # Write as csv (equivalent)
fwrite(dat, file='filename.txt', sep='\t')  # Write as tsv
```

## Writing tables as compressed text
Compressed text (e.g. with `gzip`) can save a lot of disk space for larger files.
`fwrite` automatically detects the `.gz` extension in filenames and writes as compressed text.
```
fwrite(dat, file='filename.txt.gz', sep='\t')  # Write as gzipped tsv
```


[PREV](/04_exporting_data/README.md) | [HOME](/README.md) | [NEXT](B.md)