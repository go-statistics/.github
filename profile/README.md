<p align="center"><img src="https://raw.githubusercontent.com/go-statistics/brand/main/social/go-statistics.png" alt="go-statistics" width="720"></p>

# go-statistics

🌐 **[Website](https://go-statistics.github.io)** · 📚 **[Documentation](https://go-statistics.github.io/docs/)**

**Probability distributions, descriptive statistics and statistical tests in pure Go (CGO=0), on go-ndarray.**

32 univariate distributions (24 continuous, 8 discrete) and 3 multivariate
ones, each with the methods of SciPy's frozen distributions — pdf, logpdf, cdf,
logcdf, sf, logsf, ppf, isf, moments, entropy, interval, support, random
draws and fits. Every distribution function is measured in ULPs against
[mpmath](https://mpmath.org), with SciPy measured on the same points: over
1479 regions the error is at or below SciPy's in 1473, and the six exceptions
are under 4.5 ulp ([docs/accuracy.md](https://github.com/go-statistics/stats/blob/main/docs/accuracy.md)).
For the same seed, the draws of 17 distributions, Dirichlet and multinomial
are bit-identical to SciPy's; the means, variances, the 13 quantile methods
and the histograms are NumPy's bit for bit.

```go
n := stats.Normal{Loc: 0, Scale: 1}
n.PDF(1.5)    // 0.12951759566589172
n.LogCDF(-40) // -804.6084420137538
n.PPF(0.975)  // 1.9599639845400538

// the same 1000 draws as scipy.stats.norm.rvs(10, 2, size=1000,
// random_state=np.random.default_rng(42)), to the bit
x, _ := stats.Normal{Loc: 10, Scale: 2}.Rvs(random.DefaultRNG(42), 1000)

r, _ := stats.TTestInd(a, b, &stats.TTestIndOptions{Welch: true})
qs, _ := stats.Percentiles(x, []float64{25, 50, 75}, nil)
```

## Repositories

| Repo | What it is |
|------|------------|
| [**stats**](https://github.com/go-statistics/stats) | 24 continuous, 8 discrete and 3 multivariate distributions; descriptive statistics (NumPy's 13 quantile methods, weights, histograms, trimmed and binned statistics); hypothesis tests from t-tests and contingency tables to Kolmogorov–Smirnov, Shapiro–Wilk and Anderson–Darling; correlations and linear regression; Gaussian KDE and the bootstrap |
| [**docs**](https://github.com/go-statistics/docs) | the documentation site (Hugo + Hextra), served at [/docs/](https://go-statistics.github.io/docs/) |
| [**go-statistics.github.io**](https://github.com/go-statistics/go-statistics.github.io) | the landing page (Hugo) |
| [**brand**](https://github.com/go-statistics/brand) | logo, icons and social images |

`stats` needs Go 1.27.2 or later, and its accuracy budgets are enforced on
amd64, arm64, 386, arm, riscv64, loong64, ppc64le and s390x. It is part of an
ecosystem with [go-ndarray](https://github.com/go-ndarray/ndarray)
(N-dimensional arrays and NumPy's random generator),
[go-numerics](https://github.com/go-numerics) (the special functions and
optimisers underneath), [go-plot](https://github.com/go-plot/plot) (figures),
[go-dataframe](https://github.com/go-dataframe/dataframe) (labelled tables)
and [go-notebook](https://github.com/go-notebook/notebook) (Go notebooks).
