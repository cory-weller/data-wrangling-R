# Joins

To **join** data means to combine based on matching **keys**. A key is a column of values shared between two tables that can be used to link shared identity.

Perhaps you have a two tables:

```R
set.seed(1)
dat.groups <- data.table('PatientID'=paste0('PAT-', 1:50),
                    'ARM'=sample(c('treatment','control'), size=50, replace=TRUE))

dat.outcomes <- data.table('PatientID'=sample(dat.groups$PatientID, size=40),
                    'Outcome'=sample(0:1, size=40, replace=TRUE))
```

Check the structure of the two tables. In this example, `dat.outcomes` has fewer rows because some patients dropped out of the study.

Firstly, `rbind` wouldn't make sense because the columns are not the same. 

Secondly, while we do want to combine by columns, the two tables have different numbers of rows, AND the patient IDs are in different order. Try using `cbind` to combine the tables and note what happens.

## Joining data with `merge`

The desired table should contain only three columns: the `PatientID` and the corresponding `ARM` and `Outcome` for that patient. To combine these data sets, we
use `merge` with the `PatientID` column as our key.

```R
dat.merged <- merge(dat.groups, dat.outcomes, by='PatientID')
```

The resulting table contains only the patients that are present in both tables.
This is referred to as an *inner join*, and can be thought of the overlap of two
circles in a Venn diagram.

If we wanted to retain all patients even if they're not present in both tables, we
can add `all=TRUE` to the `merge` command:

```R
dat.merged2 <- merge(dat.groups, dat.outcomes, by='PatientID', all=TRUE)
```

Note that any missing values are filled with `NA`.

This is referred to as a *full outer join* because it includes all data from both sets.[^1]

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](/06_transforming_long_and_wide/README.md)


[^1]: There is also less commonly the *left outer join* and *right outer join* that retains all keys from the first or second table, respectively.