
# Quarto_Sandbox

This is a minimal example demonstrating and experimenting with Quarto CI/CD.

## Why?

CI/CD (via GitHub or on-premises) can be used to store, build, and host reports, jobs, or Shiny apps in production. By using a standard build, we can avoid code that only works on one machine at a particular time with a specific setup. This approach aims to be more reproducible, reliable, and collaborative.

## How?

This repository is a Quarto project created with the command:

```bash
quarto create-project .
```

The document `quarto_sandbox.qmd` includes a very simple Quarto document setup that uses `ggplot2` and `knitr` to generate a table and plot from a built-in dataset. The document and process were taken from DevOps for Data Science. https://do4ds.com/

Quarto has a command that performs the initial build and creates a `gh-pages` branch:

```bash
quarto publish gh-pages
```

Note that all development is done in the `dev` branch. When changes are made, follow up with a pull request to the `main` branch, and GitHub will rebuild the site on `gh-pages`. Doing development on `main` would result in constant rebuilds for every change and could lead to broken builds being hosted in the interim.

The end result is available here: https://jasonlocklin.github.io/quarto_sandbox/

### Notable Files

- `quarto_sandbox.qmd`: The main Quarto document.
- `.github/workflows/publish.yml`: The GitHub Actions workflow file that instructs GitHub to build the site on push to the `main` branch. It uses Ubuntu, installs Quarto and R, builds the necessary environment with `renv`, and then builds the page.
- `.github/workflows/renv.lock`: The lock file for the `renv` environment.

## About Quarto Freeze

Let's say you have an article with lots of long-running computations, fragile code, or unreliable data sources. If you want to be able to edit the content of the article without re-computing everything, Quarto's freeze feature might be a good idea. Generally, however, the data will change more often than the content, so re-computing every build is a good idea to ensure the data is up-to-date.
