# Chaining Filters

Thus far, we've only applied a single statement in `i` (even if that statement is testing multiple conditions with AND/OR operators). Conveniently, `data.table` lets you chain multiple AND statements together by appending them right after one another.

The `data.table` is evaluated at every stage to subset only the specified rows, then applies the next filter, and so on.

Still working with the example `data.table` from before:
```R
dat <- data.table('N'=1:26, 'lower'=letters, 'upper'=LETTERS)
```

Run the following command and see what happens:
```R
dat[N < 10][N > 3]
```


---
## On your own

Convert the following `AND` command into chained format. Both commands should yield the same result.
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

