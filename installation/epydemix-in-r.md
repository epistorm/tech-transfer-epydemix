
# Using **epydemix** in an R session

This guide assumes you have R and RStudio installed. If not, see [r-setup.md](r-setup.md) first.

The R package [**reticulate**](https://rstudio.github.io/reticulate) offers an
easy way to use the **epydemix** package in R, since it allows to import Python
modules within an R session, automatically handling the conversion between
Python and R data types.

## Installing the **reticulate** package

To install the **reticulate** package from CRAN use the following statement:

```r
install.packages("reticulate")
```

## Importing the **epydemix** package in R

Once **reticulate** is installed, one can load this package with
`library(reticulate)`, and then import **epydemix**. The recommended way is by
calling `py_require()`, which allows to declare Python requirements for an R
session, followed by the `import()` statement.

**Reticulate** will automatically create and use an ephemeral Python
environment that satisfies the requirements, downloading and installing the
**epydemix** package and its dependencies if not already installed.

Essentially, one needs to do the following:

```r
library(reticulate)
py_require("epydemix")
epydemix <- import("epydemix")
```

It is then possible to call functions and access other objects defined in
**epydemix** by using the `$` operator:

```r
library(reticulate)
py_require("epydemix")
epydemix <- import("epydemix")

# A simple SIR model
sir_model <- epydemix$EpiModel(
    name="SIR Model", 
    compartments=list("S", "I", "R")
)

sir_model$add_transition(source = "S", target = "I", params = list(0.3, "I"), kind = "mediated")
sir_model$add_transition(source = "I", target = "R", params = 0.1, kind = "spontaneous")
```

## Common patterns when using epydemix in R

Below are the main tricks and tools used in the workshop tutorials.

### Python tuples

Some epydemix functions expect Python tuples (e.g., mediated transition
parameters). Use `import_builtins()` to access the Python `tuple()` constructor:

```r
builtins <- import_builtins()
params_SE <- builtins$tuple(list("beta", "I"))
model$add_transition("S", "E", params = params_SE, kind = "mediated")
```

### Python dictionaries

Use `reticulate::dict()` to create Python dictionaries (e.g., for initial
conditions):

```r
initial_conditions <- reticulate::dict(
  Susceptible = susceptible,
  Infected = infected,
  Recovered = recovered
)
```

### Importing submodules

Import specific submodules with `import()`:

```r
viz <- import("epydemix.visualization")
plot_quantiles <- viz$plot_quantiles

scipy_stats <- import("scipy.stats")
prior <- scipy_stats$uniform(loc = 0.01, scale = 0.02)
```

### Defining Python callback functions

Some components (e.g., `ABCSampler`) require a Python-callable function. Use
`py_run_string()` to define it in Python, then retrieve it:

```r
py_run_string("
from epydemix import simulate

def simulate_wrapper(parameters):
    results = simulate(**parameters)
    return {'data': results.transitions['Susceptible_to_Infected_total']}
")

simulate_wrapper <- py$simulate_wrapper
```

### Converting Python objects to R

Use `py_to_r()` to convert Python objects (NumPy arrays, pandas DataFrames) into
R vectors or data frames:

```r
Nk_r <- py_to_r(model$population$Nk)

# For pandas DataFrames returned by epydemix
df <- py_to_r(results$get_calibration_quantiles(dates = simulation_dates))
df$date <- as.Date(df$date)
```

### Displaying matplotlib plots

Epydemix's built-in visualization functions return matplotlib axes objects. In
RStudio, these plots are not displayed automatically—you need to call
`plt$show()` explicitly:

```r
plt <- import("matplotlib.pyplot")

# After any epydemix plot call
plot_quantiles(df_quantiles, columns = "data", title = "My Plot")
plt$show()
```

This applies to all epydemix visualization functions (`plot_quantiles`,
`plot_posterior_distribution`, `plot_contact_matrix`, etc.).

### Mixing ggplot2 and epydemix outputs

You can extract data from epydemix results and plot with ggplot2 instead of
matplotlib. This is useful when you want full control over the plot styling:

```r
library(tidyr)

# Extract quantiles and convert to R data frame
df <- py_to_r(results$get_projection_quantiles(simulation_dates))
df$date <- as.Date(df$date)

# Pivot from long format (date, data, quantile) to wide format
df_wide <- pivot_wider(df, names_from = quantile, values_from = data, names_prefix = "q")

# Plot with ggplot2
ggplot(df_wide, aes(x = date)) +
  geom_ribbon(aes(ymin = q0.05, ymax = q0.95), fill = "blue", alpha = 0.3) +
  geom_line(aes(y = q0.5)) +
  theme_minimal()
```

---

## Further reading

For more details about how to install Python packages and declaring
requirements, please refer to [Installing Python
Packages](https://rstudio.github.io/reticulate/articles/python_packages.html).

Also particularly useful is [Calling Python from
R](https://rstudio.github.io/reticulate/articles/calling_python.html), which
describes, among other things, how to deal with different data types in R
and Python.
