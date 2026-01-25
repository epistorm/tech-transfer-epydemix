# Session 4: Tutorials and Exercises

Independent exercises to reinforce concepts from Session 3. Work through these at your own pace—solutions are provided, but try to solve them yourself first.

---

## Exercise 1: SEIRS Model for a Different Country

| | Template | Solution |
|---|---|---|
| Python | [exercise_1_seirs_model.ipynb](exercises/python/exercise_1_seirs_model.ipynb) | [exercise_1_seirs_model.ipynb](solutions/python/exercise_1_seirs_model.ipynb) |
| R (Colab) | [exercise_1_seirs_model.ipynb](exercises/r-colab/exercise_1_seirs_model.ipynb) | [exercise_1_seirs_model.ipynb](solutions/r-colab/exercise_1_seirs_model.ipynb) |
| R (Local) | [exercise_1_seirs_model.Rmd](exercises/r-local/exercise_1_seirs_model.Rmd) | [exercise_1_seirs_model.Rmd](solutions/r-local/exercise_1_seirs_model.Rmd) |

**Objective:** Build an SEIRS model (with waning immunity) and simulate it for a country of your choice.

**Skills practiced:**
- Defining compartments and transitions
- Loading population data
- Running and visualizing simulations

**Tasks:**

1. Create an SEIRS model with compartments: S, E, I, R
   - Add an additional transition R → S with rate `omega` (waning immunity)
   - Use parameters: β=0.03, σ=0.2, γ=0.1, ω=0.01 (immunity lasts ~100 days)

2. Load population data for a country of your choice from the [supported locations](https://github.com/epistorm/epydemix-data/blob/main/locations.csv)

3. Run 50 simulations over 1 year and visualize:
   - All compartments over time
   - Infections by age group

4. **Discussion:** How does waning immunity affect the long-term dynamics compared to a standard SEIR model?

<details>
<summary>Hint</summary>

The R → S transition is spontaneous (doesn't depend on other compartments):
```python
model.add_transition(source="R", target="S", params="omega", kind="spontaneous")
```
</details>

---

## Exercise 2: Comparing Intervention Strategies 

| | Template | Solution |
|---|---|---|
| Python | [exercise_2_interventions.ipynb](exercises/python/exercise_2_interventions.ipynb) | [exercise_2_interventions.ipynb](solutions/python/exercise_2_interventions.ipynb) |
| R (Colab) | [exercise_2_interventions.ipynb](exercises/r-colab/exercise_2_interventions.ipynb) | [exercise_2_interventions.ipynb](solutions/r-colab/exercise_2_interventions.ipynb) |
| R (Local) | [exercise_2_interventions.Rmd](exercises/r-local/exercise_2_interventions.Rmd) | [exercise_2_interventions.Rmd](solutions/r-local/exercise_2_interventions.Rmd) |

**Objective:** Design and compare three different intervention strategies for controlling an outbreak.

**Skills practiced:**
- Using `add_intervention` for contact reductions
- Using `override_parameter` for transmission changes
- Quantifying intervention impact

**Scenario:** An outbreak begins on March 1, 2026. You have until the end of the year to control it. Compare:

1. **School closure only:** 80% reduction in school contacts from April 1 to June 30
2. **Work-from-home only:** 60% reduction in work contacts from April 1 to August 31
3. **Combined but lighter:** 40% reduction in both school and work from April 1 to May 31

**Tasks:**

1. Create an SEIR model for the United States (or another large country)
2. Implement all three intervention scenarios
3. Run simulations and compare:
   - Peak infection size
   - Total infections (final R count)
   - Time to peak
4. Create a summary visualization comparing all scenarios

**Discussion:** Which strategy is most effective? What trade-offs exist between intervention intensity and duration?

<details>
<summary>Hint</summary>

To compute time to peak:
```python
trajectories = results.get_stacked_compartments()
peak_days = trajectories["I_total"].argmax(axis=1)  # Index of peak for each simulation
```
</details>

---

## Exercise 3: Two-Strain Model (Intermediate-Advanced)

| | Template | Solution |
|---|---|---|
| Python | [exercise_3_two_strains.ipynb](exercises/python/exercise_3_two_strains.ipynb) | [exercise_3_two_strains.ipynb](solutions/python/exercise_3_two_strains.ipynb) |
| R (Colab) | [exercise_3_two_strains.ipynb](exercises/r-colab/exercise_3_two_strains.ipynb) | [exercise_3_two_strains.ipynb](solutions/r-colab/exercise_3_two_strains.ipynb) |
| R (Local) | [exercise_3_two_strains.Rmd](exercises/r-local/exercise_3_two_strains.Rmd) | [exercise_3_two_strains.Rmd](solutions/r-local/exercise_3_two_strains.Rmd) |

**Objective:** Model the emergence of a more transmissible variant using a multi-strain SIR model.

**Skills practiced:**
- Designing complex compartmental structures
- Using `override_parameter` for delayed strain emergence
- Interpreting multi-strain dynamics

**Model structure:**

A second, more transmissible strain emerges after the first strain has been circulating:

- **Compartments:** S, I₁, I₂, R₁, R₂
- **Transitions:**
  - S + I₁ → 2I₁ (rate β)
  - S + I₂ → 2I₂ (rate β·ψ, where ψ > 1 is the transmissibility advantage)
  - R₁ + I₂ → I₂ + R₂ (rate β·ψ·γ, partial cross-immunity)
  - I₁ → R₁ (rate μ)
  - I₂ → R₂ (rate μ)

**Tasks:**

1. Implement the two-strain model with:
   - β = 0.20, μ = 0.1
   - ψ = 1.5 (strain 2 is 50% more transmissible)
   - γ = 0.4 (R₁ individuals have 60% protection against strain 2)

2. Use `override_parameter` to delay strain 2 emergence:
   - Set ψ = 0 and μ₂ = 0 for the first 30 days

3. Simulate for 6 months and visualize I₁ and I₂ over time

4. **Experiments:**
   - What happens if strain 2 emerges earlier (day 15) vs. later (day 45)?
   - What if strain 2 is only 20% more transmissible (ψ = 1.2)?

<details>
<summary>Hint</summary>

For the S → I₂ transition (infection with strain 2), use a parameter expression:
```python
model.add_transition(source="S", target="I2", kind="mediated", params=("beta*psi", "I2"))
```

For the R₁ + I₂ → I₂ + R₂ transition (reinfection), the target is I₂:
```python
model.add_transition(source="R1", target="I2", kind="mediated", params=("beta*psi*gamma", "I2"))
```
</details>

---

## Exercise 4: Calibrate and Project an SEIR Model with Interventions

| | Template | Solution |
|---|---|---|
| Python | [exercise_4_seir_calibration.ipynb](exercises/python/exercise_4_seir_calibration.ipynb) | [exercise_4_seir_calibration.ipynb](solutions/python/exercise_4_seir_calibration.ipynb) |
| R (Colab) | [exercise_4_seir_calibration.ipynb](exercises/r-colab/exercise_4_seir_calibration.ipynb) | [exercise_4_seir_calibration.ipynb](solutions/r-colab/exercise_4_seir_calibration.ipynb) |
| R (Local) | [exercise_4_seir_calibration.Rmd](exercises/r-local/exercise_4_seir_calibration.Rmd) | [exercise_4_seir_calibration.Rmd](solutions/r-local/exercise_4_seir_calibration.Rmd) |

**Objective:** Generate synthetic outbreak data with an intervention, calibrate model parameters, and project under alternative policy scenarios.

**Skills practiced:**
- Generating synthetic "ground truth" data with interventions
- Setting up ABC-SMC calibration with multiple parameters
- Using `override_parameter` for time-varying transmission
- Running scenario-based projections with uncertainty

**Scenario:** An SEIR outbreak begins in California. On day 50, interventions reduce transmission (β) to 60% of its original value. You observe incidence data through day 74, then project forward under different policy scenarios.

**Tasks:**

1. **Generate synthetic data** from an SEIR model for California:
   - Use β = 0.035, σ = 0.2, γ = 0.1
   - At day 50, β drops to 60% of baseline (intervention effect)
   - Run for 120 days, extract E → I transitions as "observed" incidence

2. **Set up calibration** with priors for two parameters:
   - `beta`: U(0.02, 0.045) — baseline transmission rate
   - `reduction`: U(0.3, 0.9) — fraction β drops to during intervention

3. **Run ABC-SMC calibration** using the first 74 days of data:
   - 100 particles, 5 generations
   - Compare posterior distributions to true values

4. **Project under two scenarios** from day 74 onward:
   - **Status quo:** Intervention continues (β stays reduced)
   - **Relaxation:** Interventions are lifted (β returns to baseline)

5. **Visualize and compare** projections against the held-out "truth"

**Discussion:**
- Can ABC-SMC recover the true β and reduction factor?
- How do the two scenarios differ in projected infections?
- What are the implications for policy decision-making under uncertainty?

<details>
<summary>Hint</summary>

To implement the intervention in the simulation wrapper:
```python
def simulate_wrapper(parameters):
    # Extract calibrated parameters
    beta = parameters["beta"]
    reduction = parameters["reduction"]

    # Override beta after intervention day
    model.override_parameter(
        start_date=intervention_date,
        end_date=end_date,
        parameter_name="beta",
        value=beta * reduction
    )

    results = simulate(**parameters)
    return {"data": results.transitions["S_to_E_total"]}
```
</details>

---

## Exercise Templates

Starter notebooks with structure, imports, and setup (but not the full solution code) are available in the [exercises/](exercises/) folder. Use these to work through the exercises on your own.

## Solutions

Solutions are available in three formats (Python, R Colab, R Local). See the [solutions/](solutions/) folder.

---

## Resources

- [Epydemix Documentation](https://epydemix.readthedocs.io/)
- [Supported Geographies](https://github.com/epistorm/epydemix-data/blob/main/locations.csv)
- [Session 3 Tutorial 1: Modeling](../session-3/python/01_modeling_tutorial.ipynb)
- [Session 3 Tutorial 2: Calibration](../session-3/python/02_calibration_tutorial.ipynb)
