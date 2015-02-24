# rio: A Swiss-army knife for data I/O #

The aim of **rio** is to make data file I/O in R as easy as possible by implementing three simple functions in Swiss-army knife style:

 - `export` and `import` provide a painless data I/O experience by automatically choosing the appropriate data read or write function based on file extension
 - `convert` wraps `import` and `export` to allow the user to easily convert between file formats (thus providing a FOSS replacement for programs like [Stat/Transfer](https://www.stattransfer.com/) or [Sledgehammer](http://www.openmetadata.org/site/?page_id=1089))

The core advantage of **rio** is that it makes assumptions that the user is probably willing to make. Specifically, **rio** uses the file extension of a file name to determine what kind of file it is. This is the same logic used by Windows OS, for example, in determining what application is associated with a given file type. By taking away the need to manually match a file type (which a beginner may not recognize) to a particular import or export function, **rio** allows almost all common data formats to be read with the same function.
 
The package also wraps a variety of faster, more stream-lined I/O packages than those provided by base R or the **foreign** package. Namely, the package uses [**haven**](https://github.com/hadley/haven) for reading and writing SAS, Stata, and SPSS files and [**fastread**](https://github.com/hadley/fastread) for reading simple text-delimited and fixed-width file formats.

## Supported file formats ##

**rio** supports a variety of different file formats for import and export.

*Import*

* txt (tab-seperated)
* tsv
* csv
* rds
* Rdata
* json
* dta (Stata)
* sav (SPSS)
* por (SPSS portable)
* sas7bdat (SAS)
* xpt (SAS XPORT)
* mtp (Minitab)
* rec (Epiinfo)
* syd (Systat)
* dif (Data Interchange Format)
* dbf ("XBASE" database files)
* xlsx (Excel)
* arff (Weka Attribute-Relation File Format)

**Export**

* txt (tab-seperated)
* tsv
* csv
* rds
* Rdata
* json
* dbf ("XBASE" database files)
* dta (Stata)
* sav (SPSS)
* xlsx (Excel)
* arff (Weka Attribute-Relation File Format)
* clipboard (on Mac and Windows only; as tab-separated data)


## Package Installation ##

The package is available on [CRAN](http://cran.r-project.org/web/packages/rio/) and can be installed directly in R using:

```R
install.packages("rio")
```

The latest development version on GitHub can be installed using **devtools**:

```R
if(!require("devtools")){
    install.packages("devtools")
    library("devtools")
}
install_github("leeper/rio")
```

## Examples ##

Because **rio** is meant to streamline data I/O, the package is extremely easy to use. Here are some examples of reading, writing, and converting data files.

### Export ###


```r
library("rio")

export(iris, "iris.csv")
export(iris, "iris.rds")
export(iris, "iris.dta")
```

### Import ###


```r
library("rio")

x <- import("iris.csv")
y <- import("iris.rds")
z <- import("iris.dta")

# confirm identical
identical(iris, x)
```

```
## [1] TRUE
```

```r
identical(x, y)
```

```
## [1] TRUE
```

```r
identical(y, z)
```

```
## [1] FALSE
```

### Convert ###


```r
library("rio")

convert("iris.csv", "iris.dta")
```

