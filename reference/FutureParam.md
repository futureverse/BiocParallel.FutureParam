# Creates a FutureParam object

Creates a FutureParam object

## Usage

``` r
FutureParam(...)
```

## Arguments

- ...:

  Arguments passed to the initialization method of
  [BiocParallel::BiocParallelParam](https://rdrr.io/pkg/BiocParallel/man/BiocParallelParam-class.html).

## Value

A
[BiocParallel::BiocParallelParam](https://rdrr.io/pkg/BiocParallel/man/BiocParallelParam-class.html)
object of class FutureParam.

## Examples

``` r
library("BiocParallel.FutureParam")
register(FutureParam())
plan(multisession)

mu <- 1.0
sigma <- 2.0
x <- bplapply(1:3, mu = mu, sigma = sigma, function(i, mu, sigma) {
  rnorm(i, mean = mu, sd = sigma)
})
#> Error in .composeTry(FUN, bplog(BPPARAM), bpstopOnError(BPPARAM), stop.immediate = bpstopOnError(BPPARAM),     timeout = bptimeout(BPPARAM)): unused arguments (stop.immediate = bpstopOnError(BPPARAM), timeout = bptimeout(BPPARAM))
print(x)
#> Error: object 'x' not found

## WORKAROUND: For some reason, 'R CMD check' on Windows will give an
## error when running this example with plan(multisession), unless we
## reset the future plan at the end.
plan(sequential)
```
