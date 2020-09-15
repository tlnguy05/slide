---
title       : DEVELOPING DATA PRODUCT
subtitle    : COURSE PROJECT - COVID19 USA DASHBOARD
author      : TUAN NGUYEN
job         : 
framework   : revealjs        
revealjs    : {theme:night}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---
<style>
.reveal h1 {
    font-size: 2em;
    // color: #0000b3;
    padding-bottom: 10px;
    font-family: 'Permanent Marker', Impact, sans-serif;
}

.reveal h2 {
    font-size: 1.2em;
    color: ##ffa500;
    padding-bottom: 10px;
    font-family: 'Permanent Marker', Impact, sans-serif;
}


.reveal p, .reveal em {
    padding-bottom: 10px;
    width: 960px;
    font-family: 'Open Sans', Verdana, sans-serif;
}

.reveal p {
    font-size: .75em;
}

.reveal small {
    width: 500px;
}

.reveal .slides {
    text-align: left;
}

.reveal .roll {
    vertical-align: text-bottom;
}

code {
    color: red;
}

.reveal pre code { 
     height: 250px;
}

.reveal .tab {
margin-left: 40px;
}

</style>
## <h1>Developing Data Products</h1>
<h2>Course Project: <a href="https://nguyenlehoangtuan.shinyapps.io/covid/">COVID-19 USA DASHBOARD</a></h2>

Student : TUAN NGUYEN
<p><center>
<em>&quot;Tracking Covid-19 Cases in the United States&quot;</em>
</center></p>

--- .class #id 

## THE PROJECT ASSIGNMENT

This project aims to build:  
<p align = "justify"; class = "tab">1. <a style="color:yellow;"><b>A shiny application</b></a> that has some forms of widget inputs, operations on the ui input in <b>sever.R</b>, reactive outputs displayed as a result of server calculations and support documentations.</p>
<p align = "justify"; class = "tab">2. <a style="color:yellow;"><b>A reproducible pitch presentation</b></a> that contains five slides with embedded R codes, prepared in either Slidify or Rstudio Repsenter and then pushed to github or Rpubs.</p>

<p > Links to the project's shiny application & documentations:
<p class = "tab"><a href="https://nguyenlehoangtuan.shinyapps.io/covid/">- Shiny application</a></p> 
<p class = "tab"><a href="https://github.com/tlnguy05/developing_data_product/tree/gh-pages/covid">- Documentations</a></p>   

--------------------------------------------------------------------------------
## THE COVID-19 DATA
<p align = "justify">The data are scraped directly from <a href="www.worldometers.info/coronavirus/country/us/">Worldometers</a>, making sure our Shiny application's data are always up-to-date.</p>
<em align = "justify">Note: When there are a lot of NAs in a specific column, it means the data for that column is being updated</em>

```r
library(rvest)
fileurl <- "https://www.worldometers.info/coronavirus/country/us/"
data <- fileurl %>% read_html() %>% 
        html_nodes(xpath = '//*[@id="usa_table_countries_today"]') %>%
        html_table(fill = TRUE)
data <- data[[1]]
covidUSA_temp <- data[,c(-1, -14, -15)]
str(covidUSA_temp)
```

```
'data.frame':	64 obs. of  12 variables:
 $ USAState        : chr  "USA Total" "California" "Texas" "Florida" ...
 $ TotalCases      : chr  "6,749,289" "765,779" "697,735" "665,730" ...
 $ NewCases        : logi  NA NA NA NA NA NA ...
 $ TotalDeaths     : chr  "199,000" "14,462" "14,582" "12,649" ...
 $ NewDeaths       : logi  NA NA NA NA NA NA ...
 $ TotalRecovered  : chr  "4,027,826" "378,323" "600,046" "154,588" ...
 $ ActiveCases     : chr  "2,522,463" "372,994" "83,107" "498,493" ...
 $ Tot Cases/1M pop: chr  "20,390" "19,381" "24,063" "30,996" ...
 $ Deaths/1M pop   : chr  "601" "366" "503" "589" ...
 $ TotalTests      : chr  "93,242,920" "12,806,189" "5,989,638" "4,948,075" ...
 $ Tests/1M pop    : chr  "281,698" "324,107" "206,569" "230,382" ...
 $ Population      : chr  "" "39,512,223" "28,995,881" "21,477,737" ...
```

--------------------------------------------------------------------------------
## THE COVID-19 USA DASHBOARD
<h4> MAKE SELECTIONS TO GET THE INSIGHTS.</h4>
<p>Use the reactive input panel on the Analysis tab to select the analysis you wish to make:</p>
<p align = "justify"; class = "tab">- To the extent of this assignment, these analysis are limited to Total Cases, Total Deaths, New Cases, New Deaths and Total Recovered across the United States.</p>
<p align = "justify"; class = "tab">- Select the number of ranked states that will display the list of top states for each analysis option.</p>
<p align = "justify"; class = "tab">- After making selections, click on the <b>ANALYSIS</b> button and the server will calculate to extract the data insights.</p>  
<p >From the main panel on the Analysis tab, hover on the graphs to see more insights.</p>  
<p >Switch to the Data tab to see how the filters control and subset data. Click on the <b>Download</b> button to download the csv file. </p>  

--------------------------------------------------------------------------------
## FUTURE DEVELOPMENT
<p align = "justify">My vision is to incorporate more analyses to the dashboard, delivering more insights to users. i.e gender analysis, ethnicity analysis, predictions... </p>
<p align = "justify">Scraping data directly from websites is a temporary solution that is inefficient when dealing with large databases. Our solution is to develop a robust backend infrastructure to store and automatically update the data. This could be done by using R markdown with Rstudio Connect.</p>







