# Predict Method for multinomial_naive_bayes Objects

Classification based on the Multinomial Naive Bayes model.

## Usage

``` r
# S3 method for class 'multinomial_naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"), ...)
```

## Arguments

- object:

  object of class inheriting from `"multinomial_naive_bayes"`.

- newdata:

  matrix with non-negative integer predictors (only numeric matrix is
  accepted).

- type:

  if "class", new data points are classified according to the highest
  posterior probabilities. If "prob", the posterior probabilities for
  each class are returned.

- ...:

  not used.

## Value

`predict.multinomial_naive_bayes` returns either a factor with class
labels corresponding to the maximal conditional posterior probabilities
or a matrix with class label specific conditional posterior
probabilities.

## Details

This is a specialized version of the Naive Bayes classifier, where the
features represent the frequencies with which events have been generated
by a multinomial distribution.

The Multinomial Naive Bayes is not available through the
[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
function.

The NAs in the newdata are not included into the calculation of
posterior probabilities; and if present an informative warning is given.

## References

McCallum, Andrew; Nigam, Kamal (1998). A comparison of event models for
Naive Bayes text classification (PDF). AAAI-98 workshop on learning for
text categorization. 752.
`http://www.cs.cmu.edu/~knigam/papers/multinomial-aaaiws98.pdf`

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md),
[`coef.multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/coef.md)

## Examples

``` r
### Simulate the data:
cols <- 10 ; rows <- 100
M <- matrix(sample(0:5, rows * cols,  TRUE), nrow = rows, ncol = cols)
y <- factor(sample(paste0("class", LETTERS[1:2]), rows, TRUE, prob = c(0.3,0.7)))
colnames(M) <- paste0("V", seq_len(ncol(M)))
laplace <- 1

### Train the Multinomial Naive Bayes
mnb <- multinomial_naive_bayes(x = M, y = y, laplace = laplace)

# Classification
head(predict(mnb, newdata = M, type = "class"))
#> [1] classB classB classB classB classA classB
#> Levels: classA classB
head(mnb %class% M)
#> [1] classB classB classB classB classA classB
#> Levels: classA classB

# Posterior probabilities
head(predict(mnb, newdata = M, type = "prob"))
#>          classA    classB
#> [1,] 0.17623129 0.8237687
#> [2,] 0.41834308 0.5816569
#> [3,] 0.09334622 0.9066538
#> [4,] 0.19324231 0.8067577
#> [5,] 0.56491024 0.4350898
#> [6,] 0.23376937 0.7662306
head(mnb %prob% M)
#>          classA    classB
#> [1,] 0.17623129 0.8237687
#> [2,] 0.41834308 0.5816569
#> [3,] 0.09334622 0.9066538
#> [4,] 0.19324231 0.8067577
#> [5,] 0.56491024 0.4350898
#> [6,] 0.23376937 0.7662306
```
