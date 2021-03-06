
DATA SCIENCE FOR BUSINESS PRGM - 2014-2015 Autumn
================================================================================
width: 1920
height: 1080

Author: Gene Leynes

Date: September 18, 2014



How to learn R
================================================================================

"There are many like it, but this one is mine."  - from the Rifleman's Creed, Major General William H. Rupertus 

There is a truly vast and ever growing growing body of literature dedicated to helping people learn R, however not all of the information is created equally. 

 - CRAN is always the maintainer of the R application and the default source of information: http://cran.r-project.org/
 - Currently, R Studio is the best choice for code editing and project mangement http://www.rstudio.com/
 - R has hundreds of user contributed libraries that you can install within R.
 
CRAN Specific resources:
 - The R FAQs are invaluable: http://cran.r-project.org/faqs.html
 - The statndard documentation is also invaluable: http://cran.r-project.org/manuals.html
 - There are several "task views" that are very helpful for learning about R resources associated with particular tasks.
 - You can access help right from R with "?".  For example, you can learn about the `lm` funciton by typing `?lm` at the console.
 - CRAN resources and help can be very hard to understand, this is normal.  Use many approaches to solve problems. 
 - Download and print this cheat sheet: http://cran.r-project.org/doc/contrib/Short-refcard.pdf
 - See also http://cran.r-project.org/doc/contrib/Baggott-refcard-v2.pdf (this one is new to me)


Where to get help
================================================================================

<br>
 - Pay attention to _when_ something was written, and to _who_ wrote it. Some people seem to write guides as a way of learning themselves...
 - Early R contributors really understand the internals, but their writings can be hard to understand.
 - Newer R contributors tend to approach things from the perspective of their particular angle / set of packages 
 - Stack Overflow is a great place to find questions and answers if you get stuck. http://stackoverflow.com/questions/tagged/R
 - I highly recommend Stack Overflow over the r-help mailing list. 
 - Many pacakges have vignettes which can be extremely helpful.

------------------------
Stackoverflow posting guide:
------------------------
![SO Posting guide](images_lec2/tech_support_cheat_sheet.png)<br>
source: http://www.xkcd.com/627/

Standing on the shoulders of giants
================================================================================
<br>
### Best Guides:
My favorite R resources for quick help:
 - http://www.cookbook-r.com/
 - http://www.r-statistics.com/

If you have experienced a singularity and have near infinite time to think:
 - http://www.r-bloggers.com/
 - http://cran.r-project.org/doc/contrib/
 - http://cran.r-project.org/doc/contrib/usingR.pdf
 - http://cran.r-project.org/web/views/

-------------
<br>
### Best packages:
 - `data.table` The data frame evolved.
  - http://cran.r-project.org/web/packages/data.table/vignettes/datatable-faq.pdf
 - `ggplot2` Hadley's Grammar of graphics
 	- http://ggplot2.org/
 	- http://www.cookbook-r.com/Graphs/
 - `caret` Max Kuhn's machine learning pacakge
    - http://topepo.github.io/caret/index.html 
 	- http://www.amazon.com/Applied-Predictive-Modeling-Max-Kuhn/dp/1461468485
 - `knitr` Yihui Xie's report writing tool based on markdown
 	- http://yihui.name/knitr/
 	- http://rmarkdown.rstudio.com/
 - `shiny` R Studio's jQuery powered application maker
 	- http://shiny.rstudio.com/


Big picture of R
================================================================================

<br>
**Things to install**
 - R http://cran.r-project.org/
 - RStudio  http://www.rstudio.com/products/rstudio/download/
 - git http://git-scm.com/downloads

**Things in R**
 - Elements
 - Vectors
 - Matricies
 - Data frames
 - Lists
 - Environments
 - Functions

-------------
<br>
**Things in R that do things (mostly within R)**
 - Scripts
 - Projects
 - Packages on CRAN (install.packages)
 - Packages elsewhere (devtools)

**There are different ways to use R**
 - Step through code
 - Run a script at the command line
 - Put things into functions (more like making software)

**Technical details**
 - The PATH environmental variable
 - Environmental variables
 - You don't need admin rights to have a good time
 - R was not written by pirates
 - R was not written programmers either



Start of a typical script
================================================================================

Because the environment is completely initialized, the result is reproducable.

```r
##------------------------------------------------------------------------------
## INITIALIZATION
##------------------------------------------------------------------------------
rm(list=ls())
gc()
library(geneorama)
detach_nonstandard_packages()
library(geneorama)
loadinstall_libraries(c("geneorama", "data.table", "reshape2", "Matrix"))

sourceDir("functions/")
op <- readRDS("data/op.Rds")  ## Default par
par(op)

##------------------------------------------------------------------------------
## Load data for vacant buildings and violations
##------------------------------------------------------------------------------
filepath1 <- "data/20140507/Building_Violations.Rds"
filepath2 <- "data/20140507/Building_Violations__VIOLATION_ORDINANCE.Rds"
filepath3 <- "data/20140507/Building_Violations__VIOLATION_ORDINANCE_dummy_matrix.Rds"

datBuild <- readRDS(filepath1)
VIOLATION_ORDINANCE <- readRDS(filepath2)
VIOLATION_ORDINANCE_DM <- readRDS(filepath3)

##------------------------------------------------------------------------------
## (describe next steps here...)
##------------------------------------------------------------------------------

## Typically this includes, data prep, analysis, saving results
```

Typical Project's folder structure (more about this later)
================================================================================

<br>
## Project structure
![TypicalProject](images_lec1/TypicalProject.png)  

**********

<br>
## Data Structure
![TypicalProject](images_lec1/TypicalProjectData.png)




================================================================================
# Small Example

Topics: Assignment, variables, functions, random number generation,
        factors, comments, vectors


```r
rm(list=ls())

## Boxplot Example with gl
g <- factor(round(10 * runif(10*100)))
x <- rnorm(10*100) + sqrt(as.numeric(g))

boxplot(x~g, col='lavender', notch=T, var.width=T,
		main = "something random")
```

<img src="Lecture_2-figure/unnamed-chunk-3.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />


================================================================================
# `ggplot` (Grammar of graphics) Example


```r
rm(list=ls());library(data.table);library(ggplot2);
## Generate some data:
MyData <- data.table(group = factor(round(10 * runif(10*100))))
MyData[ , YValue := rnorm(10*100) + sqrt(as.numeric(group))]
## GGplot code:
ggplot(MyData) + aes(x=group, y=YValue, color=group) + 
	geom_boxplot()
```

<img src="Lecture_2-figure/unnamed-chunk-4.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

```r
# ggplot(MyData) + aes(x=group, y=YValue, color=group) + 
# 	geom_point()
```

================================================================================
# Tsay Time Series book cover

Topics: How to untangle code


```r
# Make two plots on the same canvas # Legend # Random walk  # Tsay book cover
set.seed(123456)
e <- rnorm(500)           ## White noise
randwalk <- cumsum(e)     ## Random walk
trend <- 1:500            ## Trend
plot.ts(0.5 * trend + e, lty=1, ylab='', xlab='')  ## deterministic trend + noise
lines(0.5 * trend + cumsum(e), lty=2)              ## random walk with drift
lines(randwalk, lty=3, col='red')                  ## random walk (same scale)
par(new=T)
plot.ts(randwalk, lty=3, axes=FALSE, col='red')    ## random walk (own scale)
axis(4, pretty(range(randwalk)))
legend(10, 18.7, legend=c('deterministic trend + noise (left)',
						  'random walk w/ drift (left)', 'random walk (left+right)'),
	   lty=c(1, 2, 3), col=c('black', 'black', 'red')) 
```

<img src="Lecture_2-figure/unnamed-chunk-5.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />

================================================================================
# Tsay Time Series book cover (plot from previous slide)


<img src="Lecture_2-figure/unnamed-chunk-6.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

================================================================================
# Source Control using git

I _highly_ recommend that you avoid using a GUI for git.

The ruby on rails book has an excellent and concise description of how to use git
 - https://www.railstutorial.org/book/beginning#sec-version_control
source: RUBY ON RAILS TUTORIAL - Learn Rails by Example by Michael Hartl

The website that hosts git also host the best documentation on git.
 - http://git-scm.com/
 
Also, github has excellent documentation, especially on technical issues like RSA keys and ssh access.
 - https://github.com/

Github uses git, but they are not the same things!
People seem to think that github is git.  Github is a host (probably the best host) were people can share git repositories.

https://github.com/ <br>
https://github.com/geneorama/  <<- me

## File comparison

It's important to have a good way to compare and merge files.  My preferred solution is Winmerge, but you can find many other programs online
 - http://winmerge.org/




