# Changelog

## BiocParallel.FutureParam 0.2.1-9000

## BiocParallel.FutureParam 0.2.1

#### Bug Fixes

- bplapply() and bpiterate() for FutureParam now uses value() instead of
  values(), which is deprecated in future (\>= 1.20.0).

- Using argument ‘result = TRUE’ in internal resolve() calls instead of
  ‘value = TRUE’, which is deprecated in future (\>= 1.15.0).

## BiocParallel.FutureParam 0.2.0

#### Bug Fixes

- FutureParam did not work in Bioconductor (\>= 3.8) due to updates in
  the BiocParallel package.

#### Deprecated and Defunct

- Argument ‘catch.errors’ for FutureParam is now defunct and hidden.

## BiocParallel.FutureParam 0.1.1

#### Software Quality

- TESTS: Now testing FutureParam with all built-in strategies of the
  future package as well as the ‘local’ and ‘interactive’ strategies of
  future.batchtools and future.BatchJobs. In order to test with the
  latter two, those packages need to be installed.

## BiocParallel.FutureParam 0.1.0

#### New Features

- Package created.
