# Learning Econophysics — Tutorial Notebooks

Worked solutions to the tutorial exercises of ***Modelling Financial Markets: an
Introduction to Econophysics*** by **Michael Benzaquen** (course ECO 586 /
PHY 560C, École Polytechnique). The lecture notes the exercises belong to are
committed here as
[`Modelling Financial Markets - Lecture Notes.pdf`](Modelling%20Financial%20Markets%20-%20Lecture%20Notes.pdf).

These are the notebooks written to actually understand the notes: each one takes
a result stated in the text, derives it by hand in the markdown cells, then
implements it and checks the derivation against a simulation. They are the three
parts of **Tutorial 1: Time series simulation and analysis**, and they are meant
to be read in order — each builds the tools the next one uses.

All three open in Google Colab from the badge at the top of the notebook.

## The three parts

### Part 1 — `Fractional_Brownian_motion_(fBM).ipynb`

Fractional Brownian motion, introduced by Mandelbrot and van Ness: the
generalisation of Brownian motion whose increments are correlated, tuned by the
**Hurst exponent** $H$.

The construction is linear-algebraic and is derived before it is coded: if $x$
is an i.i.d. Gaussian vector of length $T$ and $L$ is a $T \times T$ matrix,
then $y = Lx$ has correlation matrix $C = LL^\top$. Building an fBM with a
prescribed covariance therefore reduces to **factorising the target covariance
matrix** and applying the factor to white noise. The notebook does exactly that,
then verifies that the simulated paths have the intended $H$.

$H = 1/2$ recovers ordinary Brownian motion; $H > 1/2$ gives persistent,
trending paths; $H < 1/2$ gives anti-persistent, mean-reverting ones.

### Part 2 — `The_Ornstein_Uhlenbeck_process.ipynb`

The Ornstein–Uhlenbeck process centred on zero: the canonical **mean-reverting**
process, and the one financial modelling reaches for whenever a quantity is
supposed to be pulled back towards a level rather than wander freely.

Implements `ornstein_uhlenbeck(x_0, omega, sigma, dt, T)`, returning one
realisation from initial condition $x_0$ with mean-reversion rate $\omega$ and
noise amplitude $\sigma$ over $T$ steps of size $\mathrm{d}t$; then studies the
stationary distribution and the autocorrelation, and checks both against the
analytic results.

### Part 3 — `Scale_invariance,_monofractality_and_multifractality.ipynb`

The part the first two exist to make possible, and the one closest to real
market data.

For an fBM of Hurst exponent $H$, the structure functions
$M_q(\tau) = \langle |x(t+\tau) - x(t)|^q \rangle_t$ can be rewritten purely as
a function of $\sigma(\tau) = \sqrt{M_2(\tau)}$, because the distribution of
increments is self-similar: $P_\tau(\Delta x)$ depends on $\Delta x$ and $\tau$
only through $\Delta x / \sigma(\tau)$. That is **monofractality** — a single
exponent, $\zeta_q = qH$, describes every moment.

The notebook derives this, measures $\zeta_q$ on simulated paths, and then
contrasts it with **multifractality**, where $\zeta_q$ is nonlinear in $q$ and a
single Hurst exponent is no longer enough — the regime that real financial time
series are actually in.

## Running the notebooks

Click the Colab badge at the top of any notebook, or run locally:

```bash
pip install numpy pandas matplotlib
jupyter lab
```

Standard scientific Python only; no data files are needed, since every series is
simulated.

## Related repository

- [`learning_statistical_learning`](https://github.com/alessiomartini/learning_statistical_learning)
  — the same learn-by-implementing approach applied to machine learning and deep
  learning.
