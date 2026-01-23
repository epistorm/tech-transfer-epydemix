
# Using Google Colab

[Google Colab](https://colab.research.google.com/) is a free, cloud-based
Jupyter notebook environment hosted by Google. It requires **no local
installation** — everything runs in your browser.

## Why we use it

- **Zero setup**: Python, common libraries, and GPU/TPU access are
  pre-configured.
- **Cross-platform**: Works on any OS with a modern browser.
- **Shareable**: Notebooks can be opened directly from GitHub with a single
  click (via the "Open in Colab" badge at the top of each notebook).

## Requirements

- A **Google account** (Gmail, Google Workspace, etc.).
- A modern web browser (Chrome, Firefox, Edge, Safari).
- An internet connection.

## How to open a workshop notebook

1. Navigate to the notebook on GitHub.
2. Click the **"Open in Colab"** badge at the top of the notebook.
3. Sign in with your Google account if prompted.
4. The notebook opens in a temporary runtime — you can run cells immediately.

## R notebooks in Colab

Some workshop notebooks use R via the
[rpy2](https://rpy2.github.io/) extension. These notebooks include a setup cell
that loads the `rpy2.ipython` extension and enables `%%R` magic, so you can
write R code directly inside Colab cells. No separate R installation is needed.

## Important notes

- **Runtimes are ephemeral**: if you disconnect or are idle for too long, your
  runtime resets and all variables are lost. Re-run cells from the top if this
  happens.
- **Saving your work**: use *File → Save a copy in Drive* to keep your changes
  in your Google Drive, or *File → Download .ipynb* to save locally.
- **Installing packages**: the first cell in each notebook installs any required
  packages (e.g., `!pip install epydemix`). This runs once per session.
