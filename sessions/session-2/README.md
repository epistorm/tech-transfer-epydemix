# Session 2: A Gentle Introduction to Epidemic Modeling with EpyScenario

![EpyScenario](https://cdn.prod.website-files.com/67bde9057c9d78157874e100/6970f89f26957a863a9a4711_epyscenario-p-1080.png)

Platform: [EpyScenario](https://scenario.epydemix.org/)

This session provides a gentle, no-code introduction to epidemic modeling using the Epydemix simulation dashboard. No programming experience required—everything runs through an interactive web interface.

## What You'll Do

- Configure and run age-structured epidemic models (SEIR, SEIRS, SEIHR) for 400+ geographies worldwide
- Adjust model parameters and compare scenarios side-by-side
- Design contact interventions and vaccination campaigns
- Visualize epidemic trajectories and summary metrics

## Why Start Here

The dashboard lets you build intuition for epidemic modeling concepts before diving into code. You'll see how parameter choices and interventions shape outbreak dynamics—foundational knowledge that carries into the Python and R sessions.

---

## Hands-On 1: SEIR Model (Measles) — Immunity vs. Transmission

📖 [Model structure reference](https://scenario.epydemix.org/Background#seir-measles)

**Goal:** Learn to modify model parameters and initial conditions; observe the interplay between background immunity and transmission rate.

**Setup:** Select the SEIR (Measles) model and set the population to North Carolina, USA.

### Scenarios

| Scenario | R₀ | Background Immunity | Purpose |
|----------|-----|---------------------|---------|
| A (Baseline) | 12 | 85% | Default measles parameters |
| B | 12 | 90% | Higher immunity — smaller outbreak |
| C | 12 | 95% | Herd immunity threshold — no outbreak |

### Steps

1. **Run Scenario A** with default parameters. Note the epidemic peak size and timing.
2. **Run Scenario B** by increasing background immunity to 90%. Compare: How does higher immunity affect the outbreak?
3. **Run Scenario C** by setting immunity to 95%. Observe: The outbreak fails to take off — herd immunity in action.

### Discussion Points

- How does background immunity shift the effective reproductive number?
- At what immunity threshold does the outbreak fail to take off?
- What does this tell us about herd immunity thresholds for highly transmissible diseases?

### Explore: Population Visualization

Before moving on, check out the **Population Viz** tab. Here you can explore:

- **Population pyramids** — Age distribution of the selected geography
- **Contact matrices** — Who contacts whom, broken down by setting (home, school, work, community)

---

## Hands-On 2: SEIRS Model (Influenza) — Vaccination Campaigns

📖 [Model structure reference](https://scenario.epydemix.org/Background#seirs-influenza) | [Vaccination campaigns](https://scenario.epydemix.org/Background#vaccination-campaigns)

**Goal:** Learn to configure vaccination campaigns and understand how rollout timing affects outbreak mitigation.

**Setup:** Select the SEIRS (Influenza) model and set the population to Italy.

### Scenarios

| Scenario | Vaccination | Coverage by Age Group | Campaign End | Ramp-up | Purpose |
|----------|-------------|----------------------|--------------|---------|---------|
| A (Baseline) | None | — | — | — | No intervention |
| B | Yes | 65+ → 65%, others → 20% | Day 50 | No | Immediate full-capacity rollout |
| C | Yes | 65+ → 65%, others → 20% | Day 50 | 25 days | Gradual rollout with ramp-up |

### Steps

1. **Run Scenario A** with default parameters and no vaccination. Note the epidemic trajectory and peak.
2. **Run Scenario B** by adding a vaccination campaign targeting 65% coverage in the 65+ group and 20% in all other age groups, ending on day 50, with no ramp-up (flat rollout). Compare: How does vaccination reduce the outbreak?
3. **Run Scenario C** by keeping the same coverage but enabling a 25-day ramp-up period. Compare: How does a slower rollout affect the outcome?

### Discussion Points

- How does vaccination coverage translate to outbreak reduction?
- Why does ramp-up timing matter, even with the same total coverage?
- What trade-offs exist between rapid rollout and logistical constraints?

### Explore: Vaccination Visualization

Check out the **Vaccination Viz** tab to see:

- **Dose allocation over time** — How doses are distributed across the campaign period
- **Age group targeting** — Which groups receive vaccines and when

Compare how the flat vs. ramp-up rollout strategies differ in dose distribution.

### Optional: Explore on Your Own

Using the baseline scenario (no vaccination), try modifying these parameters:

- **Duration of immunity** — Shorten the waning immunity period. What happens to the epidemic dynamics?
- **Seasonality** — Shift the peak day or change the intensity. How does timing affect outbreak size and shape?

---

## Hands-On 3: SEIHR Model (COVID-19) — Contact Interventions

📖 [Model structure reference](https://scenario.epydemix.org/Background#seihr-covid-19) | [Contact interventions](https://scenario.epydemix.org/Background#contact-interventions)

**Goal:** Learn to configure contact interventions (NPIs) and understand the trade-off between timing and intensity.

**Setup:** Select the SEIHR (COVID-19) model and set the population to United States.

### Scenarios

| Scenario | Intervention | Contact Layers | Reduction | Start Day | Purpose |
|----------|--------------|----------------|-----------|-----------|---------|
| A (Baseline) | None | — | — | — | No intervention |
| B | Yes | All | 60% | Day 10 | Early intervention |
| C | Yes | All | 60% | Day 30 | Late intervention |

### Steps

1. **Run Scenario A** with default parameters and no intervention. Note the epidemic peak and total hospitalizations.
2. **Run Scenario B** by adding contact interventions on all layers (home, school, work, community) with 60% reduction starting at day 10. Compare: How does early action affect the outbreak trajectory?
3. **Run Scenario C** by keeping the same 60% reduction but starting at day 30 instead. Compare: How does a 20-day delay affect peak hospitalizations?

### Discussion Points

- How does intervention timing affect peak hospitalizations?
- What are the trade-offs between acting early vs. waiting for more information?
- How might these results inform real-world policy decisions?

### Explore: Contact Interventions

Experiment with different contact layers (school, work, community) to see which settings have the greatest impact on transmission.

---

## EpyScenario is Open Source

The EpyScenario dashboard is fully open source: [github.com/ngozzi/epydemix-dashboard](https://github.com/ngozzi/epydemix-dashboard/tree/main)

You can fork the repository, modify it for your own use case, and deploy your own version using [Streamlit](https://streamlit.io/).

**Want to contribute?** We welcome contributions via pull request. You can also [open an issue](https://github.com/ngozzi/epydemix-dashboard/issues) on GitHub or reach out at epydemix@isi.it.
