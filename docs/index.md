# Naïve Bayes

## Overview

The `naivebayes` package presents an efficient implementation of the
widely-used Naïve Bayes classifier. It upholds three core principles:
efficiency, user-friendliness, and reliance solely on Base `R`. By
adhering to the latter principle, the package ensures stability and
reliability without introducing external dependencies[^1]. This design
choice maintains efficiency by leveraging the optimized routines
inherent in Base `R`, many of which are programmed in high-performance
languages like `C/C++` or `FORTRAN`. By following these principles, the
`naivebayes` package provides a reliable and efficient tool for Naïve
Bayes classification tasks, ensuring that users can perform their
analyses effectively and with ease.

The
[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
function is designed to determine the class of each feature in a
dataset, and depending on user specifications, it can assume various
distributions for each feature. It currently supports the following
class conditional distributions:

- categorical distribution for discrete features (with Bernoulli
  distribution as a special case for binary outcomes)
- Poisson distribution for non-negative integer features
- Gaussian distribution for continuous features
- non-parametrically estimated densities via Kernel Density Estimation
  for continuous features

In addition to that specialized functions are available which implement:

- Bernoulli Naive Bayes via
  [`bernoulli_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md)
- Multinomial Naive Bayes via
  [`multinomial_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md)
- Poisson Naive Bayes via
  [`poisson_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md)
- Gaussian Naive Bayes via
  [`gaussian_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md)
- Non-Parametric Naive Bayes via
  [`nonparametric_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/nonparametric_naive_bayes.md)

These specialized functions are carefully optimized for efficiency,
utilizing linear algebra operations to excel when handling dense
matrices. Additionally, they can also exploit *sparsity* of matrices for
enhanced performance and work in presence of missing data. The package
also includes various helper functions to improve user experience.
Moreover, users can access the general
[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
function through the excellent `Caret` package, providing additional
versatility.

## Installation

The `naivebayes` package can be installed from the `CRAN` repository by
simply executing in the console the following line:

``` r
install.packages("naivebayes")

# Or the the development version from GitHub:
devtools::install_github("majkamichal/naivebayes")
```

[^1]: Specialized Naïve Bayes functions within the package may
    optionally utilize sparse matrices if the Matrix package is
    installed. However, the Matrix package is not a dependency, and
    users are not required to install or use it.
