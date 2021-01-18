---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Monetary policy shocks from EA-MPD data"
authors: ["Martin Baumgärtner"]
date: 2021-01-19T21:22:38+01:00
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-01-17T21:22:38+01:00


# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""


# Summary. An optional shortened abstract.
summary: "R package to calculate monetary policy shocks with the high frequency data from the Euro Area Monetary Policy Event-Study Database (EA-MPD)."
tags: ["R","VAR", "Monetary Economics"]
categories: []
featured: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: 
url_code: "https://github.com/martinbaumgaertner/hfdshocks"
url_dataset:
url_poster:
url_project:
url_slides:
url_source:
url_video:

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---

This Package estimates the monetary policy surprises from high-frequency data in R. It is based on

**Altavilla, C., Brugnolini, L., Gürkaynak, R. S., Motto, R., & Ragusa, G. (2019). Measuring euro area monetary policy. Journal of Monetary Economics, 108, 162-179.** [Link](https://www.sciencedirect.com/science/article/pii/S0304393219301497)

The corresponding Julia/R/Stata code and sample data can be found here: <http://www.bilkent.edu.tr/~refet/ABGMR_replication_files.zip> (by Refet S. Gürkaynak)

# Installation:

> library(“devtools”) 
>
> devtools::install_github("https://github.com/martinbaumgaertner/hfdshocks.git") 
>
> library(hfdshocks)

# Content

The package downloads the EA-MPD data and calculates the monetary policy shocks.

Please note that the current data of the EA-MPD have been slightly revised compared to the original data of the paper. Accordingly, the calculated surprises are (slightly) different from the original surprises. To reproduce the original data uses the original database from the replication files. So far, I have not been able to find any significant difference in VAR models.

There are various setting options:

​	**Exclude outlier**

​	If you want to exclude data as outliers, enter them here. No specific date format is required. The standard excludes 3 data points based on the original 
​    paper.  : 2001-09-17, 2008-10-08, 2008-11-06

​	**Specify data window**

​	Changes the window of the input data. This influences the final result! Until now, I recommend using all data up to the current point in time and then
​    shorten the time series afterwards. Nevertheless, the default in the package is the time window used in the original paper

​	**Specify Crisis date**

​	The third factor (QE) is calculated by minimising the variance before the financial crisis. The corresponding value can be changed here.

*Disclaimer: Although the methodology is not  mine, all errors are first to be credited to me personally. Please note  that this package has not yet been tested extensively. I am grateful for  every hint for improvement.*

# Example

```r
#load package
library(devtools)
devtools::install_github("https://github.com/martinbaumgaertner/hfdshocks.git") 

library(hfdshocks)
ecb_shocks("https://www.ecb.europa.eu/pub/pdf/annex/Dataset_EA-MPD.xlsx","",
               exclude_date=c("2001-09-17","2008-10-08","2008-11-06"),
               range=c("2001-12-31","2018-09-13"),crisis_date="2008-09-04")
```