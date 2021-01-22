---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Vector Autoregression with Instrument Variables"
authors: ["Martin Baumgärtner"]
date: 2019-11-19T21:22:38+01:00
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-01-17T21:22:38+01:00


# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""


# Summary. An optional shortened abstract.
summary: "R package for a VAR with external instruments including robust CI"

tags: ["R","VAR"]
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
url_code: "https://github.com/martinbaumgaertner/varexternal"
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

This Package estimates a Vector Autoregressive Model with an External Instrument in R. It is based on

**“Inference in Structural Vector Autoregressions Identified  With and External Instrument”, Montiel Olea, José L; Stock, James H.;  and Watson, Mark W; Working Paper Columbia University.** [Link](http://www.joseluismontielolea.com/papers.html)

The corresponding Matlab code and sample data can be found here: <https://github.com/jm4474/SVARIV>

# Installation:

> install.packages("devtools”) 
> devtools::install_github("https://github.com/martinbaumgaertner/varexternal.git") 
> library(varexternal)

# Content

For now two different Confidence Intervals (CI) for Impulse responses are included:

1. **Delta Method**

2. **Anderson-Rubin confidence set**

   The confidence interval is robust to the construction of  weak-instrument. Note that for strong instrument estimation the CI  convergence to standard CI intervals.

In addition the authors propose an modified Wald test as a test for  weak instruments concerns which is also included in the package.  Bootstrap procedures are currently not included.

> […] these  weak instrument  robust  confidence  sets  should  routinely be used for impulse response coefficients identified with an  external instrument.  Along with  our  weak-instrument  robust   confidence  sets,  we  suggest that  practitioners report either the  Wald   statistic   for   the   null   hypothesis   that   the   external    instrument   is   irrelevant,   or   the heteroskedasticity-robust  first-stage F-statistic as described in Section 4.2. Large values of  these statistics(e.g.,  above  >10)  suggest approximately  valid   coverage of standard  95%  confidence intervals.” (Olea, Stock, Watson 2018)

*Disclaimer: Although the methodology and the basic code is not  mine, all errors are first to be credited to me personally. Please note  that this package has not yet been tested extensively. I am grateful for  every hint for improvement.*

# Example

```r
#load package
library(devtools)
install_github("martinbaumgaertner/varexternal")
library(varexternal)

    data(oil)

    ydata<-oil[,1:3]
    z<-oil[,4]
    p           = 24    #Number of lags in the VAR model
    NWlags      = 0;  # Newey-West lags(if it is neccessary to account for time series autocorrelation)
    norm        = 1; # Variable used for normalization
    scale       = 1; # Scale of the shock
    horizons    = 20; #Number of horizons for the Impulse Response Functions(IRFs)
    confidence=c(0.6,0.9,0.95);

    VAR<-SVARIV(ydata,z,p,confidence,NWlags,norm,scale,horizons,instrument_name="test")

    sh.col<-      c("#E41A1C")
    names(sh.col)<-c("test")
    pretty_irf(data=list(VAR$irfs),shock_names="test",pretty_names=c("a","b","c"),manual_color=sh.col,title="subheading")
```