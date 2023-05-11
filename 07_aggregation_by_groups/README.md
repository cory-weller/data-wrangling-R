# Aggregating data by groups

Calculating summaries for statistics across groups.

Thus far we've referred to `i` and `j` notation, but there's also a
third category, known as `by`.

By including `by` in our `data.table` command, we can automatically
perform operations separately for different groups.

Functionally, when you include a column in `by`, every other operation
specified in the `data.table` command will be conducted on a subset of
the data:

![](/assets/group-by.png)

## Counting groups by `.N`

One of the most common tasks is counting occurrences per group, such as:
* counting the number of samples per treatment group
* counting the number of outcomes per treatment, across all samples
* counting the number of genes per group, etc.

The `.N` variable is a shortcut for counting number of rows:

First, initialize this familiar table:
```R
set.seed(1)
dat <- data.table(
    'group'=sample(LETTERS, size=1000, replace=TRUE),
    'count'=sample(100, size=1000, replace=TRUE)
)
```

If we only were interested in how many times each letter shows up in `dat`:

```R
dat[, .N, by=group]
```

Alternatively, if we wanted to know how many times each `group` has a
`count` above 80, we would add a filter in `i`:

```R
dat[count > 80, .N, by=group]
```

## Counting by multiple groups

We aren't limited ty group by a single column. We can include as many
columns as we want within a list, i.e. `by=list(col1, col2, col3)`.

First, re-initialize our table of ARM and outcome:
```R
set.seed(1)
dat.groups <- data.table(
    'PatientID'=paste0('PAT-', 1:50),
    'ARM'=sample(c('treatment','control'), size=50, replace=TRUE)
)

dat.outcomes <- data.table(
    'PatientID'=sample(dat.groups$PatientID, size=40),
    'Outcome'=sample(0:1, size=40, replace=TRUE)
)

dat.merged <- merge(dat.groups, dat.outcomes, all=TRUE)
```

We can then calculate occurrences for every combination of `ARM` and
`Outcome`:
```R
# Counts for all combinations:
dat.merged[, .N, by=list(ARM, Outcome)]

# Same, but first filtering out NA outcomes:
dat.merged[!is.na(Outcome), .N, by=list(ARM, Outcome)]      
```


[PREV](README.md) | [HOME](/README.md) | [NEXT](A.md)
