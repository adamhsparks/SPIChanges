
<!-- README.md is generated from README.Rmd. Please edit that file -->

# SPIChanges

<!-- badges: start -->
<!-- badges: end -->

A package designed to improve the interpretation of the Standardized
Precipitation index under changing climate conditions.

# Basic Description

The package improves the interpretation of the Standardized
Precipitation Index (SPI) under changing climate conditions. It is based
on the nonstationary parametric approach proposed in Blain et
al. (2022). This latter study developed a four-step algorithm able to
detect trends in rainfall patterns and to quantify the effect of such
trends on the probability of a SPI value occurring.

## Installation

You can install the development version of SPIChanges from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("gabrielblain/SPIChanges")
```

## Example 1

Aggregating daily rainfall values at 4-quasiWeek time scale, which
corresponds to monthly data.

``` r
library(SPIChanges)
daily.rain <- CampinasRain[,2]
rainTS4 <- TSaggreg(daily.rain=daily.rain,start.date="1991-01-01",TS=4)
#> Done. Just ensure the last quasi-week is complete.
#>   The last day of your series is 31 and TS is 4
View(rainTS4)
```

## Example 2

Using only linear non-stationary parametric models to assess the
probability of rainfall amounts. The models are based on the
two-parameter gamma distribution with parameters estimated by the
maximum likelihood method. The packages `gamlss` and `gamlss.dist` are
used for such estimations.

``` r
#
library(SPIChanges)
daily.rain <- CampinasRain[,2]
rainTS4 <- TSaggreg(daily.rain=daily.rain,start.date="1991-01-01",TS=4)
#> Done. Just ensure the last quasi-week is complete.
#>   The last day of your series is 31 and TS is 4
Changes.in.the.SPI <- SPIChanges(rain.at.TS=rainTS4, only.linear = "Yes")
View(Changes.in.the.SPI$data.week)
View(Changes.in.the.SPI$data.week)
View(Changes.in.the.SPI$model.selection)
View(Changes.in.the.SPI$Changes.Freq.Drought)
```

## Example 3

Using linear and non-linear non-stationary parametric models to assess
the probability of rainfall amounts. The models are based on the
two-parameter gamma distribution with parameters estimated by the
maximum likelihood method. The packages `gamlss` and `gamlss.dist` are
used for such estimations.

``` r
#
library(SPIChanges)
daily.rain <- CampinasRain[,2]
rainTS4 <- TSaggreg(daily.rain=daily.rain,start.date="1991-01-01",TS=4)
#> Done. Just ensure the last quasi-week is complete.
#>   The last day of your series is 31 and TS is 4
Changes.in.the.SPI <- SPIChanges(rain.at.TS=rainTS4, only.linear = "No")
View(Changes.in.the.SPI$data.week)
View(Changes.in.the.SPI$data.week)
View(Changes.in.the.SPI$model.selection)
View(Changes.in.the.SPI$Changes.Freq.Drought)
```

## BugReports:

\<<https://github.com/gabrielblain/SPIChanges/issues> \>

## License:

MIT

## Authors:

Gabriel Constantino Blain, Graciela da Rocha Sobierajski. Maintainer:
Gabriel Constantino Blain, <gabriel.blain@sp.gov.br>

## Acknowledgments:

The package uses data from the Agronomic Institute of Campinas. The
authors greatly appreciate this initiative.

## References

Blain G C, Sobierajski G R, Weight E, Martins L L, Xavier A C F 2022.
Improving the interpretation of standardized precipitation index
estimates to capture drought characteristics in changing climate
conditions. International Journal of Climatology, 42, 5586-5608.
<https://doi.org/10.1002/joc.7550>

Package ‘gamlss’, Version 5.4-22, Author Stasinopoulos Mikis et al.,
<https://CRAN.R-project.org/package=gamlss>

Package ‘gamlss.dist’, Version 6.1-1, Author Stasinopoulos Mikis et al.,
<https://CRAN.R-project.org/package=gamlss.dist>
