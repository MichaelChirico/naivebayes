# Changelog

## naivebayes 1.0.0

CRAN release: 2024-03-16

### Major Release: Maturity and Stability

The package has reached a significant milestone of maturity and
stability, leading to the version update to 1.0.0.

- Improvement: enhanced print methods.
- Improvement: updated documentation.
- Improvement: minor internal enhancements.

## naivebayes 0.9.7

CRAN release: 2020-03-08

- Improvement:
  [`multinomial_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md),
  [`bernoulli_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md),
  [`poisson_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md)
  and
  [`gaussian_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md)
  now support sparse matrices (`dgCMatrix` class from the `Matrix`
  Package).

- Improvement: updated documentation.

- Improvement: better informative errors.

## naivebayes 0.9.6

CRAN release: 2019-06-03

### Improvements:

- Enhanced documentation - this includes a new webpage:
  <https://majkamichal.github.io/naivebayes/>

- In
  [`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)
  Poisson distribution is now available to model class conditional
  probabilities of non-negative integer predictors. It is applied to all
  vectors with class “integer” via a new parameter `usepoisson = TRUE`.
  By default `usepoisson = FALSE`. All `naive_bayes` objects created
  with previous versions are fully compatible with the `0.9.6` version.

- [`predict.naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/predict.naive_bayes.md)
  has a new parameter `eps` that specifies a value of an epsilon-range
  to replace zero or close to zero probabilities by specified threshold.
  It applies to metric variables as well as to discrete variables, but
  only when `laplace = 0`.

- [`predict.naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/predict.naive_bayes.md)
  is now more efficient and reliable.

- [`print()`](https://rdrr.io/r/base/print.html) method has been
  enhanced for better readability.

- [`plot()`](https://rdrr.io/r/graphics/plot.default.html) method allows
  now visualising class marginal and class conditional distributions for
  each predictor variable via new parameter `prob` with two possible
  values: `"marginal"` or `"conditional"`.

### New functions

- [`bernoulli_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md) -
  specialised version of
  [`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
  where all features take on 0-1 values and each feature is modelled
  with the Bernoulli distribution.

- [`gaussian_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md) -
  specialised version of
  [`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
  where all features are real valued and each feature is modelled with
  the Gaussian distribution.

- [`poisson_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md) -
  specialised version of
  [`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
  where all features are non-negative integers and each feature is
  modelled with the Poisson distribution.

- [`nonparametric_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/nonparametric_naive_bayes.md) -
  specialised version of
  [`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md),
  where all features are real valued and distribution of each is
  estimated with kernel density estimation (KDE).

- [`multinomial_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md) -
  specialised Naive Bayes classifier suitable for text classification.

- `%class%` and `%prob%` - infix operators that are shorthands for
  performing classification and obtaining posterior probabilities,
  respectively.

- [`coef()`](https://rdrr.io/r/stats/coef.html) - a generic function
  which extracts model coefficients from specialized Naive Bayes
  objects.

- [`get_cond_dist()`](https://majkamichal.github.io/naivebayes/reference/get_cond_dist.md) -
  for obtaining names of class conditional distributions assigned to
  features.

## naivebayes 0.9.5

CRAN release: 2019-03-17

- Fixed: when `laplace > 0` and discrete feature with `>2` distinct
  values, the probabilities in the probability table do not sum up to 1.

## naivebayes 0.9.4

CRAN release: 2019-03-10

- Fixed:
  [`plot.naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/plot.naive_bayes.md)
  crashes when missing data present in training set (bug found by Mark
  van der Loo).

## naivebayes 0.9.3

CRAN release: 2019-01-07

- Fixed: numerical underflow in predict.naive_bayes function when the
  number of features is big (bug found by William Townes).

- Fixed: when all names of features in the `newdata` in
  [`predict.naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/predict.naive_bayes.md)
  do not match these defined in the `naive_bayes` object, then the
  calculation based on prior probabilities is done only for one row of
  `newdata`.

- Improvement: better handling (informative warnings/errors) of not
  correct inputs in
  [`predict.naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/predict.naive_bayes.md).

- Improvement: `print.naive_bayes()` is now more transparent.

## naivebayes 0.9.2

CRAN release: 2018-01-03

- Fixed: when the data have two classes and they are not alphabetically
  ordered, the predicted classes are incorrect (bug found by Max Kuhn).

## naivebayes 0.9.1

CRAN release: 2017-01-15

- Fixed: when the prediction data has one row, the column names get
  dropped (bug found by Max Kuhn).
