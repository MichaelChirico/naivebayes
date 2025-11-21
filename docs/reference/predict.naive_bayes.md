# Predict Method for naive_bayes Objects

Classification based on Naive Bayes models.

## Usage

``` r
# S3 method for class 'naive_bayes'
predict(object, newdata = NULL, type = c("class","prob"),
  threshold = 0.001, eps = 0, ...)
```

## Arguments

- object:

  object of class inheriting from `"naive_bayes"`.

- newdata:

  matrix or dataframe with categorical (character/factor/logical) or
  metric (numeric) predictors.

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

`predict.naive_bayes` returns either a factor with class labels
corresponding to the maximal conditional posterior probabilities or a
matrix with class label specific conditional posterior probabilities.

## Details

Computes conditional posterior probabilities for each class label using
the Bayes' rule under the assumption of independence of predictors. If
no new data is provided, the data from the object is used. Logical
variables are treated as categorical (binary) variables. Predictors with
missing values are not included into the computation of posterior
probabilities.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`plot.naive_bayes`](https://majkamichal.github.io/naivebayes/reference/plot.naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md),
[`%class%`](https://majkamichal.github.io/naivebayes/reference/infix_class_prob.md)

## Examples

``` r
### Simulate example data
n <- 100
set.seed(1)
data <- data.frame(class = sample(c("classA", "classB"), n, TRUE),
                   bern = sample(LETTERS[1:2], n, TRUE),
                   cat  = sample(letters[1:3], n, TRUE),
                   logical = sample(c(TRUE,FALSE), n, TRUE),
                   norm = rnorm(n),
                   count = rpois(n, lambda = c(5,15)))
train <- data[1:95, ]
test <- data[96:100, -1]

### Fit the model with default settings
nb <- naive_bayes(class ~ ., train)

# Classification
predict(nb, test, type = "class")
#> [1] classA classB classA classA classA
#> Levels: classA classB
nb %class% test
#> [1] classA classB classA classA classA
#> Levels: classA classB

# Posterior probabilities
predict(nb, test, type = "prob")
#>         classA    classB
#> [1,] 0.7174638 0.2825362
#> [2,] 0.2599418 0.7400582
#> [3,] 0.6341795 0.3658205
#> [4,] 0.5365311 0.4634689
#> [5,] 0.7186026 0.2813974
nb %prob% test
#>         classA    classB
#> [1,] 0.7174638 0.2825362
#> [2,] 0.2599418 0.7400582
#> [3,] 0.6341795 0.3658205
#> [4,] 0.5365311 0.4634689
#> [5,] 0.7186026 0.2813974


if (FALSE) { # \dontrun{
vars <- 10
rows <- 1000000
y <- sample(c("a", "b"), rows, TRUE)

# Only categorical variables
X1 <- as.data.frame(matrix(sample(letters[5:9], vars * rows, TRUE),
                           ncol = vars))
nb_cat <- naive_bayes(x = X1, y = y)
nb_cat
system.time(pred2 <- predict(nb_cat, X1))
} # }
```
