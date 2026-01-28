#  Insight Net Tech Transfer Workshop, 28-29 January, 2026 (Chapel Hill, NC)
This repository contains all the materials (code, data, and instructions) for the 28-29 January, 2026 Insight Net Tech Transfer Workshop focused on epydemix.


## Workshop Objectives

This two-day hands-on workshop introduces [Epydemix](https://github.com/epistorm/epydemix), an open-source platform for stochastic epidemic modeling, simulation, and forecasting. You'll gain both theoretical foundations and practical skills across Epydemix's interfaces: simulation dashboards, Python package, R integration, and forecasting tools.

### What You'll Learn

**Theory**
- Stochastic epidemic processes and chain-binomial models
- Approximate Bayesian Computation (ABC) for model calibration
- Principles of epidemic forecasting with mechanistic models

**Hands-On Skills**
- Install and use the Epydemix Python package and R interface
- Implement ABC calibrations, retrospective analyses, and forecasting pipelines
- Explore intervention strategies and visualize epidemic trajectories

**Tools & Applications**
- Design and run epidemic models (SIR, SEIR, etc.) using the dashboard with country-specific population data and age-stratified contact matrices
- Forecasting application for real-time predictions
- Performance assessment dashboard for evaluating model accuracy

By the end, you'll be equipped to incorporate Epydemix into research and operational settings with reproducible, cross-platform workflows.

## Agenda

### Day 1 – Foundations and Core Tools

| Time | Session |
|------|---------|
| 09:00 – 09:30 | **Welcome and Overview** — Workshop objectives, introductions, Epydemix ecosystem overview |
| 09:30 – 11:00 | **Session 1: Theory Behind Epydemix** — Stochastic models (deterministic SIR to chain-binomial), ABC approaches, linking models to forecasting |
| 11:00 – 11:10 | *Coffee Break* |
| 11:10 – 12:30 | **Session 2: Epydemix Simulation Platform** — Running SIR/SEIR/SIS simulations, population & contact matrices, configuring interventions |
| 12:30 – 13:30 | *Lunch Break* |
| 13:30 – 15:30 | **Session 3: Python Package & R Interface** — Environment setup, modules overview, Jupyter notebooks & R wrapper functions |
| 15:30 – 16:00 | *Coffee Break* |
| 16:00 – 17:00 | **Session 3 (cont.): Under the Hood** — Scripting simulations, accessing population data, defining custom compartments & interventions |

### Day 2 – Tutorials, Forecasting, and Performance

| Time | Session |
|------|---------|
| 09:00 – 09:15 | **Recap and Day 2 Goals** |
| 09:15 – 10:15 | **Session 4: Tutorials and Exercises** — Model design, parameterization, retrospective calibration, ABC pipelines |
| 10:15 – 10:30 | *Coffee Break* |
| 10:30 – 12:30 | **Session 5: Forecast Pipeline and Application** — Full forecasting workflow, data ingestion, GUI exploration, guided exercises |
| 12:30 – 13:30 | *Lunch Break* |
| 13:30 – 15:45 | **Session 6: Forecast Visualization & Performance** — Performance dashboard, validation metrics, comparing model outputs |
| 15:45 – 16:00 | *Coffee Break* |
| 16:00 – 17:00 | **Closing Discussion** — Wrap-up, feedback, collaboration opportunities, next steps |

## Quick Links

- [Installation Guides](installation/) (includes [Miniforge option](installation/miniforge-setup.md) for organizations with Anaconda licensing concerns)
- [Session 1: Theory Behind Epydemix](sessions/session-1/)
- [Session 2: Epydemix Simulation Platform](sessions/session-2/)
- [Session 3: Python Package & R Interface](sessions/session-3/)
- [Session 4: Tutorials and Exercises](sessions/session-4/)
- [Session 5: Forecast Pipeline and Application](sessions/session-5/)
- [Session 6: Forecast Visualization & Performance](sessions/session-6/)


## Resources

- [Epydemix Website](https://www.epydemix.org/)
- [Epydemix Documentation](https://epydemix.readthedocs.io/en/latest/)
- [EpyScenario Platform](https://scenario.epydemix.org/)

To stay updated on new features and releases, consider starring the [Epydemix repository](https://github.com/epistorm/epydemix) on GitHub.

### Citing Epydemix

If you use Epydemix in your work, please cite:

```bibtex
@article{gozzi2025epydemix,
  title={Epydemix: An open-source Python package for epidemic modeling with integrated approximate Bayesian calibration},
  author={Gozzi, Nicol{\'o} and Chinazzi, Matteo and Davis, Jessica T and Gioannini, Corrado and Rossi, Luca and Ajelli, Marco and Perra, Nicola and Vespignani, Alessandro},
  journal={PLOS Computational Biology},
  volume={21},
  number={11},
  pages={e1013735},
  year={2025},
  publisher={Public Library of Science San Francisco, CA USA}
}
```

## Contact

For questions or issues, please open an issue on [GitHub](https://github.com/epistorm/epydemix/issues) or contact the maintainer at epydemix@isi.it.
