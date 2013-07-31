---
title: BumpCharts with R and Rickshaw
framework: basedemo
highlighter: prettify
hitheme: twitter-bootstrap
mode: selfcontained
assets:
  css: 'http://fonts.googleapis.com/css?family=Open+Sans'
--- &nav

- [About](about)
- [rCharts](http://rcharts.io)
- .download [Download](item3)

--- &header

## BaseDemo 

BaseDemo is just a basic template that can be used for creating demos for your development projects. It also works great for GitHub Pages. This is an example of what you could do with this template and some content types.





<style>
  iframe {width: 100%; height: 350px;}
  /*
  p{font-family: "Open Sans"}
  pre, code{font-family: "Monaco";}
  code{color: #D14}
  */
</style>
<script>var myScriptSrc = "libraries/frameworks/basedemo/css/";</script>

--- &demo

## Get Data

Our first step is to read the data from the URL using `read.csv`, and extract the columns of interest. `FTR` stands for __Full Time Result__ and is coded as `H`, `A` or `D`, depending on whether the home team or the away team won, or the game ended in a draw. We rename the columns for easier usage, and also format the `date` appropriately.


*** .active #1

## Code


```r
dataURL <- 'http://www.football-data.co.uk/mmz4281/1213/E0.csv'
df <- read.csv(dataURL, stringsAsFactors = F)
df <- df[, c("Date", "HomeTeam", "AwayTeam", "FTR")]
df <- rename(df, c(Date = "date", HomeTeam = "H", AwayTeam = "A"))
df$date <- as.Date(df$date, format = "%d/%m/%y")
head(df)
```


*** #2

## Result


```
        date         H          A FTR
1 2012-08-18   Arsenal Sunderland   D
2 2012-08-18    Fulham    Norwich   H
3 2012-08-18 Newcastle  Tottenham   H
4 2012-08-18       QPR    Swansea   A
5 2012-08-18   Reading      Stoke   D
6 2012-08-18 West Brom  Liverpool   H
```


--- &demo

## Process Data

Our next step is to `melt` the data into its long-form, and add a column for `points` collected by the team. The first two expressions below, `melt` the data and `arrange` it in ascending order by `date`. To calculate the `points` collected by the team, we employ a simple math trick instead of writing a nested `if-then-else` statement. The idea is that the team gets 3 points on a win ( `loc` equals `FTR`), 1 point on a draw (`FTR` equals `D`) and zero otherwise.

*** .active #b1

## Code


```r
dfm <- melt(df, measure.vars = c("H", "A"), 
  variable.name = "loc", value.name = 'team')
dfm <- arrange(dfm, date)
dfm <- mutate(dfm, 
  loc = as.character(loc), 
  points = 3*(loc == FTR) + 1*(FTR == 'D')
)
head(dfm)
```


*** #b2

## Result


```
        date FTR loc      team points
1 2012-08-18   D   H   Arsenal      1
2 2012-08-18   H   H    Fulham      3
3 2012-08-18   H   H Newcastle      3
4 2012-08-18   A   H       QPR      0
5 2012-08-18   D   H   Reading      1
6 2012-08-18   H   H West Brom      3
```








