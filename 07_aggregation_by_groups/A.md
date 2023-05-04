# Advanced aggregation

While we've thus far used single commands in `j`, you aren't limited to just one!
The real power of `data.table` lies in the ability to perform multiple calculations
at the same time.

```R
# Re-initialize dat
set.seed(1)
dat <- data.table('group'=sample(LETTERS, size=1000, replace=TRUE),
                  'count'=sample(100, size=1000, replace=TRUE))
```

The following command would calculate means for every unique `group`:
```R
# Calculaing mean
dat[, list('count_mean'=mean(count)), by=group]
```

Adding an additional summary statistic:
```R
# Simultaneously calculating mean and sd
dat[, list('count_mean'=mean(count), 'count_sd'=sd(count)), by=group]

# Equivalent, perhaps easier to read
dat[, list('count_mean'=mean(count),
           'count_sd'=sd(count)),
        by=group]
```

Formatting across multiple lines gets useful when doing a lot of operations:
```R
dat[, list('N'=.N,
           'count_mean'=mean(count),
           'count_sd'=sd(count),
           'count_median'=median(count),
           'count_min'=min(count),
           'count_max'=max(count)),
        by=group]
```



## On your own

Next we want to calculate the standard deviation for counts of all rows where group is a vowel.



How would you calculate the number of times `count` is at least 50? Aggregate
separately for consonants and vowels. The result should have two columns: one that identifies `consonant` or `vowel`, and `N` with the counts. 

*Hint: first generate a new column that identifies that row as `consonant` or `vowel`.

<details><summary>Solution</summary>

```R
# Initialize a vector of vowels
vowels <- c('A','E','I','O','U')

# Assign new column depending on group being consonant or vowel
dat[group %in% vowels, 'type' := 'vowel']
dat[! group %in% vowels, 'type' := 'consonant']

# Aggregate by group
dat[count >= 50, .N, by=type]
```

Yielding the result:
```
        type   N
1: consonant 404
2:     vowel 103
```

</details>

---

How would you calculate the standard deviation of `count` for vowels and consonants?

<details><summary>Solution</summary>

You include multiple conditions in `j`. Don't forget to assign column names!

```R
dat[, list('counts_sd' = sd(count), 'counts_mean'=mean(count)), by=type]
```

Yielding the result

```
        type counts_sd counts_mean
1: consonant  28.73418      50.540
2:     vowel  29.62306      51.165
```

</details>

dat[group %in% c('A','E','I','O','U')]              

dat[group %in% c('A','E','I','O','U'), sd(count)]   # then calculate sd on count
```

What if we wanted to calculate their standard deviations separately? All that's needed is to add the
`by=group` to the command.

```R
dat[group %in% c('A','E','I','O','U')]              # Reminder: %in% to match a set

dat[group %in% c('A','E','I','O','U'), sd(count), by=group]   # then calculate sd on count
```



```R
vowels <- c('A','E','I','O','U')
dat[group %in% vowels, list('SD'=sd(count)), by=group]
dat[group %in% vowels, .('SD'=sd(count)), by=group]     # .() is equivalent to list()
```

---

[PREV](README.md) | [HOME](/README.md) | [NEXT](/08_iterating_with_foreach/README.md)
