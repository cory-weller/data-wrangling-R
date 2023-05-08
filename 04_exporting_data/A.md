# Writing data tables to text with `fwrite`

The function `fwrite` is the workhorse of saving any table as text
output such as tab-separated values (`.tsv`) or comma-separated values
(`.csv`). It's essentially the counterpart to `fread` when it comes to
exporting data.

```R
# Examples
fwrite(dat, file='filename.csv', sep=',')   # Write as csv
fwrite(dat, file='filename.csv')            # (equivalent)
fwrite(dat, file='filename.tsv', sep='\t')  # Write as tsv
```



## Writing tables as compressed text
Compressed text (e.g. with `gzip`) can save a lot of disk space for
larger files. `fwrite` automatically detects the `.gz` extension in
filenames and writes as compressed text.[^1]

```R
fwrite(dat, file='filename.txt.gz', sep='\t')  # Write as gzipped tsv
```


## On your own

Look at the `fwrite` docs to answer the following.

What happens to NA values by default when using `fwrite`?

<details><summary>Answer</summary>

`NA` values are by default written as a blank string.

</details>

---

Suppose you don't want the default behavior. How might you force
`fwrite` to write `NA` as `'NA'`?

<details><summary>Answer</summary>

By including `na='NA'` in `fwrite`
```R
fwrite(dat, file='output.csv', na='NA')
```


</details>

---

[PREV](/04_exporting_data/README.md) | [HOME](/README.md) | [NEXT](B.md)

[^1]: While `fread` acts smart here, take caution! On linux systems, file names have no REQUIRED association with the contents of the file itself. In fact, you could name the file anything, with any (or no) file extension, and it wouldn't make any difference to the contents. It is prudent to check the contents of the file match the desired outcome. Do not assume other tools will so smartly know how to handle file extensions you specify.