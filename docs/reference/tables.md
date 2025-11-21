# Browse Tables of Naive Bayes Classifier

Auxiliary function for `"naive_bayes"` and `"*_naive_bayes"` objects for
easy browsing tables.

## Usage

``` r
tables(object, which = NULL)
```

## Arguments

- object:

  object of class inheriting from: `"naive_bayes"` and
  `"*_naive_bayes"`.

- which:

  tables to be showed (all by default). This can be any valid indexing
  vector or vector containing names of variables.

## Value

list with tables.

## Details

Default print method for `"naive_bayes"` and `"*_naive_bayes"` objects
shows at most five first tables. This auxiliary function `tables`
returns by default all tables and allows easy subsetting via indexing
variables.

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`bernoulli_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md),
[`multinomial_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md),
[`poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md),
[`gaussian_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md),
`tables`,
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md)

## Examples

``` r
data(iris)
nb <- naive_bayes(Species ~ ., data = iris)
tables(nb, "Sepal.Length")
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Length (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>             
#> Sepal.Length    setosa versicolor virginica
#>         mean 5.0060000  5.9360000 6.5880000
#>         sd   0.3524897  0.5161711 0.6358796
#> 
#> --------------------------------------------------------------------------------
tables(nb, c("Sepal.Length", "Sepal.Width"))
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Length (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>             
#> Sepal.Length    setosa versicolor virginica
#>         mean 5.0060000  5.9360000 6.5880000
#>         sd   0.3524897  0.5161711 0.6358796
#> 
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Width (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>            
#> Sepal.Width    setosa versicolor virginica
#>        mean 3.4280000  2.7700000 2.9740000
#>        sd   0.3790644  0.3137983 0.3224966
#> 
#> --------------------------------------------------------------------------------
tabs <- tables(nb, 1:2)
tabs
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Length (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>             
#> Sepal.Length    setosa versicolor virginica
#>         mean 5.0060000  5.9360000 6.5880000
#>         sd   0.3524897  0.5161711 0.6358796
#> 
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Width (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>            
#> Sepal.Width    setosa versicolor virginica
#>        mean 3.4280000  2.7700000 2.9740000
#>        sd   0.3790644  0.3137983 0.3224966
#> 
#> --------------------------------------------------------------------------------
tabs[1]
#> -------------------------------------------------------------------------------- 
#> :: Sepal.Length (Gaussian) 
#> -------------------------------------------------------------------------------- 
#>             
#> Sepal.Length    setosa versicolor virginica
#>         mean 5.0060000  5.9360000 6.5880000
#>         sd   0.3524897  0.5161711 0.6358796
#> 
#> --------------------------------------------------------------------------------
```
