# Assigning new columns

In `data.table` notation, new columns are assigned using the `:=` operator.
It just so happens that deleting a column is actually just assigning
it the value `NULL`:

```R
# Example syntax
dat[, col_to_delete := NULL]
```

We can put either values or commans to the right of `:=` when
generating new columns. 

First, re-initialize the `bed` object:

```R
bed <- fread('transcripts.bed',
             select=1:4,
             col.names=c('CHR','start','stop','ENSEMBL'))
```

Say we want to add a column with the same value for all rows, identifying
the dataset's ID. We can assign the same string to all rows as follows:

```R
bed[, 'date' := '20230509']
```

recheck `bed` to confirm the results.

## Math operations on columns

We can use math across columns to calculate new values. Say we want to
determine the length of the ranges in the `bed` table.

```R
bed[, 'len' := stop - start]
```

## Changing column types

Oops! Just a moment ago we assigned the column `date` as a character,
which we can confirm by running `str(bed)` to check the structure of the
table.

We actually want it to be a number. We can convert it with `as.numeric`:

```R
# re-assign the date column as numeric
bed[, date := as.numeric(date)]     
```

---

## Pattern replacement

With this new `subset_bed` table, suppose we want to ONLY have the
chromosome ID, without `'chr'` included in the text. We can use `gsub`
to match-and-replace by pattern. 

`gsub` follows the syntax `gsub(pattern, replacement, x)` where
* `pattern` is the text to look for
* `replacement` is the text to take its place
* `x` is the vector (or column name) we are searching through

We can use `gsub` to make a new column `chrID` that excludes the text `'chr'`

```R
bed[, 'chrID' := gsub('chr', '', CHR)]
```
Specifically, in this example,
* `'chrID'` is the name of the new column to add
* `'chr'` is the pattern we are searching for
* `''` is the pattern (empty string) we are replacing `'chr'` with
* `CHR` is the name of the column we are searching in

Check the results to confirm.

---

## On your own

Suppose you are looking at a single sample's data from an RNA-seq
experiment. First load in `rna_seq_sample.tsv` using `fread`.

```R
rnaseq_sample <- fread('rna_seq_sample.tsv', select=1:2)
```


How would you create a new column that contains the log2 transformation
of the `SampleA` counts? Note that we often take `log2` of `(count value +1)`
in order to prevent `-Inf` results!

<details><summary>Solution</summary>

```R
rnaseq_sample[, 'log2counts' := log2(SampleA + 1)]
```

*Note that all values should start as positive integers. Otherwise we*
*might want to first take the absolute values with `abs()` before `log2()`*

</details>

---

How might you calculate the median of the top ten highest `log2counts`?

<details><summary>Solution</summary>

Building the command step by step:
```R
# reorder the rows in descending order
rnaseq_sample[order(-log2counts)]       

# Subset to the first 10 rows of the reordered table
rnaseq_sample[order(-log2counts)][1:10] 

# Calculate the median
rnaseq_sample[order(-log2counts)][1:10, median(log2counts)]
```

</details>

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
