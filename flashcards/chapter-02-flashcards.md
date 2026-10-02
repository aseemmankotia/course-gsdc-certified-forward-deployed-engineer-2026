## Chapter 2: Production-Grade Python for Client Delivery — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Poetry vs pip+requirements.txt — which guarantees reproducible transitive dependency resolution via a lock file? | Poetry (poetry.lock). pip+requirements.txt only pins what you list; transitive deps can still drift unless you use pip freeze on a fully built env. Exam tip: 'reproducible + lock file' = Poetry. |
| 2 | ruff vs flake8+pylint — main reason ruff is preferred in production tooling stacks? | Speed (Rust-based, 10-100x faster) plus a single pyproject.toml config replacing multiple legacy tools. Exam tip: 'fast unified linter' = ruff. |
| 3 | black vs yapf/autopep8 — which is the 'opinionated, near zero-config' formatter? | black. It intentionally minimizes configuration to eliminate style debates and guarantee identical output for identical input. Exam tip: 'no bikeshedding, deterministic format' = black. |
| 4 | Command: add pytest as a dev-only dependency in Poetry | poetry add pytest --group dev. Exam tip: --group dev keeps prod dependency list clean, separate from testing tools. |
| 5 | Command: auto-fix lint violations with ruff | ruff check --fix . Exam tip: ruff can both lint AND autofix many issues in one pass, unlike flake8. |
| 6 | Command: verify formatting without modifying files (CI use) | black --check . Exam tip: --check makes black exit non-zero if files aren't formatted, used to gate CI pipelines. |
| 7 | Command: create and activate a virtual environment with the standard library | python -m venv venv  then  source venv/bin/activate (Linux/Mac) or venv\Scripts\activate (Windows). Exam tip: venv is stdlib, no install required — baseline dependency isolation. |
| 8 | Command: run only tests matching a name pattern, verbosely | pytest -k "pattern" -v. Exam tip: -k filters by test name substring/expression; -v shows per-test pass/fail names. |
| 9 | Python logging levels, low to high severity, with numeric values | DEBUG(10) < INFO(20) < WARNING(30) < ERROR(40) < CRITICAL(50). Exam tip: setting logger level to WARNING suppresses DEBUG and INFO messages. |
| 10 | logger.exception() — what does it add automatically compared to logger.error()? | Full traceback (exc_info=True by default). Must be called inside an except block. Exam tip: use logger.exception when you want stack trace context for debugging a caught error. |
| 11 | Recommended layered module structure for a production Python service | api/ (routes/handlers), services/ (business logic), models/ (schemas/data classes), core/ (config, logging, shared utils), main.py (thin entrypoint). Exam tip: this is the 'separation of concerns' answer pattern. |
| 12 | Custom exception hierarchy pattern for defensive programming | Define a base AppError(Exception), then subclass specific errors (e.g., PaymentAPIError(AppError)). Catch the specific subclass, log with context, re-raise or handle — never bare 'except:'. Exam tip: bare except is always the wrong-answer trap. |
