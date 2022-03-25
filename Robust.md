---
name: Robust
topic: Robust Statistical Methods
maintainer: Martin Maechler
email: Martin.Maechler@R-project.org
version: 2022-03-24
source: https://github.com/cran-task-views/Robust/
---


Robust (or "resistant") methods for statistics modelling have been
available in S from the very beginning in the 1980s; and then in R in
package `stats`. Examples are `median()`, `mean(*, trim =. )`, `mad()`,
`IQR()`, or also `fivenum()`, the statistic behind `boxplot()` in
package `graphics`) or `lowess()` (and `loess()`) for robust
nonparametric regression, which had been complemented by `runmed()` in
2003. Much further important functionality has been made available in
recommended (and hence present in all R versions) package
`r pkg("MASS", priority = "core")` (by Bill Venables and
Brian Ripley, see *the* book [Modern Applied Statistics with
S](https://www.stats.ox.ac.uk/pub/MASS4/)). Most importantly, they
provide `rlm()` for robust regression and `cov.rob()` for robust
multivariate scatter and covariance.

This task view is about R add-on packages providing newer or faster,
more efficient algorithms and notably for (robustification of) new
models.

Please send suggestions for additions and extensions via e-mail to the
maintainer or submit an issue or pull request in the GitHub
repository linked above.

An international group of scientists working in the field of robust
statistics has made efforts (since October 2005) to coordinate several
of the scattered developments and make the important ones available
through a set of R packages complementing each other. These should build
on a basic package with "Essentials", coined
`r pkg("robustbase", priority = "core")` with (potentially
many) other packages building on top and extending the essential
functionality to particular models or applications. Since 2020 and the
2nd edition of [*Robust Statistics: Theory and
Methods*](https://www.wiley.com/go/maronna/robust) ,
`r pkg("RobStatTM")` covers its estimators and examples,
notably by importing from `r pkg("robustbase")` and
`r pkg("rrcov", priority = "core")`. Further, there is the
quite comprehensive package
`r pkg("robust", priority = "core")`, a version of the robust
library of S-PLUS, as an R package now GPLicensed thanks to Insightful
and Kjell Konis. Originally, there has been much overlap between
`r pkg("robustbase")` and `r pkg("robust")`, now `r pkg("robust")`
*depends* on `r pkg("robustbase")` and
`r pkg("rrcov")`, where `r pkg("robust")` provides convenient
routines for the casual user while `r pkg("robustbase")` and
`r pkg("rrcov")` contain the underlying functionality, and
provide the more advanced statistician with a large range of options for
robust modeling.

We structure the packages roughly into the following topics, and
typically will first mention functionality in packages
`r pkg("robustbase")`, `r pkg("rrcov")` and
`r pkg("robust")`.

### Regression

-   ***Linear** Regression:*  
    `lmrob()` (`r pkg("robustbase")`) and `lmRob()`
    (`r pkg("robust")`) where the former uses the latest of
    the fast-S algorithms and heteroscedasticity and autocorrelation
    corrected (HAC) standard errors, the latter makes use of the M-S
    algorithm of Maronna and Yohai (2000), automatically when there are
    factors among the predictors (where S-estimators (and hence
    MM-estimators) based on resampling typically badly fail). The
    `ltsReg()` and `lmrob.S()` functions are available in
    `r pkg("robustbase")`, but rather for comparison
    purposes. `rlm()` from `r pkg("MASS")` had been the
    first widely available implementation for robust linear models, and
    also one of the very first MM-estimation implementations.
    `r pkg("robustreg")` provides very simple M-estimates
    for linear regression (in pure R). Note that Koenker's quantile
    regression package `r pkg("quantreg")` contains L1 (aka
    LAD, least absolute deviations)-regression as a special case, doing
    so also for nonparametric regression via splines. Package
    `r pkg("mblm")`'s function `mblm()` fits median-based
    (Theil-Sen or Siegel's repeated) simple linear models.
-   ***Generalized** Linear Models ( **GLM** s) for Regression:*  
    GLMs are provided both via `glmrob()`
    (`r pkg("robustbase")`) and `glmRob()`
    (`r pkg("robust")`). Robust ordinal regression is
    provided by `r pkg("rorutadis")` (UTADIS).
    `r pkg("drgee")` fits "Doubly Robust" Generalized
    Estimating Equations (GEEs), `r pkg("complmrob")` does
    robust linear regression with compositional data as covariates.
    `r pkg("multinomRob")` fits overdispersed multinomial
    regression models for count data.
-   ***Mixed-Effects** (Linear and Nonlinear) Regression:*  
    Quantile regression (and hence L1 or LAD) for mixed effect models,
    is available in package `r pkg("lqmm")`. Rank-based
    mixed effect fitting from package `r pkg("rlme")`,
    whereas an *MM-like* approach for robust linear **mixed effects**
    modeling is available from package `r pkg("robustlmm")`.
    More recently, `r pkg("skewlmm")` provides robust linear
    mixed-effects models **LMM** via scale mixtures of skew-normal
    distributions.
-   ***Nonlinear / Smooth** (Nonparametric Function) Regression:*  
    Robust Nonlinear model fitting is available through
    `r pkg("robustbase")`'s `nlrob()`.
    `r pkg("robustgam")` fits robust GAMs, i.e., robust
    Generalized Additive Models.

### Multivariate Analysis:

-   Here, the `r pkg("rrcov")` package which builds (`Depends`)
    on `r pkg("robustbase")` provides nice S4
    class based methods, more methods for robust multivariate
    variance-covariance estimation, and adds robust PCA methodology.
-   `r pkg("rrcov")` is extended by `r pkg("rrcovNA")`, providing
    robust multivariate methods for *for incomplete* or missing (`NA`)
    data, and by `r pkg("rrcovHD")`, providing robust
    multivariate methods for *High Dimensional* data.
-   Specialized robust PCA packages are `r pkg("pcaPP")`
    (via Projection Pursuit), `r pkg("rpca")` (incl
    "sparse") and `r pkg("rospca")`. Historically, note
    that robust PCA can be performed by using standard R's
    `princomp()`, e.g.,
    `X <- stackloss; pc.rob <- princomp(X, covmat= MASS::cov.rob(X))`
-   Here, `r pkg("robustbase")` contains a slightly more
    flexible version, `covMcd()` than `r pkg("robust")`'s
    `fastmcd()`, and similarly for `covOGK()`. On the other hand,
    `r pkg("robust")`'s `covRob()` has automatically
    chosen methods, notably `pairwiseQC()` for large dimensionality p.
    Package `r pkg("robustX")` for experimental, or other
    not yet established procedures, contains `BACON()` and `covNCC()`,
    the latter providing the neighbor variance estimation (NNVE) method
    of Wang and Raftery (2002), also available (slightly less optimized)
    in `r pkg("covRobust")`.
-   `r pkg("RobRSVD")` provides a robust Regularized
    Singular Value Decomposition.
-   `r pkg("mvoutlier")` (building on
    `r pkg("robustbase")`) provides several methods for
    outlier identification in high dimensions.
-   `r pkg("GSE")` estimates multivariate location and
    scatter in the presence of missing data.
-   `r pkg("RSKC")` provides **R**obust **S**parse **K**-means
    **C**lustering.
-   `r pkg("robustDA")` for *robust mixture Discriminant
    Analysis* (RMDA) builds a mixture model classifier with noisy class
    labels.
-   `r pkg("robcor")` computes robust pairwise correlations
    based on scale estimates, particularly on `FastQn()`.
-   `r pkg("covRobust")` provides the nearest neighbor
    variance estimation (NNVE) method of Wang and Raftery (2002).

### Clustering (Multivariate):

-   We are *not* considering cluster-resistant variance (/standard
    error) estimation (aka "sandwich"). Rather e.g. model based and
    hierarchical clustering methodology with a particular emphasis on
    robustness: Note that `r pkg("cluster")`'s `pam()`
    implementing "partioning around medians" is partly robust (medians
    instead of very unrobust k-means) but is *not* good enough, as e.g.,
    the k clusters could consist of k-1 outliers one cluster for the
    bulk of the remaining data.
-   "Truly" robust clustering is provided by packages
    `r pkg("genie")`, `r pkg("Gmedian")`,
    `r pkg("otrimle")` (trimmed MLE model-based) and notably
    `r pkg("tclust")` (robust trimmed clustering).
-   See also the `r view("Cluster")` CRAN task view.

### Large Data Sets:

-   `BACON()` (in `r pkg("robustX")`) should be applicable
    for larger (n,p) than traditional robust covariance based outlier
    detectors.
-   `r pkg("OutlierDM")` detects outliers for replicated
    high-throughput data. (See also the CRAN task view
    `r view("MachineLearning")`.)

### Descriptive Statistics / Exploratory Data Analysis:

-   `boxplot.stats()`, etc mentioned above

### Time Series:

-   R's `runmed()` provides *most robust* running median filtering.
-   Package `r pkg("robfilter")` contains robust regression
    and filtering methods for univariate time series, typically based on
    repeated (weighted) median regressions.
-   The `r pkg("RobPer")` provides several methods for
    robust periodogram estimation, notably for irregularly spaced time
    series.
-   Peter Ruckdeschel has started to lead an effort for a robust
    time-series package, see `r rforge("robust-ts")` on
    R-Forge.
-   Further, robKalman, *"Routines for Robust Kalman Filtering --
    the ACM- and rLS-filter"* , is being developed, see
    `r rforge("robkalman")` on R-Forge.

### Econometric Models:

-   Econometricians tend to like HAC (heteroscedasticity and
    autocorrelation corrected) standard errors. For a broad class of
    models, these are provided by package
    `r pkg("sandwich")`; similarly
    `r pkg("clubSandwich")` and
    `r pkg("clusterSEs")`. Note that `vcov(lmrob())` also
    uses a version of HAC standard errors for its robustly estimated
    linear models. See also the CRAN task view
    `r view("Econometrics")`

### Robust Methods for Bioinformatics:

-   There are several packages in the [Bioconductor
    project](https://www.bioconductor.org/) providing specialized robust
    methods. In addition, `r pkg("RobLoxBioC")` provides
    infinitesimally robust estimators for preprocessing omics data.

### Robust Methods for Survival Analysis:

-   Package `r pkg("coxrobust")` provides robust estimation
    in the Cox model.

### Robust Methods for Surveys:

-   Package `r pkg("robsurvey")` provides robust survey regression estimation
    and the robust Horvitz-Thompson estimator.

### Geostatistics:

-   Package `r pkg("georob")` aims at robust geostatistical
    analysis of spatial data, such as kriging and more.

### Collections of **Several** Methodologies:

-   `r pkg("WRS2")` contains robust tests for ANOVA and
    ANCOVA and other functionality from Rand Wilcox's collection.
-   `r pkg("walrus")` builds on `r pkg("WRS2")`'s computations,
    providing a different user interface.
-   `r pkg("robeth")` contains R functions interfacing to
    the extensive RobETH fortran library with many functions for
    regression, multivariate estimation and more.

### Other Approaches to Robust and Resistant Methodology:

-   The package `r pkg("distr")` and its several child
    packages also allow to explore robust estimation concepts, see e.g.,
    `r rforge("distr")` on R-Forge.
-   Notably, based on these, the project
    `r rforge("robast")` aims for the implementation of R
    packages for the computation of optimally robust estimators and
    tests as well as the necessary infrastructure (mainly S4 classes and
    methods) and diagnostics; cf. M. Kohl (2005). It includes the R
    packages `r pkg("RandVar")`,
    `r pkg("RobAStBase")`, `r pkg("RobLox")`,
    `r pkg("RobLoxBioC")`, `r pkg("RobRex")`.
    Further, `r pkg("ROptEst")`, and
    `r pkg("ROptRegTS")`.
-   `r pkg("RobustAFT")` computes Robust Accelerated Failure
    Time Regression for Gaussian and logWeibull errors.
-   `r pkg("robumeta")` for robust variance meta-regression;
    `r pkg("metaplus")` adds robustness via t- or mixtures
    of normal distributions.
-   `r pkg("ssmrob")` provides robust estimation and
    inference in sample selection models.



### Links
-   [Mailing list: R Special Interest Group on Robust Statistics](https://stat.ethz.ch/mailman/listinfo/r-sig-robust/)
-   [Robust Statistics in R (TU Vienna)](http://cstat.tuwien.ac.at/rsr/)
