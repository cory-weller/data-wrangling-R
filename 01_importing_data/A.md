# Importing data with `fread`

`fread`, as in **f**ast **read** is `data.table`'s smarter, more efficient, more flexible implementation of the base R function `read.csv`.

automatically tries to detect delimiter

*delimiter*: the character usd to mark separate values in a sequence for machine-readability. Examples include comma for `.csv` or tab for `.tsv`. Sometimes a table might include multiple optional data fields in a single column separated by semicolon. 

We may not always be aware of it, but separate lines in a file are delimited by the `newline` character `'\n'` which appears as a new line on our screens.