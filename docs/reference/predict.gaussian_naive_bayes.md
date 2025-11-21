# Predict Method for gaussian_naive_bayes Objects

Classification based on the Gaussian Naive Bayes model.

## Usage

``` r
# S3 method for class 'gaussian_naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"),
  threshold = 0.001, eps = 0, ...)
```

## Arguments

- object:

  object of class inheriting from `"gaussian_naive_bayes"`.

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

`predict.gaussian_naive_bayes` returns either a factor with class labels
corresponding to the maximal conditional posterior probabilities or a
matrix with class label specific conditional posterior probabilities.

## Details

This is a specialized version of the Naive Bayes classifier, in which
all features take on real values and class conditional probabilities are
modelled with the Gaussian distribution.

Class posterior probabilities are calculated using the Bayes' rule under
the assumption of independence of predictors. If no `newdata` is
provided, the data from the object is used.

The Gaussian Naive Bayes is available in both, `naive_bayes` and
`gaussian_naive_bayes`. The implementation of the specialized Naive
Bayes provides more efficient performance though. The speedup comes from
the restricting the data input to a numeric matrix and performing the
linear algebra as well vectorized operations on it. In other words, the
efficiency comes at cost of the flexibility.

The NAs in the newdata are not included into the calculation of
posterior probabilities; and if present an informative warning is given.

The `gaussian_naive_bayes` function is equivalent to the `naive_bayes`
function with the numeric matrix or a data.frame containing only numeric
variables.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md),
[`plot.gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/plot.gaussian_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md)

## Examples

``` r
data(iris)
y <- iris[[5]]
M <- as.matrix(iris[-5])

### Train the Gaussian Naive Bayes
gnb <- gaussian_naive_bayes(x = M, y = y)

### Classification
head(predict(gnb, newdata = M, type = "class"))
#> [1] setosa setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica
head(gnb %class% M)
#> [1] setosa setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica

### Posterior probabilities
head(predict(gnb, newdata = M, type = "prob"))
#>      setosa   versicolor    virginica
#> [1,]      1 2.981309e-18 2.152373e-25
#> [2,]      1 3.169312e-17 6.938030e-25
#> [3,]      1 2.367113e-18 7.240956e-26
#> [4,]      1 3.069606e-17 8.690636e-25
#> [5,]      1 1.017337e-18 8.885794e-26
#> [6,]      1 2.717732e-14 4.344285e-21
head(gnb %prob% M)
#>      setosa   versicolor    virginica
#> [1,]      1 2.981309e-18 2.152373e-25
#> [2,]      1 3.169312e-17 6.938030e-25
#> [3,]      1 2.367113e-18 7.240956e-26
#> [4,]      1 3.069606e-17 8.690636e-25
#> [5,]      1 1.017337e-18 8.885794e-26
#> [6,]      1 2.717732e-14 4.344285e-21
```
