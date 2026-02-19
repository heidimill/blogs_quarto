# Getting a Python Quarto Blog Running

## Install uv

**On Mac OS:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**On Windows (PowerShell):**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Install Quarto

1. [Download Quarto](https://quarto.org/docs/download/) for your OS specific CLI using a version `>=1.9`.
2. Install the CLI
3. Check that your CLI installation worked with `quarto check`

## Use uv and quarto to build structure

1. `uv init --lib .`
2. `uv venv --python 3.13` to make a different version installed.
3. `source .venv/bin/activate` to activate the shell
4. `uv add "polars[numpy, pyarrow, excel, database, fsspec, async, graph, plot, style, timezone]" lets-plot`
5. `uv add --dev ipykernel pyyaml nbformat nbclient "marimo>=0.19.11"`
6. Add the following text to your `pyproject.toml` that was created and save the file.
  ```
  [tool.uv]
  package = false
  ```
7. `quarto create project blog .` and the terminal will ask you for a title of your blog. [Read more about Quarto blogs](https://quarto.org/docs/websites/website-blog.html)
8. `quarto add marimo-team/quarto-marimo`
9. Edit your `_quarto.yml` to have the following text (see the [_quarto.yml guidance for more](https://quarto.org/docs/projects/quarto-projects.html#project-metadata)). The primary change is `output-dir: docs`.
  ```
  project:
    type: website
    output-dir: docs
  ```
10. This repo has a `new_post.sh` that can be run to create a new post with marimo chunks.
  A. Run  `chmod +x new_post.sh` so that the file will run (only needs to be run once).
  B. Now `./new_post.sh test "Test Marimo Post" "J. Hathaway"` will create a new folder in the `posts` folder with the folder name `test` that has an `index.qmd` file created with the title of `test marimo` and the author `J. Hathaway`.
11. Now run `QUARTO_MARIMO_VERSION=0.14.6 quarto preview` to build your site in the `docs` folder and serve it to your default web browser (Note: at some point we should be able to remove `QUARTO_MARIMO_VERSION=0.14.6`).
12. You can explore your website and make any other needed changes. 
13. Now push your changes to Github and then go to `settings > pages` to fix how our site is rendered using [Github pages](https://quarto.org/docs/publishing/github-pages.html). We want to use the `docs` folder method.
