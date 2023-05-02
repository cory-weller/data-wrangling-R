# Exporting 

## Background
* vectors
* tables
* multi-dimensional objects

## Writing vectors to text file

`writeLines(con='filename.txt')` saves a vector. By default, items are separated by a newline, i.e. `sep='\n'`.
You can separate by other characters if desired by changing the value of `sep=`:

```
my_vector <- c(letters,LETTERS)
# Write my_vector to file, one item per line
writeLines(my_vector, con='my_vector.txt')

# Write my_vector as a single comma-separated line
writeLines(my_vector, con='comma_separated.txt', sep=',')
```

## Writing tables to text
The function `fwrite` is the workhorse of saving any table as text output such as tab-separated values (`.tsv`) or comma-separated values (`.csv`).

```
fwrite(dat, file='filename.txt', sep=',')   # Write as csv
fwrite(dat, file='filename.txt')            # Write as csv (equivalent)
fwrite(dat, file='filename.txt', sep='\t')  # Write as tsv
```

## Writing tables as compressed text
Compressed text (e.g. with `gzip`) can save a lot of disk space for larger files.
`fwrite` automatically detects the `.gz` extension in filenames and writes as compressed text.
```
fwrite(dat, file='filename.txt.gz', sep='\t')  # Write as gzipped tsv
```

## Saving (and loading) R objects as a file

`saveRDS()` can write an entire R object to the disk for later use. It's a compressed binary format (not readable as text)

`save()` can write individual objects to disk, to be imported with `load()`
A specific instance of `save()` is `save.image()` which writes the entire workspace to disk.

## Try
```
# Generate vector of 100 random decimals within range (0,1)
my_numbers <- runif(100)

# Try writing my_numbers with writeLines. What happens?
writeLines(my_numbers, con='my_numbers.txt')
```

<details><summary>Next</summary>

Because `writeLines` only accepts character vectors, it gives an error:
```R
Error in writeLines(my_numbers, con = "my_numbers.txt") : 
  can only write character objects
```

How might you get around this limitation to write `my_numbers` to a file?

 <details><summary>Next</summary>
 
 We first have to convert the numeric vector to character with `as.character`
 ```R
 writeLines(as.character(my_numbers), con='my_numbers.txt')
 ``` 
 
 </details>


</details>


