# Plot Method for poisson_naive_bayes Objects

Plot method for objects of class `"poisson_naive_bayes"` designed for a
quick look at the class marginal or class conditional Poisson
distributions of non-negative integer predictors.

## Usage

``` r
# S3 method for class 'poisson_naive_bayes'
plot(x, which = NULL, ask = FALSE, legend = TRUE,
  legend.box = FALSE, arg.num = list(),
  prob = c("marginal", "conditional"), ...)
```

## Arguments

- x:

  object of class inheriting from `"poisson_naive_bayes"`.

- which:

  variables to be plotted (all by default). This can be any valid
  indexing vector or vector containing names of variables.

- ask:

  logical; if `TRUE`, the user is asked before each plot, see
  [`par`](https://rdrr.io/r/graphics/par.html)`(ask=.)`.

- legend:

  logical; if `TRUE` a
  [`legend`](https://rdrr.io/r/graphics/legend.html) will be be plotted.

- legend.box:

  logical; if `TRUE` a box will be drawn around the legend.

- arg.num:

  other parameters to be passed as a named list to
  [`matplot`](https://rdrr.io/r/graphics/matplot.html).

- prob:

  character; if "marginal" then marginal distributions of predictor
  variables for each class are visualised and if "conditional" then the
  class conditional distributions of predictor variables are depicted.
  By default, prob="marginal".

- ...:

  not used.

## Details

Class marginal or class conditional Poisson distributions are visualised
by [`matplot`](https://rdrr.io/r/graphics/matplot.html).

The parameter `prob` controls the kind of probabilities to be visualized
for each individual predictor \\Xi\\. It can take on two values:

- "marginal": \\P(Xi\|class) \* P(class)\\

- "conditional": \\P(Xi\|class)\\

## Author

Michal Majka, <michalmajka@hotmail.com>

## See also

[`naive_bayes`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
[`poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md),
[`predict.poisson_naive_bayes`](https://majkamichal.github.io/naivebayes/reference/predict.poisson_naive_bayes.md),
[`tables`](https://majkamichal.github.io/naivebayes/reference/tables.md),
[`get_cond_dist`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md)

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

# Visualize class conditional Poisson distributions corresponding
# to the first feature
plot(pnb, which = 1, prob = "conditional")


# Visualize class marginal Poisson distributions corresponding
# to the first feature
plot(pnb, which = 1)
```
