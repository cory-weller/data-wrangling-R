# Math operations
Operate across columns using mathematical operators

```R
# initialize new data.table
dat <- data.table(col1=sample(1:100, size=25), 
                  col2=sample(1:100, size=25))

# arithmetic operations
dat[, col3 := col1 + col2]
dat[, col4 := col1 - col2]
dat[, col5 := col1 * col2]
dat[, col6 := col1 / col2]
```

Notice `col6` contains decimals, as a result of division. 

Rounding down to nearest integer
```R
dat[, col7 := floor(col6)]
```

Rounding up to nearest integer
```R
dat[, col8 := ceiling(col6)]
```
[01: Importing data](/01_importing_data/README.md)

[02: Filtering data](/02_filtering_data/README.md)

[03: Reorganizing columns](/03_reorganize_columns/README.md)

[04: Cross-column operations](/04_column_operations/README.md)

[05: Merging data](/05_merging/README.md)

[06: Exporting data](/06_exporting/README.md)

[04: Cross-column operations](/04_column_operations/README.md)

[04: Cross-column operations](/04_column_operations/README.md)

[04: Cross-column operations](/04_column_operations/README.md)

---
[PREV](/04_column_operations/README.md) |
[HOME](/README.md) |
[NEXT](/04_column_operations/B_removing_columns.md)

