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
00_intro
    README.md
    A.md Installation and loading
    B.md Why data.table
01_importing_text
    README.md
    A.md fread
    B.md excel
    C.md importing other files
02_filtering_data
    README.md
    A.md working in i
    B.md filter by condition
    C.md chaining
    D.md useful filter functions
        %in%
        %between%
        %like%
03_organizing_columns
    README.md
    A.md changing column names
    B.md selecting a subset of columns
    C.md changing column order
    D.md removing columns
04_column_operations
    README.md
    A.md math operations
    B.md removing columns
    C.md combined operations
    D.md useful functions
05_exporting_data
    README.md
    A.md tables to text incl. compressed
    B.md vectors to text
    C.md writeRDS R objects to RDS
    D.md save R objects to Rdata
06_merging_data
    README.md
    A.md inner join
    B.md outer joins
07_transforming_long_and_wide
    README.md
    A.md melt
    B.md dcast
08_aggregation_by_groups
    README.md
    A.md operating in i,j and by
09_iterating_with_foreach
    README.md
    A.md %do%
    B.md combining files
    C.md iterating over subsets
    D.md sliding window analysis
10_putting_it_together
    README.md
    A.md import multi chromosomes with foreach,
    B.md exclude anything that isn't a SNP,
    C.md melt to long,
    D.md convert genotype to alt allele dosage,
    E.md aggregate BY to calculate summary stats,
    F.md convert . to NA
    G.md exclude samples with missingness
    H.md exclude rows with missingness
    I.md dcast back to wide
    J.md output data

## Part 1
[Introduction](00_intro/README.md)
* [Installation and Loading](00_intro/A.md)
* [Why `data.table` ?](00_intro/B.md)

[Importing Text](01_importing_data/README.md)
* [fread](01_importing_data/A.md)
* [excel](01_importing_data/B.md)
* [other files](01_importing_data/C.md)

[Filtering data by row](02_filtering_data/README.md)
* [working in `i`](02_filtering_data/A.md)
* [filtering by conditions](02_filtering_data/B.md)
* [chaining filters](02_filtering_data/C.md)
* [useful filter functions](02_filtering_data/D.md)

[Organizing columns](03_organizing_columns/README.md)
* [changing column names](03_organizing_columns/A.md)
* [subsetting columns](03_organizing_columns/B.md)
* [changing column order](03_organizing_columns/C.md)
* [removing columns](03_organizing_columns/D.md)

[Column operations](04_column_operations/README.md)
* [column types](04_column_operations/A.md)
* [math operations](04_column_operations/B.md)
* [combining row and column operations](04_column_operations/C.md)
* [useful functions across columns](04_column_operations/D.md)

[Exporting data](05_exporting_data/README.md)
* [writing data tables to text](05_exporting_data/A.md)
* [writing vectors to text](05_exporting_data/B.md)
* [saving R objects to disk](05_exporting_data/C.md)

---

## Part 2
[Merging data](06_merging_data/README.md)
* [inner joins](06_merging_data/A.md)
* [outer joins](06_merging_data/B.md)

[Transforming between long and wide](07_transforming_long_and_wide/README.md)
* [melt](07_transforming_long_and_wide/A.md)
* [dcast](07_transforming_long_and_wide/B.md)

[Aggregation by groups](08_aggregation_by_groups/README.md)
* [Basic aggregation](08_aggregation_by_groups/A.md)
* [Advanced aggregation](08_aggregation_by_groups/B.md)

[Iterating with Foreach](09_iterating_with_foreach/README.md)
* [the `%do%` operator](09_iterating_with_foreach/A.md)
* [combining data from multiple files](09_iterating_with_foreach/B.md)
* [iterating over data subsets](09_iterating_with_foreach/C.md)
* [sliding window analyses](09_iterating_with_foreach/D.md)

[Putting it together](10_putting_it_together/README.md)
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





# Installation
# Loading
# Basics of data.table

00 Intro to data.table
    09A Installation and loading
    09B Why data.table
        auto head/tail
        no row names, ever. If you want names, make it a column
        fast subset
        memory efficient, in-place changes (data.frame makes copy every time you change it)
01 importing text
    010 intro
    01A fread
    01B excel
    01C importing other files
02 filtering data
    020 intro
    02A working in i
    02B filter by condition
    02C chaining
    03D useful filter functions

03 organizing columns
    030 intro
    03A changing column names
    03B selecting a subset of columns
    03C changing column order
    04D removing columns
04 column operations
    040 intro
    04A math operations
    04B removing columns
    04C combined operations
    04D useful functions
05 exporting data
    050 intro
    05A tables to text incl. compressed
    05B vectors to text
    05C writeRDS R objects to RDS
    05D save R objects to Rdata


06 merging data
    060 intro
    06A inner join
    06B outer joins
07 transforming long and wide
    070 intro
    07A melt
    07B dcast
08 aggregation
    080 intro
    08A operating in i,j and by
09 iterating with foreach
    090 intro
    09A %do%
    09B combining files
    09C iterating over subsets
    09D sliding window analysis
10 putting it together
    100 intro
    10A import multi chromosomes with foreach,
    10B exclude anything that isn't a SNP,
    10C melt to long,
    10D convert genotype to alt allele dosage,
    10E aggregate BY to calculate summary stats,
    10F convert . to NA
    10G exclude samples with missingness
    10H exclude rows with missingness
    10I dcast back to wide
    10J output data


# Day 1

## Importing data

`fread`
    # works from web
    # works with commands
    # works with gzipped files
    # auto-detects csv
    # will NOT work for xlsx

## Looking at the docs
Doc pages for 
[base `R`](https://stat.ethz.ch/R-manual/R-devel/library/base/html/00Index.html) and 
[`data.table`](https://www.rdocumentation.org/packages/data.table/versions/1.14.8)

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

