## Chapter 2: Production-Grade Python for Client Delivery — Practice Questions

**Q1.** A client project must guarantee that every developer and CI runner installs the exact same dependency versions, including transitive dependencies, and must separate production dependencies from dev-only tools like pytest and ruff. Which approach BEST meets these requirements?

A) A single requirements.txt with unpinned package names, installed via pip
B) A conda environment.yml exported manually after each install
C) Global pip installs on each developer's machine with a shared README of versions
D) Poetry with pyproject.toml, dependency groups, and a committed poetry.lock file

<details>
<summary>Answer</summary>

**Correct: D**

Poetry resolves and pins exact versions (including transitive deps) in poetry.lock, and pyproject.toml dependency groups ([tool.poetry.group.dev]) cleanly separate prod vs dev tooling — reproducible everywhere.

**Why the others are wrong:**
- Unpinned requirements.txt allows different resolved versions over time — not reproducible.
- conda environment.yml exported manually is error-prone and not automatically kept in sync; also non-standard for pure-Python client delivery.
- Manual README-based version tracking has no enforcement and drifts immediately.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A pipeline function calls a third-party payment API. The exam scenario requires the function to fail safely, preserve the original stack trace for debugging, and never silently swallow unexpected errors. Which pattern is correct?

A) except PaymentAPIError as e: logger.exception('Payment failed'); raise
B) except: pass
C) except Exception as e: print(e)
D) except Exception: return None

<details>
<summary>Answer</summary>

**Correct: A**

Catching a specific expected exception, logging with logger.exception() (which captures the full traceback), then re-raising preserves context while still failing loudly for anything unhandled.

**Why the others are wrong:**
- 'except: pass' is a bare except that swallows ALL errors including KeyboardInterrupt/SystemExit and hides the failure completely — the classic defensive-programming exam trap.
- print(e) loses the traceback and isn't captured by log aggregation/monitoring systems.
- Returning None on any Exception masks the real error and lets bad data propagate silently downstream.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A client deliverable currently lives in a single 900-line script.py mixing HTTP handlers, business logic, and database queries. Which restructuring BEST reflects production-grade separation of concerns?

A) Move the file into a Jupyter notebook so each function is its own cell
B) Rename script.py to app.py and add more comments
C) Split into api/routes.py, services/business_logic.py, models/schemas.py, and core/config.py, with main.py as a thin entrypoint
D) Wrap the whole file's logic inside a single class with 40 methods

<details>
<summary>Answer</summary>

**Correct: C**

Layered modules (api/services/models/core) isolate transport, business logic, data schema, and configuration — each layer changes and is tested independently, which is the exam's definition of separation of concerns.

**Why the others are wrong:**
- Notebooks are for exploration, not production delivery — no imports, testing, or packaging story.
- Renaming and commenting doesn't change the architecture; the mixing of concerns remains.
- A single mega-class with 40 methods is God-object anti-pattern — concerns are still coupled, just inside one class instead of one file.

</details>

---

**Q4.** Which tool should a team pick to replace both flake8 and pylint for linting a client codebase, primarily because of execution speed and a single unified configuration in pyproject.toml?

A) mypy
B) autopep8
C) ruff
D) bandit

<details>
<summary>Answer</summary>

**Correct: C**

ruff is a Rust-based linter that reimplements most flake8/pylint rule sets, runs orders of magnitude faster, and is configured in one [tool.ruff] section of pyproject.toml.

**Why the others are wrong:**
- mypy is a static type checker, not a general-purpose linter — different tool category.
- autopep8 auto-formats code to PEP8 but doesn't perform the broad rule-based linting flake8/pylint do.
- bandit is a security-focused linter (finds vulnerabilities), not a general style/lint replacement.

</details>

---

**Q5.** A developer wants zero bikeshedding over code style and a formatter that produces identical output for the same input across the whole team, with minimal configuration options. Which tool matches this requirement?

A) yapf with a custom style file
B) autopep8 with --aggressive
C) isort configured to sort imports only
D) black with default settings

<details>
<summary>Answer</summary>

**Correct: D**

black is intentionally 'opinionated' and near-non-configurable — the same input always formats identically, eliminating style debates, which is exactly its design goal.

**Why the others are wrong:**
- yapf is highly configurable, which reintroduces the exact bikeshedding the requirement wants to avoid.
- autopep8 only enforces PEP8 minimally and allows many stylistic variations to remain.
- isort only sorts imports; it doesn't format the rest of the code.

</details>

---

**Q6.** A test module needs a database connection created once before each test function and torn down after, shared across multiple test files in the same package. Which pytest mechanism should be used?

A) A global variable defined at module import time
B) Calling setUp() from unittest.TestCase inside a plain function
C) A @pytest.fixture defined in conftest.py
D) Re-instantiating the connection manually inside every test with copy-pasted code

<details>
<summary>Answer</summary>

**Correct: C**

conftest.py fixtures decorated with @pytest.fixture are pytest's mechanism for shared, reusable setup/teardown that's automatically discovered across test files in the same directory tree.

**Why the others are wrong:**
- Global variables at import time run once for the whole session and don't reset per test, risking test pollution.
- setUp() is a unittest.TestCase method and isn't used in plain pytest-style function tests.
- Copy-pasted manual setup violates DRY and is exactly what fixtures are meant to eliminate — also flagged in code review, not a pytest idiom.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Where should ruff, black, and pytest configuration for a client project be centralized to follow current Python packaging standards?

A) setup.cfg
B) Pipfile
C) requirements.txt
D) pyproject.toml

<details>
<summary>Answer</summary>

**Correct: D**

pyproject.toml (PEP 518/621) is the modern standard config file; ruff, black, and pytest all support [tool.ruff], [tool.black], and [tool.pytest.ini_options] sections there.

**Why the others are wrong:**
- setup.cfg is legacy — still supported by some tools but superseded by pyproject.toml as the standard.
- Pipfile is specific to pipenv for dependency management, not general tool configuration.
- requirements.txt only lists dependency names/versions; it has no configuration syntax for tools.

</details>

---

**Q8.** Inside an except block, what is the primary difference between calling logger.error(msg) and logger.exception(msg)?

A) There is no difference; they are aliases
B) logger.error sends alerts to Slack automatically while logger.exception does not
C) logger.exception automatically includes the full traceback, while logger.error does not unless exc_info=True is passed
D) logger.exception is deprecated in favor of logger.error

<details>
<summary>Answer</summary>

**Correct: C**

logger.exception(msg) is shorthand for logger.error(msg, exc_info=True) — it must be called from within an except block and automatically attaches the traceback for debugging.

**Why the others are wrong:**
- They are not aliases — exc_info behavior differs by default.
- Neither method sends alerts by itself; alerting is configured separately via handlers, not the log level call.
- logger.exception is a standard, actively-used part of the logging module, not deprecated.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

