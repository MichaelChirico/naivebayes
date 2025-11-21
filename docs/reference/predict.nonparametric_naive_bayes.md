# Predict Method for nonparametric_naive_bayes Objects

Classification based on the Non-Parametric Naive Bayes model.

## Usage

``` r
# S3 method for class 'nonparametric_naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"),
  threshold = 0.001, eps = 0, ...)
```

## Arguments

- object:

  object of class inheriting from `"nonparametric_naive_bayes"`.

- newdata:

  matrix with metric predictors (only numeric matrix accepted).

- type:

  if "class", new data points are classified according to the highest
  posterior probabilities. If "prob", the posterior probabilities for
  each class are returned.

- threshold:

  value by which zero probabilities or probabilities within the
  epsilon-range corresponding to metric variables are replaced (zero
  probabilities corresponding to categorical variables can be handled
  with Laplace (additive) smoothing).

- eps:

  value that specifies an epsilon-range to replace zero or close to zero
  probabilities by `threshold`. It applies to metric variables.

- ...:

  not used.

## Value

`predict.nonparametric_naive_bayes` returns either a factor with class
labels corresponding to the maximal conditional posterior probabilities
or a matrix with class label specific conditional posterior
probabilities.

## Details

This is a specialized version of the Naive Bayes classifier, in which
all features take on real values (numeric/integer) and class conditional
probabilities are non-parametrically estimated with kernel density
estimator. By default Gaussian kernel is used and the smoothing
bandwidth is selected according to the Silverman's 'rule of thumb'. For
more details, please see the references and the documentation of
[`density`](https://rdrr.io/r/stats/density.html) and
[`bw.nrd0`](https://rdrr.io/r/stats/bandwidth.html).

The Non-Parametric Naive Bayes is available in both,
[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
and
[`nonparametric_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/nonparametric_naive_bayes.md).
This specialized implementation of the Naive Bayes does not provide a
substantial speed-up over the general
[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
function but it should be more transparent and user friendly.

The `nonparametric_naive_bayes` function is equivalent to
[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
when the numeric matrix or a data.frame contains only numeric variables
and `usekernel = TRUE`.

The missing values (NAs) are omitted during the parameter estimation.
The NAs in the newdata in `predict.nonparametric_naive_bayes()` are not
included into the calculation of posterior probabilities; and if present
an informative warning is given.

## References

Silverman, B. W. (1986). Density Estimation for Statistics and Data
Analysis. Chapman & Hall.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`nonparametric_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/nonparametric_naive_bayes.md),
[`plot.nonparametric_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/plot.nonparametric_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md)

## Examples

``` r
data(iris)
y <- iris[[5]]
M <- as.matrix(iris[-5])

### Train the Non-Parametric Naive Bayes
nnb <- nonparametric_naive_bayes(x = M, y = y, bw = "SJ")

### Classification
head(predict(nnb, newdata = M, type = "class"))
#> [1] setosa setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica
head(nnb %class% M)
#> [1] setosa setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica

### Posterior probabilities
head(predict(nnb, newdata = M, type = "prob"))
#>      setosa   versicolor    virginica
#> [1,]      1 6.001557e-10 2.007251e-11
#> [2,]      1 7.629087e-09 1.821586e-10
#> [3,]      1 3.228899e-09 1.609810e-10
#> [4,]      1 2.284583e-09 1.130646e-10
#> [5,]      1 1.873705e-10 1.568085e-11
#> [6,]      1 5.167803e-10 1.025134e-09
head(nnb %prob% M)
#>      setosa   versicolor    virginica
#> [1,]      1 6.001557e-10 2.007251e-11
#> [2,]      1 7.629087e-09 1.821586e-10
#> [3,]      1 3.228899e-09 1.609810e-10
#> [4,]      1 2.284583e-09 1.130646e-10
#> [5,]      1 1.873705e-10 1.568085e-11
#> [6,]      1 5.167803e-10 1.025134e-09
```
