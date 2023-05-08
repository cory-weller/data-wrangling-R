# Operate on rows in `i` 

`data.table` refers to its operations as across rows as in `i`, a
notation borrowed from matrix math. You can specify which rows to
include (or exclude) in square brackets immediately following the
`data.table` object. 


## Extracting by row index
Say you have a object `dat`. Specifying numeric indices in `i` will
extract those rows.

Initialize an example `data.table` and evaluate what happens when
running the following commands:
```R
dat <- data.table('N'=1:26, 'lower'=letters, 'upper'=LETTERS)

dat[12]
dat[25]
dat[12:20]
dat[! 12:20]
dat[c(1:3, 7:12, 21:24)]
```

Note that so far we have only been calling a subset which is immediately
printed to the terminal, then 'forgotten' by R. In order to retain the
subset as an object, it has to be assigned to a variable:

```R
dat2 <- dat[! 12:20]    # Save subset as new variable
```



---

[PREV](README.md) | [HOME](/README.md) | [NEXT](B.md)

[^1]: And columns as in `j`, also equivalent to matrix notation.