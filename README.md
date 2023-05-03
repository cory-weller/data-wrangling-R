# Data wrangling in R with `data.table`

[Getting Started](00_getting_started/README.md)

# Setup


1. Download this repository. On linux, run:
    ```
    git clone https://github.com/cory-weller/intro-R-datatable
    ```

1. Enter this repository

1. thing

1. thing


## Topics


## Part 1
[00 Introduction](00_intro/README.md)
* [Installation and Setup](00_intro/A.md)
* [Why `data.table` ?](00_intro/B.md)
* [Read the docs!](00_intro/C.md)

[01 Importing Text](01_importing_data/README.md)
* [fread](01_importing_data/A.md)
* [excel](01_importing_data/B.md)
* [other files](01_importing_data/C.md)

[02 Filtering data by row](02_filtering_data/README.md)
* [`data.table` notation in `i`](02_filtering_data/A.md)
* [filtering by conditions](02_filtering_data/B.md)
* [chaining filters](02_filtering_data/C.md)
* [useful filter functions](02_filtering_data/D.md)

[03 Organizing columns](03_organizing_columns/README.md)
* [changing column names](03_organizing_columns/A.md)
* [subsetting columns](03_organizing_columns/B.md)
* [changing column order](03_organizing_columns/C.md)
* [removing columns](03_organizing_columns/D.md)

[04 Column operations](04_column_operations/README.md)
* [column types](04_column_operations/A.md)
* [math operations](04_column_operations/B.md)
* [combining row and column operations](04_column_operations/C.md)
* [useful functions across columns](04_column_operations/D.md)

[05 Exporting data](05_exporting_data/README.md)
* [writing data tables to text](05_exporting_data/A.md)
* [writing vectors to text](05_exporting_data/B.md)
* [saving R objects to disk](05_exporting_data/C.md)

---

## Part 2
[06 Merging data](06_merging_data/README.md)
* [inner joins](06_merging_data/A.md)
* [outer joins](06_merging_data/B.md)

[07 Transforming between long and wide](07_transforming_long_and_wide/README.md)
* [melt](07_transforming_long_and_wide/A.md)
* [dcast](07_transforming_long_and_wide/B.md)

[08 Aggregation by groups](08_aggregation_by_groups/README.md)
* [Basic aggregation](08_aggregation_by_groups/A.md)
* [Advanced aggregation](08_aggregation_by_groups/B.md)

[09 Iterating with Foreach](09_iterating_with_foreach/README.md)
* [the `%do%` operator](09_iterating_with_foreach/A.md)
* [combining data from multiple files](09_iterating_with_foreach/B.md)
* [iterating over data subsets](09_iterating_with_foreach/C.md)
* [sliding window analyses](09_iterating_with_foreach/D.md)

[10 Putting it together](10_putting_it_together/README.md)
* [part a](10_putting_it_together/A.md)
* [part b](10_putting_it_together/B.md)
* [part c](10_putting_it_together/C.md)
* [part d](10_putting_it_together/D.md)
* [part e](10_putting_it_together/E.md)
* [part f](10_putting_it_together/F.md)
* [part g](10_putting_it_together/G.md)
* [part h](10_putting_it_together/H.md)
* [part i](10_putting_it_together/I.md)
* [part j](10_putting_it_together/J.md)






## Filtering (subsetting or splitting) data by row
vector * boolean (lengths match)
vector * indices

# Example VCF file
# Example GTF
# Example bed


## Filtering (subsetting or splitting) data by column
dat[REF %in% c('A','T','C','G')]
dat[ALT %in% c('A','T','C','G')]
dat[REF %in% c('A','T','C','G') & ALT %in% c('A','T','C','G')]

## Paste, paste0

# Only include SNPs
exclude sample because they dropped out of a study.

dat[sort(sample(1:8548, size=238)), FILTER := 'FAIL']


dat[sort(sample(1:8548, size=238)), FILTER := 'FAIL']

## Renaming, reorganizing, removing columns


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

dat <- fread('short.vcf')
for(i in 1:50) {
    n_missing <- sample(1:1500, size=1)
    missing_rows <- sort(sample(1:8548, size=n_missing, replace=F))
    col_id <- sample(10:35, size=1)
    dat[missing_rows, eval(col_id) := '.|.']
}
colnames(dat)[10:35]

sample_names <- colnames(dat)[10:35]
 melt(dat, measure.vars=sample_names)

dat.long <- melt(dat, measure.vars=sample_names, value.name='genotype', variable.name='sample')





## Summarize missingness by position
## Summarize missingness by sample
## calculate minor allele frequency

fwrite(dat, file='missing.vcf', quote=F, row.names=F, col.names=T, sep='\t')

ncol
nrow
is.na
runif
rand

## tstrsplit: splitting values in a column into one or more new columns
    # 
    # reminder on strsplit
    # using tstrsplit
## Sorting, Keys

## Binning data
## Rank
## RLE & RLEID
## Shift
## Transforming data between long and wide
    # melt
    # dcast

## Merging

## Exporting data


## any, all


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

