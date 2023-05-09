# Chaining Filters

Thus far, we've only applied a single statement in `i` (even if that
statement is testing multiple conditions with AND/OR operators).
Conveniently, `data.table` lets you chain multiple AND statements
together by appending them right after one another.

The `data.table` is evaluated at every stage to subset only the
specified rows, then applies the next filter, and so on.

Still working with the example `data.table` from before:
```R
dat <- data.table('N'=1:26, 'lower'=letters, 'upper'=LETTERS)
```

Examples:
```R
dat[N < 10 & N > 3]
dat[N < 10][N > 3]

dat[N > 20 & upper != 'Z']
dat[N > 20][upper != 'Z']
```

Chaining becomes even more useful later on after we introduce functions
that perform calculations and generate new columns, because we can
do calculations then filter on desired conditions at the same time.

---
## On your own

Convert the following `AND` command into chained format. Both commands
should yield the same result.
```R
dat[N > 5 & N < 20]
```

<details><summary>Answer</summary>
 
```R
dat[N >  5][N < 20]
dat[N < 20][N >  5]      # equivalent
```

</details>


---

[PREV](B.md) | [HOME](/README.md) | [NEXT](D.md)

