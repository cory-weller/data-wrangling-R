# Organizing columns

## Changing column names
When we look at the names of the columns in the `bed` object:
```R
bed                 # print table, can see headers
colnames(bed)       # print only headers
```
We can see that `start` and `stop` are lower case. That doesn't really matter, but for stylistic consistency, let's make it uppercase instead with `setnames`.
The basic syntax is `setnames(DT, oldnames, newnames)` where `oldnames` and `newnames` are character vectors of the same length.[^1] Alternatively, you can only specify the new names if you're renaming ALL of them at once:
```R
setnames(DT, oldnames, newnames)    # when renaming a subset of columns
setnames(DT, newnames)              # when renaming ALL columns
```

In this case, any of the following gets the job done:

```R
setnames(bed, c('start','stop'), c('START','STOP'))     
setnames(bed, colnames(bed), toupper(colnames(bed)))
setnames(bed, toupper(colnames(bed)))
```

---

## Subsetting columns
Similar to how we subset in `i` by specifying row indices, we can subset columns in `j` by specifying column indices OR column names. Take note of the leading comma, which is necessary to indicate we're working in `j`.

```R
bed[, c('START')]       # select by col name
bed[, 1]                # equivalent, by col index

bed[, c('START', 'ENSEMBL')]
bed[, c(1,4)]

bed[, ! c(1,4)]
bed[, ! c('START', 'ENSEMBL')]
```
---

## Re-ordering columns
Columns can be reordered using the `setcolorder` function. This simply reorganizes the order columns appear. This is more memory efficient than trying to 'subset' all of the columns in a new order.
```R
# re-initialize the bed object
bed <- fread('transcripts.bed',
             select=1:4,
             col.names=c('CHR','start','stop','ENSEMBL'))


setcolorder(bed, c('start','stop','CHR','ENSEMBL'))     # FAST, edited in-place
bed[, c('start','stop','CHR','ENSEMBL')]                # works, but makes a copy, is slower on big tables
```

---

## Removing columns

This syntax looks a bit odd, but removing a single column can be done by assigning it to `NULL`:

```R
bed[, ENSEMBL := NULL]              # remove one column
bed[, c('start','stop') := NULL]    # remove multiple columns
```

*Note that when removing multiple columns, column names must be a character vector!

Speaking of the `:=` operator...

---

[HOME](/README.md) | [NEXT](B.md)


[^1]: That character vector length can also be 1, i.e. a single string: `setnames(DT, 'V1', 'GeneID')`