# Cross-column operations

## Background
`data.table` notation uses the `:=` operator to assign new columns.
For example, say we have a table `dat`

Note the leading comma in the following template:
```
dat[, 'column_name' := <values or vector> ]
```

The leading comma is necessary for `R` to know we're working in the column dimension. 


## Changing column type Type

Check the structure of an R table
```
str(dat)
```

`as.character`

`as.numeric`

`as.factor`






---
[HOME](/README.md) |
[NEXT](A_math_operations.md)
