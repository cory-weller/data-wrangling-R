

## Counting groups by `.N`

First, initialize this familiar table:
```R
set.seed(1)
dat <- data.table('group'=sample(LETTERS, size=1000, replace=TRUE),
                  'count'=sample(100, size=1000, replace=TRUE))
```
Use the `sd` function to calculate the standard deviation for counts of all rows where group is a vowel.

```R
dat[group %in% c('A','E','I','O','U')]              # Reminder: %in% to match a set

dat[group %in% c('A','E','I','O','U'), sd(count)]   # then calculate sd on count
```

What if we wanted to calculate their standard deviations separately? All that's needed is to add the
`by=group` to the command.

```R
dat[group %in% c('A','E','I','O','U')]              # Reminder: %in% to match a set

dat[group %in% c('A','E','I','O','U'), sd(count), by=group]   # then calculate sd on count
```

Notice how the column containing the standard deviation is automatically named `V1`. We can assign
a name in `j` to whatever we want, however we need to wrap the command within a `list`

```R
vowels <- c('A','E','I','O','U')
dat[group %in% vowels, list('SD'=sd(count)), by=group]
dat[group %in% vowels, .('SD'=sd(count)), by=group]     # .() is equivalent to list()
```

[HOME](/README.md) | [NEXT](/09_iterating_with_foreach/README.md)
