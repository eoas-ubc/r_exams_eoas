
```{code-cell} ipython3
%%R
library(reticulate)
```

```{code-cell} ipython3
:name: data generation
:tags: [remove_input, remove_output]

import random
dat= [["lm","least-squares regression"], ["glm", "Poisson regression"], ["glm.nb","negative binomial regression"], ["model.matrix","extracting the regressor matrix from a fitted (generalized) linear model object"],["coef","extracting the estimated coefficients from a fitted (generalized) linear model object"],["vcov","extracting the estimated covariance matrix from a fitted (generalized) linear model object"],["logLik","extracting the fitted log-likelihood from a fitted (generalized) linear model object"]]

i = random.sample(range(7),1)[0]
fun = dat[i][0]
descr = dat[i][1]
```

Question
========
What is the name of the R function for `r py$descr`?

Solution
========
``r py$fun`` is the R function for `r py$descr`.
Use ? for the corresponding manual page.

Meta-information
================
extype: string
exsolution: `r py$fun`
exname: R functions
