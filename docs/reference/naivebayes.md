# naivebayes

The **naivebayes** package presents an efficient implementation of the
widely-used Naive Bayes classifier. It upholds three core principles:
efficiency, user-friendliness, and reliance solely on Base R. By
adhering to the latter principle, the package ensures stability and
reliability without introducing external dependencies. This design
choice maintains efficiency by leveraging the optimized routines
inherent in Base R, many of which are programmed in high-performance
languages like C/C++ or FORTRAN. By following these principles, the
naivebayes package provides a reliable and efficient tool for Naive
Bayes classification tasks, ensuring that users can perform their
analyses effectively and with ease, even in the presence of missing
data.

## Details

The general
**[`naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/naive_bayes.md)**
function is designed to determine the class of each feature in a
dataset, and depending on user specifications, it can assume various
distributions for each feature. It currently supports the following
class conditional distributions:

- Categorical distribution for discrete features (with Bernoulli
  distribution as a special case for binary outcomes)

- Poisson distribution for non-negative integer features

- Gaussian distribution for continuous features

- non-parametrically estimated densities via Kernel Density Estimation
  for continuous features

In addition to the general Naive Bayes function, the package provides
specialized functions for various types of Naive Bayes classifiers. The
specialized functions are carefully optimized for efficiency, utilizing
linear algebra operations to excel when handling dense matrices.
Additionally, they can also exploit sparsity of matrices for enhanced
performance:

- Bernoulli Naiive Bayes via
  **[`bernoulli_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/bernoulli_naive_bayes.md)**

- Multinomial Naive Bayes via
  **[`multinomial_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/multinomial_naive_bayes.md)**

- Poisson Naive Bayes via
  **[`poisson_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/poisson_naive_bayes.md)**

- Gaussian Naive Bayes via
  **[`gaussian_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/gaussian_naive_bayes.md)**

- Non-Parametric Naive Bayes via
  **[`nonparametric_naive_bayes()`](https://majkamichal.github.io/naivebayes/reference/nonparametric_naive_bayes.md)**

These specialized classifiers are tailored to different assumptions
about the underlying data distributions, offering users versatile tools
for classification tasks. Moreover, the package incorporates various
helper functions aimed at enhancing the user experience. Notably, the
model fitting functions provided by the package can effectively handle
missing data, ensuring that users can utilize the classifiers even in
the presence of incomplete information.

**Extended documentation can be found on the website:**

- <https://majkamichal.github.io/naivebayes/>

**Bug reports:**

- <https://github.com/majkamichal/naivebayes/issues>

**Contact:**

- <michalmajka@hotmail.com>
