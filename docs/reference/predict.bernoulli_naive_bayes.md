# Predict Method for bernoulli_naive_bayes Objects

Classification based on the Bernoulli Naive Bayes model.

## Usage

``` r
# S3 method for class 'bernoulli_naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"), ...)
```

## Arguments

- object:

  object of class inheriting from `"bernoulli_naive_bayes"`.

- newdata:

  matrix with numeric 0-1 predictors.

- type:

  if "class", new data points are classified according to the highest
  posterior probabilities. If "prob", the posterior probabilities for
  each class are returned.

- ...:

  not used.

## Value

`predict.bernoulli_naive_bayes` returns either a factor with class
labels corresponding to the maximal conditional posterior probabilities
or a matrix with class label specific conditional posterior
probabilities.

## Details

This is a specialized version of the Naive Bayes classifier, in which
all features take on numeric 0-1 values and class conditional
probabilities are modelled with the Bernoulli distribution.

Class posterior probabilities are calculated using the Bayes' rule under
the assumption of independence of predictors. If no `newdata` is
provided, the data from the object is used.

The Bernoulli Naive Bayes is available in both, `naive_bayes` and
`bernoulli_naive_bayes`. The implementation of the specialized Naive
Bayes provides more efficient performance though. The speedup comes from
the restricting the data input to a numeric 0-1 matrix and performing
the linear algebra as well as vectorized operations on it. In other
words, the efficiency comes at cost of the flexibility.

The NAs in the newdata are not included into the calculation of
posterior probabilities; and if present an informative warning is given.

The `bernoulli_naive_bayes` function is equivalent to the `naive_bayes`
function with the numeric 0-1 matrix being coerced, for instance, to the
"0"-"1" character matrix.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md),
[`plot.bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/plot.bernoulli_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md)

## Examples

``` r
cols <- 10 ; rows <- 100 ; probs <- c("0" = 0.4, "1" = 0.1)
M <- matrix(sample(0:1, rows * cols,  TRUE, probs), nrow = rows, ncol = cols)
y <- factor(sample(paste0("class", LETTERS[1:2]), rows, TRUE, prob = c(0.3,0.7)))
colnames(M) <- paste0("V", seq_len(ncol(M)))
laplace <- 0.5

### Train the Bernoulli Naive Bayes
bnb <- bernoulli_naive_bayes(x = M, y = y, laplace = laplace)

### Classification
head(predict(bnb, newdata = M, type = "class"))
#> [1] classB classB classB classB classA classB
#> Levels: classA classB
head(bnb %class% M)
#> [1] classB classB classB classB classA classB
#> Levels: classA classB

### Posterior probabilities
head(predict(bnb, newdata = M, type = "prob"))
#>         classA    classB
#> [1,] 0.1178526 0.8821474
#> [2,] 0.1003894 0.8996106
#> [3,] 0.1426711 0.8573289
#> [4,] 0.4601912 0.5398088
#> [5,] 0.5246835 0.4753165
#> [6,] 0.3463304 0.6536696
head(bnb %prob% M)
#>         classA    classB
#> [1,] 0.1178526 0.8821474
#> [2,] 0.1003894 0.8996106
#> [3,] 0.1426711 0.8573289
#> [4,] 0.4601912 0.5398088
#> [5,] 0.5246835 0.4753165
#> [6,] 0.3463304 0.6536696
```
