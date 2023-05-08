# Combining row and column operations

Thus far, we've separately tried subsetting rows in `i` and performing
column operations in `j`. But there's nothing stopping us from doing
both at the same time in a single command: `dat[i,j]`

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

However, note that `dat[,j][i]` is *not* necessarily equivalent. This
is because the `j` command would be operated on the complete data,
instead of the desired subset.

Notice what happens when `sum` command in `j` comes first.
```R
dat[,sum(count)]
```
In this case, the entire column is summed, which is equivalent to `sum(dat$count)`


## Conditional assignment

You can conditionally assign values to a column by first including a
row filter in `i`. Working with the same `dat` object as above, suppose
we know group `A` is dated `20230401` and group `B` is dated `20230501`.
We can assign those values in a new column named `date`:

```R
dat[group=='A', 'date' := 20230401]
```
Check the `dat` object to see what's happened before continuing.

We can then assign the other date value to group `B`:
```R
dat[group=='B', 'date' := 20230501]
```

---

## On your own

Initialize this example data set, look at its contents, and then attempt
the exercises. Note that `set.seed` will ensure the random sampling gives
everyone the same result.

```R
set.seed(1)
dat <- data.table('group'=sample(LETTERS, size=1000, replace=TRUE),
                  'count'=sample(100, size=1000, replace=TRUE))
```

Use the `quantile` function to calculate the default quantiles for group `Y`

<details><summary>Solution</summary>

```R
dat[group=='Y', quantile(count)]
```

yielding the result

```
   0%   25%   50%   75%  100% 
 2.00 23.00 45.00 58.75 99.00 
```

</details>

---

Use the `sd` function to calculate the standard deviation for counts
of all rows where group is a vowel.

<details><summary>Solution</summary>


```R
# define vowel values
vowels <- c('A','E','I','O','U')

# %in% selects rows where a column matches anything in a set
dat[group %in% vowels]

# calculate standard deviation after subsetting
dat[group %in% vowels, sd(count)]
```

</details>

---

Create a new column `letter_type` that appropriately contains 
`'consonant'` or `'vowel'` for each row.

<details><summary>Solution</summary>

```R
vowels <- c('A','E','I','O','U')
dat[group %in% vowels, 'letter_type' := 'vowel']
dat[! group %in% vowels, 'letter_type' := 'consonant']
```

</details>

---

[PREV](B.md) | [HOME](/README.md) | [NEXT](D.md)
