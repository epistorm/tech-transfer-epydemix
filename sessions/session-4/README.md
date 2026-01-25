# Session 4: Tutorials and Exercises

Independent exercises to reinforce concepts from Session 3. Work through these at your own pace—solutions are provided, but try to solve them yourself first.

---

## Exercise 1: SEIRS Model for a Different Country (Beginner)

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

## Exercise 2: Comparing Intervention Strategies (Intermediate)

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

For the R₁ + I₂ → I₂ + R₂ transition (reinfection), the target is I₂:
```python
model.add_transition(source="R1", target="I2", kind="mediated", params=("beta*psi*gamma", "I2"))
```
</details>

---

## Exercise 4: Calibrate and Project an SEIR Model (Advanced)

**Objective:** Calibrate an SEIR model to real-world-like data and generate projections.

**Skills practiced:**
- Setting up ABC calibration
- Defining appropriate priors
- Running projections with uncertainty

**Tasks:**

1. Use the incidence data from the calibration tutorial but fit an **SEIR model** instead of SIR:
   ```python
   data = pd.read_csv('https://raw.githubusercontent.com/epistorm/epydemix/refs/heads/main/tutorials/data/incidence_data.csv')
   ```

2. Set up the SEIR model with Indonesia population and define priors:
   - transmission_rate: U(0.01, 0.03)
   - latent_rate (σ): U(0.1, 0.3) — corresponds to 3-10 day latent period
   - recovery_rate: U(0.1, 0.2)

3. Create a wrapper function that returns the S → E transitions (new exposures)

4. Run ABC-SMC calibration with 100 particles and 5 generations

5. Split the data: use first 80 days for calibration, remaining for validation

6. Run projections and compare to held-out data

**Discussion:**
- How do the posterior distributions compare to the SIR calibration?
- Does adding the E compartment improve the fit?

<details>
<summary>Hint</summary>

For the wrapper function with an SEIR model, extract the S → E transitions:
```python
def simulate_wrapper(parameters):
    results = simulate(**parameters)
    return {"data": results.transitions["S_to_E_total"]}  # Adjust compartment names
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
