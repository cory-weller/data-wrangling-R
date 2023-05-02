# Removing columns
in `data.table` you can remove columns by assigning them to `NULL`
```R
dat[, col4 := NULL]     # remove one column
```

To remove multiple columns at one time
```R
dat[, c('col2', 'col3') := NULL]     # remove one column

```
---
[PREV](A_math_operations.md) |
[HOME](/README.md) |
[NEXT](C_combined_operations.md)