# Data wrangling in R with `data.table`


## Part 1
### [Introduction](00_intro/README.md)
* [Installation and Setup](00_intro/A.md)
* [Why `data.table` ?](00_intro/B.md)
* [Read the docs!](00_intro/C.md)

### [Importing Text](01_importing_data/README.md)
* [fread](01_importing_data/A.md)
* [excel](01_importing_data/B.md)
* [other files](01_importing_data/C.md)

### [Filtering data by row](02_filtering_data/README.md)
* [`data.table` notation in `i`](02_filtering_data/A.md)
* [filtering by conditions](02_filtering_data/B.md)
* [chaining filters](02_filtering_data/C.md)
* [useful filter functions](02_filtering_data/D.md)

### [Column operations](03_column_operations/README.md)
* [Organizing columns](03_column_operations/A.md)
* [Assigning new columns](03_column_operations/B.md)
* [Combining row and column operations](03_column_operations/C.md)
* [Useful functions across columns](03_column_operations/D.md)

### [Exporting data](04_exporting_data/README.md)
* [writing data tables to text](04_exporting_data/A.md)
* [writing vectors to text](04_exporting_data/B.md)
* [saving R objects to disk](04_exporting_data/C.md)

---

## Part 2

### [Merging data](05_merging_data/README.md)
* [inner joins](05_merging_data/A.md)
* [outer joins](05_merging_data/B.md)

### [Transforming between long and wide](06_transforming_long_and_wide/README.md)
* [melt](06_transforming_long_and_wide/A.md)
* [dcast](06_transforming_long_and_wide/B.md)

### [Aggregation by groups](07_aggregation_by_groups/README.md)
* [Basic aggregation](07_aggregation_by_groups/A.md)
* [Advanced aggregation](07_aggregation_by_groups/B.md)

### [Iterating with Foreach](08_iterating_with_foreach/README.md)
* [the `%do%` operator](08_iterating_with_foreach/A.md)
* [combining data from multiple files](08_iterating_with_foreach/B.md)
* [iterating over data subsets](08_iterating_with_foreach/C.md)
* [sliding window analyses](08_iterating_with_foreach/D.md)

### [Putting it together](09_putting_it_together/README.md)



## Adding columns by operating across columns
    # dat[, 'newcol' := (operation) ]
    # No row filter, apply to all rows
    # With row filter, NAs otherwise
    # Ifelse
    # dat[, 'newcol' := ifelse(V1==3, TRUE, FALSE)]
        # Chaining ifelse
        # dat[, 'newcol' := ifelse(V1==3, 'three', 
                            ifelse(V1==4, 'four',
                            ifelse(V1==5, 'five',
                            other)]


# pick random sample
# pick random rows
# convert to '.|.'
# FIRST exclude samples with 25% or more missing data, THEN exclude sites with 10% or more missing data
# convert '.|.' to NA
# create column 



# Day 2

## .SD and Apply

grep = indices
grepl = grep logical

## Apply functions

## Foreach
    # Reading multiple files
    # Sliding window
    #

## Renaming with gsub
## Pattern matching with grepl
## Building test data sets

## Combos with CJ

`fwrite`


library(openxlsx)


openxlsx::read.xlsx(xlsxfilename, sheetName_OR_sheetIndex)

touch 00_getting_started/README.md
touch 01_importing_data/README.md
touch 02_filtering_data/README.md
touch 03_reorganize_columns/README.md
touch 04_column_operations/README.md
touch 05_merging/README.md
touch 06_exporting/README.md
touch 07_transform_to_long/README.md
touch 08_transform_to_wide/README.md
touch 09_iteration_with_foreach/README.md
touch 10_aggregation/README.md
touch 11_putting_it_together/README.md

