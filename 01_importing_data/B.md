# Other R data structures

Sometimes you want to load (or save) `R` objects exactly as they appear in your current session, instead of outputting to text.
This can be done by writing a binary representation of your object (or objects) to the disk. A single R object can be saved with `saveRDS`:

```R
saveRDS(file_1, file='5000_lines.rds')

# later...
varname1 <- readRDS('5000_lines.rds')
```
The `.rds` file is a binary compressed representation of the object, meaning it cannot be read as text--it needs to be loaded by `R` to convert back into its original representation.

Note that `readRDS` doesn't know the original name of the object, so you need to re-assign it to some variable name. 

Multiple objects can be written to the disk with `save`, with `save.image` being a special case that saves  all objects in your session to be restored later.

```R
save.image('mysession.Rdata')

# later...
load('mysession.Rdata')
```
The original variable names stored in the `.Rdata` file will automatically be loaded along with their contents. Note that any packages will need to be loaded again if it's a new R session!

---

# A note on excel data

Excel data is not plain text, so it won't work with `fread`. Your options are:
1. open the file in excel and save the desired sheet as plain text
2. use a package designed to interface with `.xlsx` files.

There are multiple packages that can do this, including `openxlsx`. We won't touch on this subject any more, but here's an example for reading in a sheet from an excel file. See the docs for more details.

```R
library(openxlsx)       # once openxlsx is installed
mydata <- openxlsx::read.xlsx(filename, sheetName_OR_sheetIndex)
```

[PREV](A.md) | [HOME](/README.md) | [NEXT](/02_filtering_data/README.md)
