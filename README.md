R-Cheat-Sheet
================
Clay Rowland
11 December, 2018

This cheat sheet was developed for a course project in MGSC 790 Data Resource Management, a Business Analytics elective in the [PMBA](https://sc.edu/study/colleges_schools/moore/academic_programs/mba_programs/professional_mba/) program of the [Darla Moore School of Business](https://sc.edu/study/colleges_schools/moore/index.php) at the University of South Carolina.

It is intended as a quick reference of data structures, functions, and packages for the R language. Please see the official [Rdocumentation](https://www.rdocumentation.org/) for a comprehensive reference.

This is not inclusive of all the R packages available. There are over 13,000 [packages](https://cran.r-project.org/web/packages/) that have been developed to supplement the R language. Below are a handful that were covered during the [Data Scientist With R track](https://www.datacamp.com/tracks/data-scientist-with-r) on [Data Camp](https://datacamp.com).

<br />

#### Table of Contents

###### A little bit of Base R

  [Data structures](#dataStructures)

  [Base functions](#functions)

###### Data manipulation & visualization

  [dplyr](#dplyr)

  [ggplot2](#ggplot2)

###### A handful of R packages

  [httr](#httr)

  [jsonlite](#jsonlite)

  [gdata](#gdata)

  [readr](#readr)

  [readxl](#readxl)

  [DBI](#dbi)

  [haven](#haven)

  [RMarkdown](#rMarkdown)

<br />

#### A little bit of Base R

##### <a name="dataStructures"></a>Data structures

A [vector](http://adv-r.had.co.nz/Data-structures.html#vectors) is an array of homogenous datatypes.

A list is similar to a vector but can contain heterogeneous datatypes.

A [matrix](http://adv-r.had.co.nz/Data-structures.html#matrices-and-arrays) is a two-dimensional vector of homogenous datatypes.

An array is a vector with one or more dimensions. An array with one dimension is similar to a vector. An array with two dimensions is similar to a matrix. An array with three or more dimensions is an n-dimensional array.

A [data frame](http://adv-r.had.co.nz/Data-structures.html#data-frames) is similar to a table in a database. Each column in the data frame holds a value of the same type, and the columns can (and should) be named.

A [factor](https://www.stat.berkeley.edu/~s133/factors.html) is an enumerated type representing a discrete number of categorical values.

##### <a name="functions"></a>Base functions

[c](https://www.rdocumentation.org/packages/base/topics/c)

``` r
# combine Values into a Vector or List
c("China", "India", "United States of America")
```

    ## [1] "China"                    "India"                   
    ## [3] "United States of America"

[matrix](https://www.rdocumentation.org/packages/base/topics/matrix)

``` r
# creates a matrix from the given set of values.
matrix(1:9, nrow=3)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    4    7
    ## [2,]    2    5    8
    ## [3,]    3    6    9

[data.frame](https://www.rdocumentation.org/packages/base/topics/data.frame)

``` r
# creates data frames
worldPop <- data.frame(country, population)
worldPop
```

    ##                    country population
    ## 1                    China 1409517397
    ## 2                    India 1339180127
    ## 3 United States of America  324459463

[subset](https://www.rdocumentation.org/packages/base/topics/subset)

``` r
# return subsets of vectors, matrices or data frames which meet conditions.
subset(worldPop, country=="China")
```

    ##   country population
    ## 1   China 1409517397

[factor](https://www.rdocumentation.org/packages/base/topics/factor)

``` r
# encode a vector as a factor
factor(c("A", "B", "B",  "C", "C", "C"))
```

    ## [1] A B B C C C
    ## Levels: A B C

<!--

[gl](https://www.rdocumentation.org/packages/base/topics/gl)

```r
# generate factor levels
gl(3,1)
```

```
## [1] 1 2 3
## Levels: 1 2 3
```

[levels](https://www.rdocumentation.org/packages/base/topics/levels) 

```r
# provides access to the levels attribute of a variable
lowMedHigh <- gl(3, 1)
levels(lowMedHigh) <- c("low", "medium", "high")
lowMedHigh
```

```
## [1] low    medium high  
## Levels: low medium high
```
-->
[paste](https://www.rdocumentation.org/packages/base/topics/paste)

``` r
# concatenate vectors
paste("this", "is", "a", "concatenation")
```

    ## [1] "this is a concatenation"

[lapply](https://www.rdocumentation.org/packages/base/topics/lapply)

``` r
# apply a function over a list or vector and return a list
lapply(c("a", "b", "c"), toupper)
```

    ## [[1]]
    ## [1] "A"
    ## 
    ## [[2]]
    ## [1] "B"
    ## 
    ## [[3]]
    ## [1] "C"

<!--
[sapply](https://www.rdocumentation.org/packages/base/topics/sapply) 

```r
# apply a function over a list or vector and return a vector, matrix, or array
sapply(c("a", "b", "c"), toupper)
```

```
##   a   b   c 
## "A" "B" "C"
```

[vapply](https://www.rdocumentation.org/packages/base/topics/vapply) 

```r
# apply a function over a list or vector and return a vector, matrix, or array of the specified type
vapply(c("a", "b", "c"), toupper, character(1))
```

```
##   a   b   c 
## "A" "B" "C"
```
-->
[identical](https://www.rdocumentation.org/packages/base/topics/identical)

``` r
x <- 1000
y <- 1000

# evaluate whether objects are equal
identical(x, y)
```

    ## [1] TRUE

[Sys.Date](https://www.rdocumentation.org/packages/base/topics/Sys.Date)

``` r
# return the current date
Sys.Date()
```

    ## [1] "2018-12-11"

[Sys.time](https://www.rdocumentation.org/packages/base/topics/Sys.time)

``` r
# return the current date and time
Sys.time()
```

    ## [1] "2018-12-11 09:12:58 EST"

[format](https://www.rdocumentation.org/packages/base/topics/format)

``` r
# format an object for printing
format(Sys.Date(), "%B %d %Y")
```

    ## [1] "December 11 2018"

[summary](https://www.rdocumentation.org/packages/base/topics/summary)

``` r
# produce result summaries of various model fitting functions
summary(mtcars$mpg)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   10.40   15.43   19.20   20.09   22.80   33.90

<br />

#### Data manipulation & visualization

<br />

<a name="dplyr"></a>[dplyr](http://dplyr.tidyverse.org/)

``` r
library(dplyr, warn.conflicts = FALSE)
```

dplyr provides a library for data manipulation, including the pipe operator `%>%` which allows for the chaining of functions

``` r
# filtering and ordering
starwars %>%
  filter(homeworld=="Naboo") %>% # subset the data based on criteria
  mutate(taxa = ifelse(species == "Droid", "Machine", "Biological")) %>% # add a column to the data
  select(taxa, species, name) %>% # limit the columns to those provided
  na.omit() %>% # exclude records with NA as a value in a column
  arrange(taxa, species, name) # order the result
```

    ## # A tibble: 9 x 3
    ##   taxa       species name         
    ##   <chr>      <chr>   <chr>        
    ## 1 Biological Gungan  Jar Jar Binks
    ## 2 Biological Gungan  Roos Tarpals 
    ## 3 Biological Gungan  Rugor Nass   
    ## 4 Biological Human   Cordé        
    ## 5 Biological Human   Dormé        
    ## 6 Biological Human   Gregar Typho 
    ## 7 Biological Human   Padmé Amidala
    ## 8 Biological Human   Palpatine    
    ## 9 Machine    Droid   R2-D2

``` r
# aggregation
starwars %>%
  filter(homeworld=="Naboo") %>%
  group_by(species) %>% # aggregate by the columns provided
  tally # count the results
```

    ## # A tibble: 4 x 2
    ##   species     n
    ##   <chr>   <int>
    ## 1 Droid       1
    ## 2 Gungan      3
    ## 3 Human       5
    ## 4 <NA>        2

##### <a name="ggplot2"></a>[ggplot2](http://ggplot2.tidyverse.org/)

``` r
library(ggplot2)
library(gapminder) # load gapminder dataset
```

ggplot2 provides a library for visualizing data

``` r
# scatter plot
gapminder %>% filter(year==2007) %>%
ggplot(aes(x=gdpPercap, y=lifeExp, color=continent, size=pop)) +
  geom_point() +  # produce a scatter plot
  scale_x_log10() + # use a logarithmic scale for the x axis
  theme_minimal() + # minimize the lines/color in the chart
  ggtitle("2007 Life Expectancy by GDP Per Capita") # provide a title
```

![](https://raw.githubusercontent.com/rowlanch/my-R-cheat-sheet/master/README_files/figure-markdown/unnamed-chunk-21-1.png)

``` r
# bar plot
gapminder %>% filter(year==2007) %>%
ggplot(aes(x=continent, y=gdpPercap)) +
  geom_bar(stat="identity", fill="steelblue") + # produce a bar graph
  expand_limits(y=0) + # set the y-axis to start at 0
  theme_minimal() +
  ggtitle("2007 GDP Per Capita by Continent")
```

![](https://raw.githubusercontent.com/rowlanch/my-R-cheat-sheet/master/README_files/figure-markdown/unnamed-chunk-21-2.png)

``` r
# line plot
gapminder %>% filter(country=="China") %>%
ggplot(aes(x=year, y=gdpPercap, color=country)) +
  geom_line(stat="identity", color="blue") + # produce a line graph
  expand_limits(y=0) +
  theme_minimal() +
  ggtitle("GDP Per Capita by Year in China")
```

![](https://raw.githubusercontent.com/rowlanch/my-R-cheat-sheet/master/README_files/figure-markdown/unnamed-chunk-21-3.png)

#### A handful of R packages

| Package Name                                                                           | Purpose                                                            |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| <a name="httr"></a>[httr](https://www.rdocumentation.org/packages/httr)                | Working with HTTP resources                                        |
| <a name="jsonlite"></a>[jsonlite](https://www.rdocumentation.org/packages/jsonlite)    | Parsing and generating JSON                                        |
| <a name="gdata"></a>[gdata](https://www.rdocumentation.org/packages/gdata)             | Manipulating data                                                  |
| <a name="readr"></a>[readr](https://readr.tidyverse.org/)                              | Importing tabular data file formats                                |
| <a name="readxl"></a>[readxl](https://readxl.tidyverse.org/)                           | Reading Excel spreadsheets                                         |
| <a name="dbi"></a>[DBI](https://db.rstudio.com/dbi/)                                   | Database integration                                               |
| <a name="haven"></a>[haven](https://www.rdocumentation.org/packages/haven)             | Working with statistical software package (SAS, SPSS, Stata) files |
| <a name="lubridate"></a>[lubridate](https://www.rdocumentation.org/packages/lubridate) | Dealing with dates and times                                       |
| <a name="stringr"></a>[stringr](https://www.rdocumentation.org/packages/lubridate)     | Working with strings                                               |

<br />

<!--

##### <a name="httr"></a>[httr](https://www.rdocumentation.org/packages/httr)
httr provides a library for working with HTTP resources

```r
library(httr)
response <- GET("http://httpbin.org/uuid") # make an HTTP request using the GET verb
status_code(response) # get the HTTP status code of the response
```

```
## [1] 200
```

```r
content(response, "text", encoding = "UTF-8") # get the content of the response as text
```

```
## [1] "{\n  \"uuid\": \"e01add26-2983-400d-b16d-b97b4b4f9a3d\"\n}\n"
```

##### <a name="jsonlite"></a>[jsonlite](https://www.rdocumentation.org/packages/jsonlite)
jsonlite provides a library for parsing and generating JSON

```r
library(jsonlite)
response <- fromJSON("http://httpbin.org/json") # get an R object from a JSON string
response$slideshow$author
```

```
## [1] "Yours Truly"
```

```r
gapminder %>% filter(year==2007, country=="China") %>%
  toJSON() # produce a JSON string from an R object
```

```
## [{"country":"China","continent":"Asia","year":2007,"lifeExp":72.961,"pop":1318683096,"gdpPercap":4959.1149}]
```
-->
##### <a name="rMarkdown"></a>[R Markdown](https://rmarkdown.rstudio.com/)

R Markdown provides a library for generating documents (PDF, HTML, Markdown) that include R functions and output.

This cheat sheet was produced using R Markdown. The source code for producing it can be found on [Github](https://github.com/rowlanch/my-R-cheat-sheet).

<br />

### References

Data structure and function descriptions have been taken from the [RDocumentation](https://www.rdocumentation.org/) site.

<br />
