# Session 4: Exercise Solutions

Solution notebooks for the Session 4 exercises. Try to solve the exercises yourself before looking at these!

## Available Formats

Each solution is available in three formats:

| Format | Location | Best For |
|--------|----------|----------|
| **Python Jupyter** | [`python/`](python/) | Python users, Colab |
| **R Jupyter (Colab)** | [`r-colab/`](r-colab/) | R users on Google Colab (uses `rpy2` + `%%R` magic) |
| **R Markdown** | [`r-local/`](r-local/) | R users with local RStudio (uses `reticulate`) |

---

## Solutions

| Exercise | Python | R (Colab) | R (Local) | Key Concepts |
|----------|--------|-----------|-----------|--------------|
| 1. SEIRS Model | [python](python/exercise_1_seirs_model.ipynb) | [r-colab](r-colab/exercise_1_seirs_model.ipynb) | [r-local](r-local/exercise_1_seirs_model.Rmd) | Waning immunity, R→S transition, comparing SEIR vs SEIRS |
| 2. Intervention Comparison | [python](python/exercise_2_interventions.ipynb) | [r-colab](r-colab/exercise_2_interventions.ipynb) | [r-local](r-local/exercise_2_interventions.Rmd) | `add_intervention`, contact reductions, quantifying impact |
| 3. Two-Strain Model | [python](python/exercise_3_two_strains.ipynb) | [r-colab](r-colab/exercise_3_two_strains.ipynb) | [r-local](r-local/exercise_3_two_strains.Rmd) | Multi-strain dynamics, `override_parameter`, variant emergence |
| 4. SEIR Calibration | [python](python/exercise_4_seir_calibration.ipynb) | [r-colab](r-colab/exercise_4_seir_calibration.ipynb) | [r-local](r-local/exercise_4_seir_calibration.Rmd) | ABC-SMC calibration, intervention effects, scenario projections |

## Running the Solutions

- **Python (local):** With Epydemix installed (`pip install epydemix` or `conda install -c conda-forge epydemix`)
- **Python (Colab):** Click the Colab badge at the top of each Python notebook
- **R (Colab):** Click the Colab badge at the top of each R Colab notebook (uses `rpy2`)
- **R (local):** Open the `.Rmd` files in RStudio with `reticulate` and Epydemix configured
