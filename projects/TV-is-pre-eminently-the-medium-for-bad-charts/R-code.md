TV is Pre-Eminently the Medium for Unreadable 3D Charts
================

In this file the code that generated the [two data visualisations](https://cdn-images-1.medium.com/max/1440/1*NSnCq2bex1J3RduOw-mHkQ.png) in the article [TV is Pre-Eminently the Medium for Unreadable 3D Charts](https://medium.com/tdebeus/tv-is-pre-eminently-the-medium-for-unreadable-3d-charts-9715c18d8edf) on [Colourful Facts](https://medium.com/tdebeus). The article is about the redesign of a graph that's shown on a Dutch talkshow. The subject is the 2017 UK election results or exit polls. The redesign shows a dot matrix plot and a slope graph.

The visualisations deviate from the end result in the portfolio, this is because I finalise the visuals in [Sketch](https://www.sketchapp.com/).

First thing first: loading the used R packages.

``` r
library(tidyverse)
library(waffle)
```

Data preparation
================

``` r
# Needed variables
parties <- c("CON", "CON", "LAB", "LAB", 
             "SNP", "SNP", "LD", "LD", "DUP", "DUP", "Others", "Others")
year <- c(2015, 2017, 2015, 2017, 2015, 2017, 2015, 2017, 2015, 2017, 2015, 2017)
seats <- c(331, 318, 232, 261, 56, 35, 8, 12, 8, 10, 15, 13)
# Create data frame
df2 <- cbind.data.frame(parties, year, seats)
# Convert variable year from numeric to factor.
df2$year <- as.factor(df2$year)
# Create custom colour variable to use in plots.
colours <- c(CON = "#0073CC",
             LAB = "#F01900",
             SNP = "#F8DD00",
             LD = "#E76600",
             DUP = "#C20F3A",
             Others = "#BDBDBD")
```

Visualising the data with a slope chart
---------------------------------------

``` r
slopeChart <- ggplot(df2, aes(year, 
                seats, 
                colour = parties, 
                group = parties)) +
  geom_point(aes(size = seats)) +
  geom_line() +
  scale_color_manual(values = colours) +
  theme(panel.grid = element_blank(),
        legend.position = "none",
        panel.background = element_blank(),
        plot.background = element_rect(fill = "#F4EBDB"),
        axis.text.y = element_blank(),
        axis.ticks = element_blank(),
        axis.title.y = element_blank()) +
  geom_text(aes(x = year,
                y = seats,
                label = seats),
            vjust = 0, 
            nudge_y = 10,
            colour = "black")

# Plot
slopeChart
```

<img src="R-code_files/figure-markdown_github-ascii_identifiers/slope graph-1.png" style="display: block; margin: auto;" />

The dot matrix chart
--------------------

With the waffle package I visualised all the seats after the election results. With Sketch I made it like a dot plot. See how easy?

``` r
seatsUK <- c(`Tories (318)` = 318,
           `DUP (10)` = 12,
           `SNP (35)` = 35,
           `LD (12)` = 10,
           `Others (13)` = 13,
           `Labour (262)` = 262) 

waffle <- waffle(seatsUK, rows = 13, size = 0.5,
       colors = c("#0073CC", "#C20F3A", "#F8DD00", "#E76600", "#BDBDBD", "#F01900"),
       title = "UK Seats Distribution After 2017 Election")

# Plot
waffle
```

<img src="R-code_files/figure-markdown_github-ascii_identifiers/waffle chart-1.png" style="display: block; margin: auto;" />
