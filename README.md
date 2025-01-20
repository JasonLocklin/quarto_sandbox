# Quarto_Sandbox

This is a minimal example demonstrating/experimenting with Quarto CI/CD.

This repository is a Quarto project created with the command:

> quarto create-project .

The document quarto_sandbox.qmd includes a very simple Quarto document set up
that makes use of ggplot2 and knitr to generate a table and plot from a built
in dataset. The document and process was taken from DevOps for Data Science 
( https://do4ds.com/ ).

Quarto has a command that does the initial build and creates a gh-pages
branch:

> quarto publish gh-pages

Note that all development is done in the "dev" branch. When changes are made,
follow-up with a pull request to "main" branch, and github will re-build
the site on gh-pages. Doing development on "main" would result constant in re-builds for
every change, and would see broken builds hosted in the interim. 

The end result is avialable here: https://jasonlocklin.github.io/quarto_sandbox/

Notable files:

- quarto_sandbox.qmd: The main Quarto document
- .github/workflows/publish.yml: The GitHub Actions workflow file that instructs
  GitHub to build the site on push to the main branch (note that it uses Ubuntu,
  installs Quarto and R, builds the necissary environment with `renv` and then
  builds the page).
- .github/workflows/renv.lock: The lock file for the renv environment.


## About Quarto Freeze
Let's say you have an article with lots of long-running computations, fragile
code, or unreliable data sources. If you want to be able to edit the content
of the article without re-computing everything, Quarto's freeze feature might be a good idea.
Generally, however, the data will change more often than the content, so
re-computing every build is a good idea to ensure the data is up-to-date.
