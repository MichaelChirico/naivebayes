# Obtain names of class conditional distribution assigned to features

Auxiliary function for `"naive_bayes"`, `"*_naive_bayes"` and
`"naive_bayes_tables"` objects for obtaining names of class conditional
distributions assigned to the features.

## Usage

``` r
get_cond_dist(object)
```

## Arguments

- object:

  object of class inheriting from `"naive_bayes"` or `"*_naive_bayes"`
  or `"naive_bayes_tables"`.

## Value

vector with names of class conditional distributions assigned to the
features.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md),
[`multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md),
[`poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md),
[`gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md)

## Examples

``` r
data(iris)
nb <- naive_bayes(Species ~ ., data = iris)
get_cond_dist(nb) # <=> attr(nb$tables, "cond_dist")
#> Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
#>   "Gaussian"   "Gaussian"   "Gaussian"   "Gaussian" 
get_cond_dist(tables(nb))
#> Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
#>   "Gaussian"   "Gaussian"   "Gaussian"   "Gaussian" 
```
