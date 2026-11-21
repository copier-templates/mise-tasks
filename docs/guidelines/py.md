# py guidelines

Rules for Python 3.15+ with uv as package manager. Tasks live in `tasks/py/*.tasks.toml`; run them with `mise run <task>`, never bare `uv`/`pytest`/`ruff`/`ty` in hooks or CI.

## Toolchain

- Pin `uv` in the consumer's `[tools]` (for example `uv = "0.13"`). Shared tasks never set task-level `tools`; `mise.lock` owns the exact version (see [mise guidelines](mise.md)).
- Pin Python with `.python-version` (for example `3.15`). `requires-python` in `pyproject.toml` must agree.
- Run everything through `uv run --frozen`. It uses the locked `uv.lock` and fails on drift instead of resolving anew. The task is the single source for flags.

## Project files

- `pyproject.toml` is the source of truth: `[project]`, `[dependency-groups]`, `[tool.pytest.ini_options]`. `uv.lock` is the resolved snapshot. Commit both plus `.python-version`.
- Keep runtime `dependencies` and `dev` group separate. `pytest`, `ruff`, `ty` belong in `dev`, so consumers without Python still resolve `uv run --frozen` once they add the group.
- Do not commit `.venv/`, `build/`, `dist/`, `.pytest_cache/`, `.ruff_cache/`, `htmlcov/`, or `__pycache__/`. `uv:clean` removes them.

## Install, update, audit

- Install with `uv:install` (`uv sync --all-groups`). Update within ranges with `uv:upgrade` (`uv sync --all-groups --upgrade`).
- Manage the lockfile with `uv:lock` (`uv lock`) and gate CI with `uv:lock:check` (`uv lock --check`) plus `uv:sync:check` (`uv sync --locked --check`).
- Audit with `uv:audit` (`uv audit --locked`). Inspect with `uv:tree`, prune the cache with `uv:cache:prune`.

## Lint, format, typecheck

- Lint with `ruff:lint` (`ruff check`, check-only). Autofix safe fixes with `ruff:fix` (`ruff check --fix`).
- Format in place with `ruff:fmt` (`ruff format`). Gate CI with `ruff:fmt:check` (`ruff format --check`), which never writes.
- Typecheck with `ty:check` (`ty check`, check-only). Autofix with `ty:fix` (`ty check --fix`).
- Pass files as trailing args so tasks and hooks can forward them (`mise run ruff:lint foo.py`). Keep the default task invocation unflagged; add `--statistics`, `--output-format`, or `--error-on-warning` at the call site.

## Tests

- Layout is `tests/unit/` and `tests/integration/`. `testpaths = ["tests"]` with `unit` / `integration` markers (see `pyproject.toml`).
- Run with `test:unit` / `test:integration`. Each skips with exit 0 when its directory is absent, so non-Python consumers stay green.
- Pass filters as trailing args (`mise run test:unit -- -k "pattern" -x --lf --tb=short -q`). Keep the default task invocation unflagged; `--collect-only`, `--junitxml`, `--durations`, and `-m` belong at the call site.

## Validation

Every change passes `mise tasks validate` and `prek run --all-files`.
