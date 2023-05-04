# Combining multiple files with `foreach`

It's often necessary to import data from multiple files for a single analysis. We can make quick
work of that task using `foreach` to iterate over file names.

```R
# Ensure both libraries are loaded
library(foreach)
library(data.table)

files_to_import <- c('Experiment_batch_2_05022023.tsv', 'Experiment_batch_1_05012023.tsv')

```R
dat <- foreach(file=files_to_import) %do% { fread(file) }
```

Looking at the results, `dat` is a list of `data.table` objects. We can modify our command to bind
the results together automatically with `.combine='rbind'`

```R
dat <- foreach(file=files_to_import, .combine='rbind') %do% { fread(file) }
```

But it seems we have a problem. We don't know which rows came from which file. We can edit our command
to add a new column for each iteration of the loop:

```R
# Same as before, but restructured to be simple to read
dat <- foreach(file=files_to_import, .combine='rbind') %do% { 
    fread(file) 
}

# create a temporary data.table, add the filename as a new column, and return it
dat_with_ids <- foreach(file=files_to_import, .combine='rbind') %do% { 
    tmp <- fread(file) 
    tmp[, 'filename' := file]
    return(tmp)
}
```

## Automating multiple file import

There are actually more than just two batch files! We can check our directory with `list.files` to
search for files matching a pattern. In our case, all the desired files begin with `Experiment_` and
end with `.tsv`.

In the following command, `.*` acts as a wildcard.
```R
list.files(pattern='Experiment_.*.tsv')
```

This can be particularly useful when you have hundreds or thousands of files. Let's modify our code
to automatically import all of these files and add the filename as a column:

```R
files_to_import <- list.files(pattern='Experiment_.*.tsv')

dat_with_ids <- foreach(file=files_to_import, .combine='rbind') %do% { 
    tmp <- fread(file) 
    tmp[, 'filename' := file]
    return(tmp)
}
```

This only scratches the surface of what you can accomplish with `foreach`. There are near-infinite
uses for this function, with the only requirement being it needs to return a `data.table` for
every iteration.


## On your own: splitting strings with `tstrsplit`

While the `filename` column does differentiate the four batches, it's less intuitive than simply
having a column with `1` `2` `3` or `4`. We can extract substrings to accomplish the task.

As a demonstration how string splitting works with the usual `strsplit` function:
```R
strsplit('Experiment_batch_1_05012023.tsv', split='_')
```

A small modification is using the transposed version `tstrsplit` to assign the column `batch` the
third value in the split string for *every* row:
```R
dat_with_ids[, 'batch' := tstrsplit(filename, split='_')[3]]
```

Extracting the batch was useful, but we could also extract the date from the filename. We would
need to split the string differently. Luckily, we can include multiple patterns in `split=` by
separating them by `|`. The only problem is that if we try to split on the period, it acts as
a wild card like before. In order to split on a *literal* period, and not a wildcard, we need to
prepend it with backslashes, i.e. `\\.`

```R
dat_with_ids[, 'date' := tstrsplit(filename, split='_|\\.')[4]]
```

---

[PREV](README.md) | [HOME](/README.md) | [NEXT](/09_putting_it_together/README.md)

<details><summary>How sample data was generated</summary>

```R
set.seed(1)
cell_lines <- c('WT', 'MUTA', 'MUTB', 'MUTC')
batches <- c('batch_1_05012023', 'batch_2_05022023', 'batch_3_05032023', 'batch_4_05042023')
symbols <- paste0('GENE_', LETTERS)
for(i in batches) {
    tmp <- CJ(cell_lines, symbols)
    tmp[, count := abs(floor(jitter(rpois(nrow(tmp), lambda=1))**8)) ]
    tmp <- dcast(tmp, symbols~cell_lines)
    setcolorder(tmp, c('symbols','WT','MUTA','MUTB','MUTC'))
    setnames(tmp, 'symbols', 'SYMBOL')
    fwrite(tmp, file=paste0('Experiment_', i, '.tsv'), sep='\t')
}
```

</details>