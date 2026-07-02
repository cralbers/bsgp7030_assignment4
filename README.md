# BSGP 7030 assignment 4

Jupyter notebooks for statistical analysis in Python using **pandas**, **scipy**, **statsmodels**, and **seaborn**. The notebooks explore brain size, iris, and wages datasets with descriptive statistics, hypothesis tests, and regression models.

## Description

- Files in `/manual` were generated without the use of an AI agent
- Files in `/ai` were generated with the aid of Cursor Pro

## Project structure

```
assignment4/
├── README.md                    # This file — overview, usage, and setup
├── .gitignore                   # Ignores checkpoints, local Jupyter config, REFLECTION.md
├── environment.yml              # Conda env (`assignment4`) for Python and Jupyter
│
├── data/                        # Input datasets
│   ├── brain_size.csv           # Brain size and IQ measures by gender
│   ├── iris.csv                 # Fisher iris measurements by species
│   └── wages.csv                # 1985 CPS wage determinants (534 workers)
│
├── manual/                      # Hand-written code (no AI agent)
│   └── stats_python.ipynb       # Statistical analysis notebook
│
└── ai/                          # AI-generated code (Cursor Pro)
    ├── stats_python.ipynb       # Main analysis: EDA, tests, OLS, multiple regression
    ├── stats_extension.ipynb    # Robust regression (RLM) extension for wages model
    └── PROMPTS.md               # Cursor prompts used to generate the AI files
```

## Notebooks

### `manual/stats_python.ipynb` or `ai/stats_python.ipynb`

Main statistical analysis notebook, organized into sections:

- **Setup / Load data** — imports, data loaders, previews
- **Brain size analysis** — group means, box plots, scatter matrices
- **Statistics** — t-tests, Wilcoxon, Mann-Whitney on brain size IQ measures
- **Linear models** — simulated OLS, VIQ by gender, FSIQ vs PIQ (long format)
- **Multiple regression** — iris pairplot, OLS, contrasts
- **Wages** — pairplots, lmplot, OLS main effects and interaction (log10 wage)

### `ai/stats_extension.ipynb`

Extension notebook comparing OLS and robust regression (Huber's T) for the wages model `wage ~ education + C(sex)`, with both fitted lines plotted together.

## Usage

Open and run the notebooks from the `manual/` or `ai/` directory (or project root) so that relative paths to `../data/` resolve correctly.

```bash
cd ai
jupyter lab
```

Run cells top to bottom in each notebook. The wages loader applies two transformations on import:

- `sex` recoded to `"Male"` / `"Female"` strings
- `wage` transformed with `log10`

## Installation

### Clone repo

```bash
git clone https://github.com/cralbers/bsgp7030_assignment4.git
cd bsgp7030_assignment4
```

### Conda environment

From `assignment4`:

```bash
conda env create -f environment.yml
conda activate assignment4
jupyter lab
```

Key packages: pandas, scipy, statsmodels, seaborn, matplotlib, jupyterlab.

## AI documentation

See [`ai/PROMPTS.md`](ai/PROMPTS.md) for the sequence of Cursor prompts used to build the AI notebooks.
