# BiocParallel.FutureParam: A BiocParallelParam class using Futures

The BiocParallel.FutureParam package provides
[FutureParam](https://BiocParallel.FutureParam.futureverse.org/reference/FutureParam.md),
a
[BiocParallel::BiocParallelParam](https://rdrr.io/pkg/BiocParallel/man/BiocParallelParam-class.html)
class, for the BiocParallel package that works with *any* type of
future. (that is supported by Future API of the future package) can be
used for asynchronous (parallel/distributed) or synchronous (sequential)
processing.

## Details

Futures themselves are provided by the future package, e.g. multicore,
multisession, ad hoc cluster, and MPI cluster futures. Additional
futures are provided by other packages. For example, batchtools futures
are implemented by the future.batchtools package, which expands the
support for asynchronous processing to anything that the batchtools
package supports.

To use futures with the BiocParallel package, load
BiocParallel.FutureParam, call `register(FutureParam())`, select the
type of future you wish to use via `future:plan()`.

## See also

Useful links:

- <https://BiocParallel.FutureParam.futureverse.org>

- <https://github.com/HenrikBengtsson/BiocParallel.FutureParam>

- Report bugs at
  <https://github.com/HenrikBengtsson/BiocParallel.FutureParam/issues>

## Author

**Maintainer**: Henrik Bengtsson <henrikb@braju.com> \[copyright
holder\]

Other contributors:

- Ryan Thompson \[contributor\]

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
