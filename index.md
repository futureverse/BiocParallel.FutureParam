# BiocParallel.FutureParam: Use Futures with BiocParallel

*WARNING: This package is experimental and a proof of concept what could
be done with **BiocParallel** and the future framework.*

## Introduction

The [future](https://cran.r-project.org/package=future) package provides
a generic API for using futures in R. A future is a simple yet powerful
mechanism to evaluate an R expression and retrieve its value at some
point in time. Futures can be resolved in many different ways depending
on which strategy is used. There are various types of synchronous and
asynchronous futures to choose from in the
[future](https://cran.r-project.org/package=future) package. Additional
futures are implemented in other packages. For instance, the
[future.batchtools](https://cran.r-project.org/package=future.batchtools)
package provides futures for *any* type of backend that the
[batchtools](https://cran.r-project.org/package=batchtools) package
supports. For an introduction to futures in R, please consult the
vignettes of the [future](https://cran.r-project.org/package=future)
package.

The
[BiocParallel.FutureParam](https://github.com/HenrikBengtsson/BiocParallel.FutureParam)
package provides FutureParam, a BiocParallelParam class, for the
[BiocParallel](https://bioconductor.org/packages/release/bioc/html/BiocParallel.html)
package that works with *any* type of future. The
BiocParallel.FutureParam package is cross platform just as the future
package.

Below is an example showing how to use FutureParam with *multicore*
futures. A multicore future will be evaluated in parallel using forked
workers, which is not supported on MS Windows when it will fall back to
sequential processing.

``` r
library("BiocParallel.FutureParam")
register(FutureParam())
plan(multicore)

mu <- 1.0
sigma <- 2.0
x <- bplapply(1:3, mu = mu, sigma = sigma, function(i, mu, sigma) {
  rnorm(i, mean = mu, sd = sigma)
})
```

## FutureParam replaces existing BiocParallelParam classes

Due to the generic nature of futures, the FutureParam class provides the
same functionality as many of the existing BiocParallelParam classes,
e.g. SerialParam, SnowParam, MulticoreParam, BatchtoolsParam and
DoparParam. In addition, it provides supports for additional backends
that are not yet implemented in
[BiocParallel](https://bioconductor.org/packages/release/bioc/html/BiocParallel.html),
e.g. [callr](https://cran.r-project.org/package=callr) and
[batchtools](https://cran.r-project.org/package=batchtools).

[TABLE]

## Something not working?

Please note that this package, **BiocParallel.FutureParam**, is in an
experimental stage and does not get as much real-world use as other
**BiocParallel** backends. Thus, if you run into a problem when using
this package, it could very well be a bug. However, before you report
the problem, please try with the
**[doFuture](https://cran.r-project.org/package=doFuture)**,
[`registerDoFuture()`](https://doFuture.futureverse.org/reference/registerDoFuture.html),
and the
[`DoparParam()`](https://rdrr.io/pkg/BiocParallel/man/DoparParam-class.html)
backend of **BiocParallel**, e.g.

``` r
library("BiocParallel")
library("doFuture")
register(DoparParam()) ## Tell BiocParallel to use a foreach backend
registerDoFuture()     ## Tell foreach to use a future backend
plan(multicore)        ## Tell future to use the multicore backend

mu <- 1.0
sigma <- 2.0
x <- bplapply(1:3, mu = mu, sigma = sigma, function(i, mu, sigma) {
  rnorm(i, mean = mu, sd = sigma)
})
```

If that works, but not with `register(FutureParam())`, then it’s a bug
in the **BiocParallel.FutureParam** package. Please report this at
<https://github.com/HenrikBengtsson/BiocParallel.FutureParam/issues>.

## Installation

R package BiocParallel.FutureParam is only available via
[GitHub](https://github.com/futureverse/BiocParallel.FutureParam) and
can be installed in R as:

``` r
remotes::install_github("futureverse/BiocParallel.FutureParam", ref="master")
```

### Pre-release version

To install the pre-release version that is available in Git branch
`develop` on GitHub, use:

``` r
remotes::install_github("futureverse/BiocParallel.FutureParam", ref="develop")
```

This will install the package from source.
