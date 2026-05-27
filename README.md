# Paper Project Template GitHub Repository

This repository serves as a template for code repository associated with an academic paper.
You can use this template as a starting point for your code repository when beginning a new project.

This repository follows some specific design principles:
- We use `uv` for package management.
- It is expected that code will be abstracted into a package, with functions and classes that can be imported into relevant scripts and notebooks.
- An `artifacts` folder delineates where meaningful paper deliverables (e.g., figures) go.
- Plots, scripts, and notebooks are all separated:
    - Use `plots` for scripts that will generate `artifacts`.
    - Use `scripts` for scripts that will conduct relevant analyses or launch jobs.
    - Use `notebooks` for exploratory notebooks that you need to track. 
    - It is expected that no meaningful results will remain in `notebooks`; eventually they should be formalized into `scripts` or `plots`.


## Start a New Paper Repo

Click **Use this template** on GitHub to create a new repository, then clone your new repository:

```bash
git clone git@github.com:OWNER/my_paper_repo.git
cd my_paper_repo
```

Or use the GitHub CLI:

```bash
gh repo create OWNER/my_paper_repo --template pssachdeva/template_paper_repo --private --clone
cd my_paper_repo
```

Edit `pyproject.toml` and replace `package_name` with a short importable name for your project. Rename `src/package_name/` to match that name.

## Set Up Python

This template uses Python 3.12 and `uv`.

```bash
uv sync
```

When you add dependencies, add them to `pyproject.toml`, then update the lockfile:

```bash
uv lock
uv sync
```

For a real paper repo, commit `uv.lock` so the computational environment can be reproduced. For this template repo, the lockfile does not need to be committed.

## Repository Layout

`src/` contains reusable project code.

`notebooks/` contains exploratory notebooks.

`plots/` contains scripts that generate plots and figures.

`scripts/` contains command-line or one-off workflow scripts.

`tests/` contains tests for reusable code.

`data/` is for local data files. Its contents are ignored by git.

`artifacts/` is for generated outputs such as figures, tables, logs, and model outputs. Its contents are ignored by git.

## Typical Workflow

Put reusable logic in `src/`, call that logic from notebooks or scripts, and write final plotting code in `plots/`. Keep raw data in `data/` and generated files in `artifacts/` unless there is a clear reason to commit a specific output.

Before sharing results, make sure someone else can run:

```bash
uv sync
uv run pytest
```

Add project-specific instructions here as the paper develops: where data comes from, how to regenerate each figure, and how to build the manuscript.
