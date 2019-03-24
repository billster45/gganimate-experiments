Understanding gganimate intuitively
================

-   [Introduction](#introduction)
-   [transition\_reveal()](#transition_reveal)
-   [transition\_states()](#transition_states)
-   [transition\_time() & shadow\_wake()](#transition_time-shadow_wake)
-   [transition\_states() & shadow\_wake()](#transition_states-shadow_wake)
-   [transition\_time() & shadow\_mark()](#transition_time-shadow_mark)

Introduction
============

This set of gganimate examples comes from the excellent slides tweeted here: <https://twitter.com/mitchoharawild/status/1108913366100119553?s=12>

The tweet links to these great slides: <https://mitchelloharawild.com/wombat-gganimate/#1>

Code for the slides is here: <https://github.com/numbats/gganimate-workshop>

To help understand more intuitively how gganimate works, most of the examples from the slides are presented below as static ggplot charts along with a few rows of the raw data. Then as the animated version using gganimate.

I've also made it clear which package each function comes from, either ggplot2 or gganimate by adding ggnaimte:: or ggplot2:: before each function.

``` r
library(ggplot2)
library(gganimate)
library(transformr) # devtools::install_github("thomasp85/transformr")
library(magick)
library(gifski)
library(png)
library(datasauRus)
library(gapminder)
library(kableExtra)

kable_table <- function(table, title) {
  kableExtra::kable(table, caption = title) %>%
    kable_styling(latex_options = "hold_position", full_width = F, bootstrap_options = c("striped", "condensed"), position = "left")
}
```

transition\_reveal()
====================

Adapting this example: <https://mitchelloharawild.com/wombat-gganimate/#37>

Static ggplot plot

``` r
p <- 
  ggplot2::ggplot(ggplot2::economics) +
  ggplot2::aes(date, unemploy) +
  ggplot2::geom_line() +
  ggplot2::theme_minimal()

ggplot2::ggsave(filename = "./images/economics.png")
```

![](./images/economics.png)

``` r
kable_table(head(economics), "Top few rows of ggplot2::economics data in plot above")
```

<table class="table table-striped table-condensed" style="width: auto !important; ">
<caption>
Top few rows of ggplot2::economics data in plot above
</caption>
<thead>
<tr>
<th style="text-align:left;">
date
</th>
<th style="text-align:right;">
pce
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
psavert
</th>
<th style="text-align:right;">
uempmed
</th>
<th style="text-align:right;">
unemploy
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
1967-07-01
</td>
<td style="text-align:right;">
507.4
</td>
<td style="text-align:right;">
198712
</td>
<td style="text-align:right;">
12.5
</td>
<td style="text-align:right;">
4.5
</td>
<td style="text-align:right;">
2944
</td>
</tr>
<tr>
<td style="text-align:left;">
1967-08-01
</td>
<td style="text-align:right;">
510.5
</td>
<td style="text-align:right;">
198911
</td>
<td style="text-align:right;">
12.5
</td>
<td style="text-align:right;">
4.7
</td>
<td style="text-align:right;">
2945
</td>
</tr>
<tr>
<td style="text-align:left;">
1967-09-01
</td>
<td style="text-align:right;">
516.3
</td>
<td style="text-align:right;">
199113
</td>
<td style="text-align:right;">
11.7
</td>
<td style="text-align:right;">
4.6
</td>
<td style="text-align:right;">
2958
</td>
</tr>
<tr>
<td style="text-align:left;">
1967-10-01
</td>
<td style="text-align:right;">
512.9
</td>
<td style="text-align:right;">
199311
</td>
<td style="text-align:right;">
12.5
</td>
<td style="text-align:right;">
4.9
</td>
<td style="text-align:right;">
3143
</td>
</tr>
<tr>
<td style="text-align:left;">
1967-11-01
</td>
<td style="text-align:right;">
518.1
</td>
<td style="text-align:right;">
199498
</td>
<td style="text-align:right;">
12.5
</td>
<td style="text-align:right;">
4.7
</td>
<td style="text-align:right;">
3066
</td>
</tr>
<tr>
<td style="text-align:left;">
1967-12-01
</td>
<td style="text-align:right;">
525.8
</td>
<td style="text-align:right;">
199657
</td>
<td style="text-align:right;">
12.1
</td>
<td style="text-align:right;">
4.8
</td>
<td style="text-align:right;">
3018
</td>
</tr>
</tbody>
</table>
Animated ggnanimate plot

``` r
p +
  gganimate::transition_reveal(date)
```

![](README_files/figure-markdown_github/unnamed-chunk-4-1.gif)

``` r
gganimate::anim_save(filename = "./images/along.gif")
```

![](./images/along.gif)

transition\_states()
====================

This example: <https://mitchelloharawild.com/wombat-gganimate/#42>

Static ggplot chart

``` r
p <- 
  ggplot2::ggplot(data = datasauRus::datasaurus_dozen) +
  ggplot2::aes(x, y) +
  ggplot2::geom_point() +
  ggplot2::facet_wrap(~dataset)  +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
kable_table(head(datasauRus::datasaurus_dozen), "Top few rows of datasauRus::datasaurus_dozen data in plot above")
```

<table class="table table-striped table-condensed" style="width: auto !important; ">
<caption>
Top few rows of datasauRus::datasaurus\_dozen data in plot above
</caption>
<thead>
<tr>
<th style="text-align:left;">
dataset
</th>
<th style="text-align:right;">
x
</th>
<th style="text-align:right;">
y
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
55.3846
</td>
<td style="text-align:right;">
97.1795
</td>
</tr>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
51.5385
</td>
<td style="text-align:right;">
96.0256
</td>
</tr>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
46.1538
</td>
<td style="text-align:right;">
94.4872
</td>
</tr>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
42.8205
</td>
<td style="text-align:right;">
91.4103
</td>
</tr>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
40.7692
</td>
<td style="text-align:right;">
88.3333
</td>
</tr>
<tr>
<td style="text-align:left;">
dino
</td>
<td style="text-align:right;">
38.7179
</td>
<td style="text-align:right;">
84.8718
</td>
</tr>
</tbody>
</table>
Animated gganimate plot

``` r
p <- 
  ggplot2::ggplot(data = datasauRus::datasaurus_dozen) +
  ggplot2::aes(x, y) +
  ggplot2::geom_point() +
  # ggplot2::facet_wrap(~dataset)
  gganimate::transition_states(states = dataset, transition_length = 3, state_length = 1) +
  ggplot2::labs(title = "Dataset: {closest_state}") +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-6-1.gif)

transition\_time() & shadow\_wake()
===================================

This example: <https://mitchelloharawild.com/wombat-gganimate/#74>

Static ggplot plot

``` r
p <- 
  ggplot2::ggplot(data = gapminder::gapminder) + 
  ggplot2::aes(x = gdpPercap, y=lifeExp, size = pop, colour = country) +
  ggplot2::geom_point(show.legend = FALSE) +
  ggplot2::scale_x_log10() +
  ggplot2::scale_color_viridis_d() +
  ggplot2::scale_size(range = c(2, 12)) +
  ggplot2::labs(x = "GDP per capita", y = "Life expectancy") +
  ggplot2::facet_wrap(~year) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-7-1.png)

``` r
kable_table(head(gapminder::gapminder), "Top few rows of gapminder::gapminder data in plot above")
```

<table class="table table-striped table-condensed" style="width: auto !important; ">
<caption>
Top few rows of gapminder::gapminder data in plot above
</caption>
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
</tbody>
</table>
Animated gganimate plot

``` r
p <- 
  ggplot2::ggplot(data = gapminder::gapminder) + 
  ggplot2::aes(x = gdpPercap, y=lifeExp, size = pop, colour = country) +
  ggplot2::geom_point(show.legend = FALSE) +
  ggplot2::scale_x_log10() +
  ggplot2::scale_color_viridis_d() +
  ggplot2::scale_size(range = c(2, 12)) +
  ggplot2::labs(x = "GDP per capita", y = "Life expectancy") +
  # ggplot2::facet_wrap(~year)
  gganimate::transition_time(time = year) +
  ggplot2::labs(title = "Year: {frame_time}") +
  gganimate::shadow_wake(wake_length = 0.1, alpha = FALSE) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-8-1.gif)

transition\_states() & shadow\_wake()
=====================================

This example: <https://mitchelloharawild.com/wombat-gganimate/#57>

Static ggplot plot

``` r
p <- 
  ggplot2::ggplot(data = datasets::iris) +
  ggplot2::aes(x = Petal.Length, y = Sepal.Length) +
  ggplot2::geom_point(size = 2) +
  ggplot2::facet_wrap(~Species) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-9-1.png)

``` r
kable_table(head(datasets::iris), "Top few rows of datasets::iris data in plot above")
```

<table class="table table-striped table-condensed" style="width: auto !important; ">
<caption>
Top few rows of datasets::iris data in plot above
</caption>
<thead>
<tr>
<th style="text-align:right;">
Sepal.Length
</th>
<th style="text-align:right;">
Sepal.Width
</th>
<th style="text-align:right;">
Petal.Length
</th>
<th style="text-align:right;">
Petal.Width
</th>
<th style="text-align:left;">
Species
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
5.1
</td>
<td style="text-align:right;">
3.5
</td>
<td style="text-align:right;">
1.4
</td>
<td style="text-align:right;">
0.2
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
<tr>
<td style="text-align:right;">
4.9
</td>
<td style="text-align:right;">
3.0
</td>
<td style="text-align:right;">
1.4
</td>
<td style="text-align:right;">
0.2
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
<tr>
<td style="text-align:right;">
4.7
</td>
<td style="text-align:right;">
3.2
</td>
<td style="text-align:right;">
1.3
</td>
<td style="text-align:right;">
0.2
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
<tr>
<td style="text-align:right;">
4.6
</td>
<td style="text-align:right;">
3.1
</td>
<td style="text-align:right;">
1.5
</td>
<td style="text-align:right;">
0.2
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
<tr>
<td style="text-align:right;">
5.0
</td>
<td style="text-align:right;">
3.6
</td>
<td style="text-align:right;">
1.4
</td>
<td style="text-align:right;">
0.2
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
<tr>
<td style="text-align:right;">
5.4
</td>
<td style="text-align:right;">
3.9
</td>
<td style="text-align:right;">
1.7
</td>
<td style="text-align:right;">
0.4
</td>
<td style="text-align:left;">
setosa
</td>
</tr>
</tbody>
</table>
Animated gganimate plot

``` r
p <- 
  ggplot2::ggplot(data = datasets::iris) +
  ggplot2::aes(x = Petal.Length, y = Sepal.Length) +
  ggplot2::geom_point(size = 2) +
  # ggplot2::facet_wrap(~Species)
  gganimate::transition_states(states = Species, transition_length = 4, state_length = 1) +
  ggplot2::labs(title = "{closest_state}") +
  gganimate::shadow_wake(wake_length = 0.1) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-10-1.gif)

transition\_time() & shadow\_mark()
===================================

This example: <https://mitchelloharawild.com/wombat-gganimate/#58>

Static ggplot plot

``` r
p <- 
  ggplot2::ggplot(data = datasets::airquality) +
  ggplot2::aes(x = Day, y = Temp) +
  ggplot2::geom_line(color = 'steelblue', size = 1) +
  ggplot2::facet_wrap(~Month) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-11-1.png)

``` r
kable_table(head(datasets::airquality), "Top few rows of datasets::airquality data in plot above")
```

<table class="table table-striped table-condensed" style="width: auto !important; ">
<caption>
Top few rows of datasets::airquality data in plot above
</caption>
<thead>
<tr>
<th style="text-align:right;">
Ozone
</th>
<th style="text-align:right;">
Solar.R
</th>
<th style="text-align:right;">
Wind
</th>
<th style="text-align:right;">
Temp
</th>
<th style="text-align:right;">
Month
</th>
<th style="text-align:right;">
Day
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
41
</td>
<td style="text-align:right;">
190
</td>
<td style="text-align:right;">
7.4
</td>
<td style="text-align:right;">
67
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:right;">
36
</td>
<td style="text-align:right;">
118
</td>
<td style="text-align:right;">
8.0
</td>
<td style="text-align:right;">
72
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:right;">
12.6
</td>
<td style="text-align:right;">
74
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
3
</td>
</tr>
<tr>
<td style="text-align:right;">
18
</td>
<td style="text-align:right;">
313
</td>
<td style="text-align:right;">
11.5
</td>
<td style="text-align:right;">
62
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
14.3
</td>
<td style="text-align:right;">
56
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:right;">
28
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
14.9
</td>
<td style="text-align:right;">
66
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
6
</td>
</tr>
</tbody>
</table>
Animated gganimate plot

``` r
p <- 
  ggplot2::ggplot(data = datasets::airquality) +
  ggplot2::aes(x = Day, y = Temp) +
  ggplot2::geom_line(color = 'steelblue', size = 1) +
  # ggplot2::facet_wrap(~Month)
  gganimate::transition_time(time = Month) +
  ggplot2::labs(title = "Month: {frame_time}") +
  gganimate::shadow_mark(colour = 'grey', size = 0.75) +
  ggplot2::theme_minimal()
p
```

![](README_files/figure-markdown_github/unnamed-chunk-12-1.gif)
