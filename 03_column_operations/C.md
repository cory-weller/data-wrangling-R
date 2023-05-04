# Combining row and column operations

Thus far, we've separately tried subsetting rows in `i` and performing column operations in `j`.
But there's nothing stopping us from doing both at the same time in a single command: `dat[i,j]`

This is functionally the same as chaining together an `i` then a `j` command:

```R
dat[i][,j]
dat[i,j]        # equivalent
```

Example:

```R
# Initialize example data
dat <- data.table('group'=sample(c('A','B'), size=20, replace=TRUE),
                  'count'=sample(100, size=20))

dat[group=='B']                 # Subset to only group B
dat[group=='B', sum(count)]     # Subset only group B, then sum counts
dat[group=='B'][, sum(count)]   # equivalent
```

However, note that `dat[,j][i]` is *not* necessarily equivalent. This is because the `j` command would be operated on the complete data, instead of the desired subset.

Notice what happens when `sum` command in `j` comes first.
```R
dat[,sum(count)]
```
In this case, the entire column is summed, which is equivalent to `sum(dat$count)`


## Conditional assignment

## `ifelse` conditional assignment

---

## On your own

Initialize this example data set and then attempt the exercises.
Note that `set.seed` will ensure the random sampling gives everyone the same result.

```R
set.seed(1)
dat <- data.table('group'=sample(LETTERS, size=1000, replace=TRUE),
                  'count'=sample(100, size=1000, replace=TRUE))
```

Use the `quantile` function to calculate the default quantiles for group `Y`

```R
dat[group=='Y', quantile(count)]
```

yielding the result

```
   0%   25%   50%   75%  100% 
 2.00 23.00 45.00 58.75 99.00 
```

---

Use the `sd` function to calculate the standard deviation for counts of all rows where group is a vowel.

```R
dat[group %in% c('A','E','I','O','U')]              # Reminder: %in% to match a set

dat[group %in% c('A','E','I','O','U'), sd(count)]   # then calculate sd on count
```

ifelse




---

[PREV](B.md) | [HOME](/README.md) | [NEXT](D.md)
