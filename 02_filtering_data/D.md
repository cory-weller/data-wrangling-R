# Useful filter functions

`data.table` includes several convenience functions for filtering data.

We'll use a bigger example this time[^1]

```R
bed <- fread('transcripts.bed',
             select=1:4,
             col.names=c('CHR','start','stop','ENSEMBL'))
```

Check the structure of the object. Note that the `bed` object has chromosome ID in the `CHR` column, but there's more than just the 'usual' autosomes. We can look at all the values in the `CHR` column:
```R
unique(bed$CHR)
```
Say we want to subset the data to only include the values of the typical autosomes (including X and Y). Writing out a filter to exclude the others would be fairly cumbersome based on what we've done so far.


## Selecting a defined set with `%in%`
The `%in%` operator works similar to `==` but works for multiple values. For example, if we want to subset the `bed` object where `CHR` is only chromosomes 1-3, we could do:
```R
bed[CHR == 'chr1' | CHR == 'chr2' | CHR == 'chr3']
```

But that's a lot of repetition. Instead, we can use `%in%` as follows:
```R
bed[CHR %in% c('chr1','chr2','chr3')]
```

If we first build a character vector of our desired values, we can then subset the data using `%in%`. Check the contents of this character vector created using `paste`:[^2]

```R
desired_chrs <- paste('chr', c(1:22, 'X', 'Y'), sep='')
```

Now that we have our vector of desired values, we can filter using `%in%`:
```R
new_bed <- bed[CHR %in% desired_chrs]
```

Check the values in the `CHR` column of this newly generated object to confirm the results.

You can combine `!` with `%in%` to get the inverse as well:
```R
bed[! CHR %in% desired_chrs]
```

---

## Filtering numeric values within a range using `%between%`

The %between% operator is an optimized shorthand function that checks if the numeric value in a column is within the bounds of two values:
```R
min_val <- 1000000
max_val <- 1005000
bed[start >= min_val & start <= max_val]    # 'typical' syntax

bed[start %between% c(min_val, max_val)]    # equivalent, but easier to understand
```

---

## Pattern-matching strings with `%like%`

The `%like%` operator returns rows where the specified column matches a defined text pattern (including regular expressions if desired).

This actually gives us a simpler method of filtering `bed` on the `CHR` column. We can subset only rows that contain the string 'chr':

```R
filter_by_in <- bed[CHR %in% desired_chrs]    # previous method
filter_by_like <- bed[CHR %like% 'chr']       # same result?
filter_by_like_regex <- bed[CHR %like% '^chr[0-9]?|[XY]']  # more specific, using regular expressions
```

Do these provide equivalent results? We might suspect so based on row numbers. But we can check with the function `identical`:

```R
identical(filter_by_in, filter_by_like)
identical(filter_by_in, filter_by_like_regex)
```


---
## On your own

Using one of these convenience functions, how might you select only rows pertaining to the sex chromosomes?
<details><summary>Answer</summary>
 
```R
bed[CHR %in% c('chrX','chrY')]
```

</details>

---

How could you check whether all values in `ENSEMBL` start with the string `'ENSG'`?
<details><summary>Answer</summary>
 
```R
bed[! ENSEMBL %like% 'ENSG']        # returns empty data.table
bed[ENSEMBL %like% 'ENSG']          # returns all rows from bed
```

</details>



---

[PREV](B.md) | [HOME](/README.md) | [NEXT](/03_column_operations/README.md)


[^1]: `select=(1:4)` tells `fread` to only import columns 1, 2, 3 and 4.
`col.names` is used to give meaningful names instead of `V1` `V2`... etc, as the file does not contain headers.

[^2]: `paste` is a very useful command that stitches together values and returns a character vector. In our case, all values should start with 'chr' then end with either a number 1-22 or X or Y. We specify `sep=''` because we don't want anything put between 'chr' and '1', for example, but sometimes you want to include a separator like hyphens or underscores, etc.