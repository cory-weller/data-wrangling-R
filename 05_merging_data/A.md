# Binding rows or columns

In `R`, binding refers to the combining of data sets by pasting rows or columns together. Perhaps you
have two tables that have the same columns, and you want to combine them into a single table. It's
typically necessary that the data is the same length to properly be bound together.

## Binding rows with `rbind` or `rbindlist`
Say we have two separate tables, but they contain the same column structure:
```R
dat1 <- data.table('group'=LETTERS[1:13], 'X'=runif(13))
dat2 <- data.table('group'=LETTERS[14:26], 'X'=runif(13))
```

we can *bind* the *rows* with `rbind`:[^1]
```R
rbound <- rbind(dat1, dat2)
```

## Binding columns with `cbind`

The same principal applies to combining data in a column-wise fasion. 

```R
dat3 <- data.table('group'=LETTERS, 'X'=runif(26))
dat4 <- data.table('group'=LETTERS, 'Y'=runif(26))

cbound_1 <- cbind(dat3, dat4)         # Note what happens
cbound_2 <- cbind(dat3, dat4[,'Y'])   # Without duplicate 'group' column
```

Binding columns is less common, because it's not typically the case that you have pre-sorted vectors
ready to tack onto an existing data set. Instead, it's more typical to perform a `join`, covered in the next section.

[HOME](/README.md) | [NEXT](B.md)

[^1]: Confusingly, `data.table` can operate with `rbindlist` instead of `rbind`. The general
premise is the same, but the objects being bound can be enclosed within a list, e.g. `rbindlist(list(dat1, dat2))`.
This is important for advanced operations using `foreach`, which returns a list of objects, and will
not work with plain old `rbind`.