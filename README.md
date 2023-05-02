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


# Installation
# Loading
# Basics of data.table

    auto head/tail
    no row names, ever. If you want names, make it a column
    fast subset
    memory efficient, in-place changes (data.frame makes copy every time you change it)



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

