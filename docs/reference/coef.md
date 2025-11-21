# Extract Model Coefficients

`coef` is a generic function which extracts model coefficients from
specialized Naive Bayes objects.

## Usage

``` r
# S3 method for class 'bernoulli_naive_bayes'
coef(object, ...)

# S3 method for class 'multinomial_naive_bayes'
coef(object, ...)

# S3 method for class 'poisson_naive_bayes'
coef(object, ...)

# S3 method for class 'gaussian_naive_bayes'
coef(object, ...)
```

## Arguments

- object:

  object of class inheriting from `"*_naive_bayes"`.

- ...:

  not used.

## Value

Coefficients extracted from the specialised Naive Bayes objects in form
of a data frame.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md),
[`multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md),
[`poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md),
[`gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md)

## Examples

``` r
data(iris)
y <- iris[[5]]
M <- as.matrix(iris[-5])

### Train the Gaussian Naive Bayes
gnb <- gaussian_naive_bayes(x = M, y = y)

### Extract coefficients
coef(gnb)
#>              setosa:mu setosa:sd versicolor:mu versicolor:sd virginica:mu
#> Sepal.Length     5.006 0.3524897         5.936     0.5161711        6.588
#> Sepal.Width      3.428 0.3790644         2.770     0.3137983        2.974
#> Petal.Length     1.462 0.1736640         4.260     0.4699110        5.552
#> Petal.Width      0.246 0.1053856         1.326     0.1977527        2.026
#>              virginica:sd
#> Sepal.Length    0.6358796
#> Sepal.Width     0.3224966
#> Petal.Length    0.5518947
#> Petal.Width     0.2746501

coef(gnb)[c(TRUE,FALSE)] # only means
#>              setosa:mu versicolor:mu virginica:mu
#> Sepal.Length     5.006         5.936        6.588
#> Sepal.Width      3.428         2.770        2.974
#> Petal.Length     1.462         4.260        5.552
#> Petal.Width      0.246         1.326        2.026

coef(gnb)[c(FALSE,TRUE)] # only standard deviations
#>              setosa:sd versicolor:sd virginica:sd
#> Sepal.Length 0.3524897     0.5161711    0.6358796
#> Sepal.Width  0.3790644     0.3137983    0.3224966
#> Petal.Length 0.1736640     0.4699110    0.5518947
#> Petal.Width  0.1053856     0.1977527    0.2746501
```
