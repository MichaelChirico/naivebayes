# Predict Method for poisson_naive_bayes Objects

Classification based on the Poisson Naive Bayes model.

## Usage

``` r
# S3 method for class 'poisson_naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"),
  threshold = 0.001, eps = 0, ...)
```

## Arguments

- object:

  object of class inheriting from `"poisson_naive_bayes"`.

- newdata:

  matrix with non-negative integer predictors (only numeric matrix is
  accepted).

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
  probabilities by `threshold`.

- ...:

  not used.

## Value

`predict.poisson_naive_bayes` returns either a factor with class labels
corresponding to the maximal conditional posterior probabilities or a
matrix with class label specific conditional posterior probabilities.

## Details

This is a specialized version of the Naive Bayes classifier, in which
all features are non-negative integers and class conditional
probabilities are modelled with the Poisson distribution.

Class posterior probabilities are calculated using the Bayes' rule under
the assumption of independence of predictors. If no `newdata` is
provided, the data from the object is used.

The Poisson Naive Bayes is available in both, `naive_bayes` and
`poisson_naive_bayes`. The implementation of the specialized Naive Bayes
provides more efficient performance though. The speedup comes from the
restricting the data input to a numeric matrix and performing the linear
algebra as well vectorized operations on it.

The NAs in the newdata are not included into the calculation of
posterior probabilities; and if present an informative warning is given.

The `poisson_naive_bayes` function is equivalent to the `naive_bayes`
function with `usepoisson=TRUE` and a numeric matrix or a data.frame
containing only non-negative integer valued features (each variable has
class "integer").

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md),
[`plot.poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/plot.poisson_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md),
[`coef.poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/coef.md)

## Examples

``` r
cols <- 10 ; rows <- 100
M <- matrix(rpois(rows * cols, lambda = 3), nrow = rows, ncol = cols)
# is.integer(M) # [1] TRUE
y <- factor(sample(paste0("class", LETTERS[1:2]), rows, TRUE))
colnames(M) <- paste0("V", seq_len(ncol(M)))
laplace <- 0

### Train the Poisson Naive Bayes
pnb <- poisson_naive_bayes(x = M, y = y, laplace = laplace)

### Classification
head(predict(pnb, newdata = M, type = "class"))
#> [1] classB classB classB classB classB classB
#> Levels: classA classB
head(pnb %class% M)
#> [1] classB classB classB classB classB classB
#> Levels: classA classB

### Posterior probabilities
head(predict(pnb, newdata = M, type = "prob"))
#>          classA    classB
#> [1,] 0.04297243 0.9570276
#> [2,] 0.30693453 0.6930655
#> [3,] 0.17136603 0.8286340
#> [4,] 0.09829519 0.9017048
#> [5,] 0.44241727 0.5575827
#> [6,] 0.37354122 0.6264588
head(pnb %prob% M)
#>          classA    classB
#> [1,] 0.04297243 0.9570276
#> [2,] 0.30693453 0.6930655
#> [3,] 0.17136603 0.8286340
#> [4,] 0.09829519 0.9017048
#> [5,] 0.44241727 0.5575827
#> [6,] 0.37354122 0.6264588
```
