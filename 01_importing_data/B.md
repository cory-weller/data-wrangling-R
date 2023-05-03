# A note on excel data

Excel data is not plain text, so it won't work with `fread`. Your options are:
1. open the file in excel and save the desired sheet as plain text
2. use a package designed to interface with `.xlsx` files.

There are multiple packages that can do this, including `openxlsx`. We won't touch on this subject any more, but here's an example for reading in a sheet from an excel file. See the docs for more details.

```R
library(openxlsx)       # once openxlsx is installed
mydata <- openxlsx::read.xlsx(filename, sheetName_OR_sheetIndex)
```

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
