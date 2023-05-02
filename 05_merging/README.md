# Merging multiple tables



## Background

Need to know what column is being used to merge.

That column must be unique

`by` determines what column (or columns) are being used for the merge.

If you are merging on a single column, that value must be unique.

If you are merging on multiple columns, each combination of those columns must be unique.

If the uniqueness condition isn't satisfied, how would R know which one to pick when merging?

If you want to merge two tables:
* `dat.1` containing columns `A` `B` `C`

* with `dat.2` containing `A` `D` `E`

* to yield `dat.3`, the merged table `A` `B` `C` `D` `E`

Then the values in column A must be unique in both `dat.1` and `dat.2`.


## Inner joins
An inner join refers to only keeping keys (or key combinations) that exist in both tables. It's akin to the intersection of two circles in a Venn diagram.
```
merge(dat1, dat2)
```

## Left or Right Outer join
A Left outer join refers to only keeping keys (or key combinations) that exist in the first (left) table. It's akin to the entire left circle in a Venn diagram.

```
merge(dat1, dat2, all.x = TRUE)
```

Conversely, a right outer join refers to only keeping keys in the second (right) table--the entire right circle in a Venn diagram.
```
merge(dat1, dat2, all.y = TRUE)
```

## Full outer join
A full outer join keeps everything, whether or not both tables match, so no values are dropped. It's akin to the union of both circles of a Venn diagram.

```
merge(dat1, dat2, all.x = TRUE, all.y = TRUE)
merge(dat1, dat2, all = TRUE)
```

## Final note
`merge` only finds intersections or unions of values that exist in the original data. It won't generate new combinations that don't already exist.