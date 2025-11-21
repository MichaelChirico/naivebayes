# Predict Method for Family of Naive Bayes Objects

The infix operators `%class%` and `%prob%` are shorthands for performing
classification and obtaining posterior probabilities, respectively.

## Usage

``` r
lhs %class% rhs
lhs %prob% rhs
```

## Arguments

- lhs:

  object of class inheriting from `"naive_bayes"` and `"*_naive_bayes"`
  family.

- rhs:

  dataframe or matrix for "naive_bayes" objects OR matrix for all
  "\*\_naive_bayes" objects.

## Value

- `%class%` returns factor with class labels corresponding to the
  maximal conditional posterior probabilities.

- `%prob%` returns a matrix with class label specific conditional
  posterior probabilities.

## Details

If `lhs` is of class inheriting from the family of the Naive Bayes
objects and `rhs` is either dataframe or matrix then the infix operators
`%class%` and `%prob%` are equivalent to:

- `lhs %class% rhs` \<=\>
  `predict(lhs, newdata = rhs, type = "class", threshold = 0.001, eps = 0)`

- `lhs %prob% rhs` \<=\>
  `predict(lhs, newdata = rhs, type == "prob", threshold = 0.001, eps = 0)`

Compared to [`predict()`](https://rdrr.io/r/stats/predict.html), both
operators do not allow changing values of fine tuning parameters
`threshold` and `eps`.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`predict.naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.naive_bayes.md),
[`predict.bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.bernoulli_naive_bayes.md),
[`predict.multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.multinomial_naive_bayes.md),
[`predict.poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.poisson_naive_bayes.md),
[`predict.gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.gaussian_naive_bayes.md),
[`predict.nonparametric_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.nonparametric_naive_bayes.md)

## Examples

``` r
### Fit the model
nb <- naive_bayes(Species ~ ., iris)

newdata <- iris[1:5,-5] # Let's pretend

### Classification
nb %class% newdata
#> [1] setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica
predict(nb, newdata, type = "class")
#> [1] setosa setosa setosa setosa setosa
#> Levels: setosa versicolor virginica

### Posterior probabilities
nb %prob% newdata
#>      setosa   versicolor    virginica
#> [1,]      1 2.981309e-18 2.152373e-25
#> [2,]      1 3.169312e-17 6.938030e-25
#> [3,]      1 2.367113e-18 7.240956e-26
#> [4,]      1 3.069606e-17 8.690636e-25
#> [5,]      1 1.017337e-18 8.885794e-26
predict(nb, newdata, type = "prob")
#>      setosa   versicolor    virginica
#> [1,]      1 2.981309e-18 2.152373e-25
#> [2,]      1 3.169312e-17 6.938030e-25
#> [3,]      1 2.367113e-18 7.240956e-26
#> [4,]      1 3.069606e-17 8.690636e-25
#> [5,]      1 1.017337e-18 8.885794e-26

```
