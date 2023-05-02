# Cross-column operations

## Background
`data.table` notation uses the `:=` operator to assign new columns.
For example, say we have a table `dat`

Note the leading comma in the following template:
```
dat[, 'column_name' := <values or vector> ]
```

The leading comma is necessary for `R` to know we're working in the column dimension. 

## Type

as.character
as.numeric
as.factor

## Math operations
Operate across columns using mathematical operators

```R
# initialize new data.table
dat <- data.table(col1=sample(1:100, size=25), 
                  col2=sample(1:100, size=25))

# arithmetic operations
dat[, col3 := col1 + col2]
dat[, col4 := col1 - col2]
dat[, col5 := col1 * col2]
dat[, col6 := col1 / col2]
```

Notice `col6` contains decimals, as a result of division. 

Rounding down to nearest integer
```R
dat[, col7 := floor(col6)]
```

Rounding up to nearest integer
```R
dat[, col8 := ceiling(col6)]
```

---

## Combining row and column operations
So far, we've put nothing before the comma in these `data.table` column assignment commands. However, we can include a statement that conditionally assigns new values.

```
#       row         col       values
# dat[<condition>, colname := <operation>]
```

Before we try conditional column assignment, here's an example where we apply conditional filter to only show rows where the value in `col1` is even. The `%%` operator shows the remainder after division, and any even number is evenly divisible by 2 with no remainder.
```R
dat[col1 %% 2 == 0]     # only prints rows where col1 is even
```

We can assign a new column `isEven` as follows:
```R
dat[col1 %% 2 == 0, isEven := TRUE]
```
After running the above command, run `dat` in your terminal to see what happened. A new column `isEven` should exist, with the value `TRUE` only for rows where `col1` contains an even value. All other columns are automatically filled with `NA`.

How would you change the `isEven` column to contain `FALSE` values in place of the current `NA`?

<details><summary>Hint</summary>
 
The following filter should only point to to rows where `col1` is odd:
```R
dat[col1 %% 2 != 0]
```
To this command, you can add the necessary code to assign the colum `isEven` the value `FALSE`, similar to how we assigned `TRUE` before.
</details>

<details><summary>Answer</summary>
 
The filter should only refer to rows where `col1` is odd.
```R
dat[col1 %% 2 != 0, isEven := FALSE]
```
</details>


Hint
```R
dat[col1 %% 2 != 0]
dat[is.na(isEven)]
```

Using either of the above commands, add the necessary 
We can fill in the other rows with `FALSE` in a few different ways:


---

## Removing columns
in `data.table` you can remove columns by assigning them to `NULL`
```R
dat[, col4 := NULL]     # remove one column
```

To remove multiple columns at one time
```R
dat[, c('col2', 'col3') := NULL]     # remove one column

```

---

## Rounding
floor ceiling

---

## Functions
cut
tstrsplit
rle
rleid

---

## Binning
cut