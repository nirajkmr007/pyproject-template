# pyproject-template

An opinionated [Copier](https://copier.readthedocs.io/) template for starting new
Python **libraries** with a modern, batteries-included toolchain.

Answer a short questionnaire, pick the features you want, and get a clean,
ready-to-develop project in seconds.

## Quick start

You only need [uv](https://docs.astral.sh/uv/) installed — it runs Copier for you
with `uvx`, so there is nothing else to install globally.

```bash
# From the published GitHub repo:
uvx copier copy gh:nirajkmr007/pyproject-template my-new-project

# ...or from a local checkout of this template:
uvx copier copy /path/to/pyproject-template my-new-project
```

Then:

```bash
cd my-new-project
just bootstrap     # create venv, install deps, install git hooks
just check         # lint + format-check + type-check + tests
```

## What you always get

- **uv** for package & environment management (with a committed `uv.lock`)
- **just** as the command runner (`just` lists everything)
- **ruff** for linting *and* formatting
- **pytest** for testing
- **pre-commit** hooks wired to ruff (and mypy when enabled)
- `src/` layout, `py.typed` marker, hatchling build backend, `pyproject.toml`-only config

## Features you can toggle

When you run the template you'll be asked which of these to include:

| Question | Default | What it adds |
|---|---|---|
| `use_mypy` | yes | Strict `mypy` type checking + a pre-commit hook |
| `use_coverage` | yes | `pytest-cov` with terminal coverage report |
| `use_github_actions` | yes | CI workflow: lint + type-check + tests |
| `publish_pypi` | no | Tag-triggered PyPI publish via Trusted Publishing |
| `use_docker` | no | Multi-stage, non-root `Dockerfile` + `.dockerignore` |
| `use_docs` | no | MkDocs Material site (+ a Pages deploy workflow if CI is on) |

You're also prompted for project name, slug, package name, description, author,
GitHub username, target Python version (3.10–3.13), and license
(MIT / Apache-2.0 / BSD-3-Clause / GPL-3.0-only / Proprietary).

## Customization

- **Change defaults / add questions:** edit [`copier.yml`](copier.yml).
- **Change generated files:** everything under [`template/`](template/) is the
  scaffold. Files ending in `.jinja` are rendered (the suffix is stripped);
  `{% raw %}{{ ... }}{% endraw %}` and `{% raw %}{% if ... %}{% endraw %}` are
  Jinja. Filenames like `{% raw %}{% if use_docker %}Dockerfile{% endif %}.jinja{% endraw %}`
  are conditionally generated — when the condition is false the file is skipped.
- **Update existing projects:** because this is Copier, once a project is
  generated you can pull in later template improvements with
  `copier update` from inside that project.

## Repository layout

```
pyproject-template/
├── copier.yml          # the questionnaire + Copier config
├── README.md           # this file
└── template/           # the scaffold that becomes a new project
    ├── pyproject.toml.jinja
    ├── justfile.jinja
    ├── .pre-commit-config.yaml.jinja
    ├── src/{% raw %}{{ package_name }}{% endraw %}/...
    ├── tests/...
    └── (conditional) .github/, Dockerfile, mkdocs.yml, docs/
```

## License

MIT — see [LICENSE](LICENSE).
