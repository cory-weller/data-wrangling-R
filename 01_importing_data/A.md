# Importing data with `fread`

`fread`, as in **f**ast **read** is `data.table`'s smarter, more efficient, more flexible implementation of the base R function `read.csv`.

It 'just works' most of the time, by
* automatically detecting the delimiter[^1]
* automatically detecting headers
* automatically uses multiple threads (faster loading)
* automatically decompresses compressed text files

```R
# Syntax examples (these files should  not exist)
file_1 <- fread('filename.txt')             # read in a standard file
file_2 <- fread('compressed_file.txt.gz')   # Automatic decompression
```

## Using `bash` commands within `fread`
You can specify a bash command within `fread` by specifying the argument `cmd=<bash command>`. This will execute the `bash` command on the system level and then automatically read in the output. 

*Note: this will not work if you are running `Rstudio` on a windows machine, because you don't have bash!

```R
# Syntax example (bigfile.txt does not exist)
random_100_lines <- fread(cmd='shuf -n 100 bigfile.txt')    # Read in 100 randomly ordered lines from bigfile.txt
```

---
## On your own

Reference the `fread` documentation to answer the following:

Say you're importing a `VCF` file and you don't care about any entries of `'.|.'` in the file and want to convert them to NA. How would you force `fread` to automatically convert them to NA while loading?

<details><summary>Answer</summary>
 
include `na.strings='.|.'`
 
</details>

---
Sometimes a `VCF` file has hundreds of metadata lines at the start of the file. These metadata lines always begin with `##`. The header row always begins with `#CHROM`. How do you format `fread` to ignore the metadata lines and begin reading at the header?

<details><summary>Answer</summary>
 
include `skip='#CHROM'`
 
</details>

---
You are reading a large table with 2000 columns, but you only need to read in columns 21-40. How do you read in this subset of data?

<details><summary>Answer</summary>
 
The `select` argument lets you specify which columns to keep. You would include `select=21:40` in your command. Alternatively, `drop` lets you specify columns to exclude, i.e. `drop=c(1:20, 41:2000)`

</details>



---

[PREV](README.md) | [HOME](/README.md) | [NEXT](B.md)


[^1]: *delimiter*: the character used to mark separate values in a sequence for machine-readability. Examples include comma for `.csv` or tab for `.tsv`. Sometimes a table might include multiple optional data fields in a single column separated by semicolon. We may not always be aware of it, but separate lines in a file are delimited by the `newline` character `'\n'` which appears as a new line on our screens.

