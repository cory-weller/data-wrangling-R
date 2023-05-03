# Assigning new columns

In `data.table` notation, new columns are assigned using the `:=` operator.
It just so happens that deleting a column is actually just assigning it the value `NULL`:

```R
# Example syntax
dat[, col_to_delete := NULL]
```

We can put either values or commans to the right of `:=` when generating new columns. 

First, re-initialize the `bed` object:

```R
bed <- fread('transcripts.bed',
             select=1:4,
             col.names=c('CHR','start','stop','ENSEMBL'))
```

Say we want to add a column with the same value for all rows, identifying the dataset's ID. We can assign the same string to all rows as follows:

```R
bed[, 'date' := '20230509']
```

recheck `bed` to confirm the results.

## Math operations on columns

We can use math across columns to calculate new values. Say we want to determine the length of the ranges in the `bed` table.

```R
bed[, 'len' := stop - start]
```

## Changing column types

Oops! Just a moment ago we assigned the column `date` as a character, which we can confirm by running `str(bed)` to check the structure of the table.

We actually want it to be a number. We can convert it with `as.numeric`:

```R
bed[, date := as.numeric(date)]     # re-assign the same column as numeric
```

---

## Pattern replacement

With this new `subset_bed` table, suppose we want to ONLY have the chromosome ID, without `'chr'` included in the text. We can use `gsub` to match-and-replace by pattern. 

`gsub` follows the syntax `gsub(pattern, replacement, x)` where
* `pattern` is the text to look for
* `replacement` is the text to take its place
* `x` is the vector (or column name) we are searching through

How would you use `gsub` to make a new column `chrID` that excludes the text `'chr'`?

<details><summary>Answer</summary>


```R
bed[, 'chrID' := gsub('chr', '', CHR)]
```

Check the results to confirm.
```R
unique(bed$CHR)
unique(bed$chrID)
```

</details>

---

Suppose you have some RNA expression data, with a column `counts`. How would you create a new column that contains the log2 transformation of these counts?

<details><summary>Answer</summary>


```R
# For example,
dat[, 'log2counts' := log2(counts)]
```

</details>

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
