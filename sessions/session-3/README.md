# Session 3: Epydemix Python Package & R Interface

Hands-on tutorials covering epidemic model design, simulation, interventions, and calibration using Epydemix in both Python and R.

## Prerequisites

Before starting, make sure you have Epydemix installed:

**Python:**
- [Python Setup (Anaconda)](../../installation/python-setup.md)
- [Using Epydemix in Python](../../installation/epydemix-in-python.md)

**R:**
- [R & RStudio Setup](../../installation/r-setup.md)
- [Using Epydemix in R](../../installation/epydemix-in-r.md)

Alternatively, run the notebooks directly in **Google Colab** (no local installation required)—click the Colab badge at the top of each notebook.

---

## Available Formats

Each tutorial is available in three formats:

| Format | Location | Best For |
|--------|----------|----------|
| **Python Jupyter** | [`python/`](python/) | Python users, Colab |
| **R Jupyter (Colab)** | [`r-colab/`](r-colab/) | R users on Google Colab (uses `rpy2` + `%%R` magic) |
| **R Markdown** | [`r-local/`](r-local/) | R users with local RStudio (uses `reticulate`) |

---

## Tutorial 1: Epidemic Modeling with Epydemix

| Format | File |
|--------|------|
| Python | [python/01_modeling_tutorial.ipynb](python/01_modeling_tutorial.ipynb) |
| R (Colab) | [r-colab/01_modeling_tutorial.ipynb](r-colab/01_modeling_tutorial.ipynb) |
| R (Local) | [r-local/01_modeling_tutorial.Rmd](r-local/01_modeling_tutorial.Rmd) |

Build age-structured epidemic models, run simulations with real population data, and compare intervention scenarios.

### Topics Covered

| Section | What You'll Learn |
|---------|-------------------|
| **1. Building an SEIR Model** | Define compartments (S, E, I, R), add mediated and spontaneous transitions, set parameters |
| **2. Loading Population Data** | Import demographics and contact matrices for 400+ geographies |
| **3. Running Simulations** | Execute stochastic chain-binomial simulations, visualize compartments and trajectories |
| **4. Modeling Interventions** | Use `add_intervention` (contact reduction) and `override_parameter` (transmission changes) |
| **5. Vaccination Campaigns** | Add a vaccination compartment (S→SV) with spontaneous transition, model vaccine effectiveness |

### Key Concepts

- **Mediated transitions**: Depend on contact with another compartment (e.g., S→E requires contact with I)
- **Spontaneous transitions**: Happen at a fixed rate (e.g., E→I, I→R)
- **Contact matrices**: Age-stratified contact rates by setting (home, school, work, community)
- **Spectral radius**: Largest eigenvalue of contact matrix, proportional to R₀

---

## Tutorial 2: Model Calibration with Epydemix

| Format | File |
|--------|------|
| Python | [python/02_calibration_tutorial.ipynb](python/02_calibration_tutorial.ipynb) |
| R (Colab) | [r-colab/02_calibration_tutorial.ipynb](r-colab/02_calibration_tutorial.ipynb) |
| R (Local) | [r-local/02_calibration_tutorial.Rmd](r-local/02_calibration_tutorial.Rmd) |

Calibrate epidemic models to observed data using Approximate Bayesian Computation (ABC) methods.

### Topics Covered

| Section | What You'll Learn |
|---------|-------------------|
| **1. Loading Data** | Import and visualize incidence time series |
| **2. Setting Up the Model** | Configure initial conditions and simulation parameters |
| **3. Defining Priors** | Specify prior distributions using `scipy.stats` |
| **4. Running Calibration** | Compare ABC-SMC, ABC Rejection, and Top X% strategies |
| **5. Comparing Results** | Visualize posterior distributions and calibration fits |
| **6. Running Projections** | Generate forecasts with uncertainty quantification |

### Calibration Methods

| Method | Description | When to Use |
|--------|-------------|-------------|
| **ABC-SMC** | Sequential Monte Carlo with adaptive tolerance | Most accurate, recommended for final results |
| **ABC Rejection** | Simple accept/reject with fixed tolerance | Fast exploratory analysis |
| **Top X%** | Keep best fraction of simulations | Fixed runtime, good for prototyping |

### Key Concepts

- **Prior distributions**: Encode beliefs about parameters before seeing data
- **Posterior distributions**: Updated beliefs after calibration
- **Distance function**: Measures fit between simulated and observed data (e.g., RMSE)
- **Projections**: Forward simulations using calibrated parameter samples

---

## Data Files

- [data/incidence_data.csv](data/incidence_data.csv) — Synthetic incidence data used in Tutorial 2

---

## Resources

- [Epydemix Documentation](https://epydemix.readthedocs.io/)
- [Supported Geographies](https://github.com/epistorm/epydemix-data/blob/main/locations.csv)
- [Full Tutorial Series](https://github.com/epistorm/epydemix/tree/main/tutorials)
- [ABC Methods Reference (Minter et al., 2019)](https://www.sciencedirect.com/science/article/pii/S175543651930026X)

---

## Next Steps

After completing these tutorials, proceed to [Session 4: Exercises](../session-4/) to practice independently.
