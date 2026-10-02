## Chapter 2 Cheat Sheet — Production-Grade Python

### Project Structure (Separation of Concerns)
| Layer | Folder | Responsibility |
|---|---|---|
| Transport | `api/` | Route/handler definitions only |
| Business logic | `services/` | Core logic, orchestration |
| Data | `models/` | Schemas, dataclasses, ORM models |
| Shared | `core/` | Config, logging setup, constants |
| Entrypoint | `main.py` | Thin — wires layers together, no logic |

### Error Handling Rules
- Never use bare `except:` — always catch specific exception types.
- Build a custom hierarchy: `AppError(Exception)` → `PaymentAPIError(AppError)`.
- Use `logger.exception(msg)` inside `except` blocks to auto-capture traceback.
- Re-raise after logging unless you're fully handling the failure.
- Fail loudly on unexpected exceptions; fail gracefully (with context) on expected ones.

### Logging Levels (low→high)
| Level | Numeric | Use Case |
|---|---|---|
| DEBUG | 10 | Verbose dev tracing |
| INFO | 20 | Normal operational events |
| WARNING | 30 | Unexpected but recoverable |
| ERROR | 40 | Operation failed |
| CRITICAL | 50 | System-level failure |

`logger.exception()` = `logger.error(msg, exc_info=True)` — only inside `except`.

### Dependency Management
| Tool | Lock file | Dev/Prod separation | Notes |
|---|---|---|---|
| pip + requirements.txt | No (unless pip freeze) | Manual (requirements-dev.txt) | Simple, less reproducible |
| Poetry | `poetry.lock` (auto) | `--group dev` | Standard for reproducible client delivery |

Key commands:
```
poetry add requests
poetry add pytest --group dev
poetry install
python -m venv venv && source venv/bin/activate
```

### Code Quality Tooling
| Tool | Purpose | Config location |
|---|---|---|
| ruff | Fast linting (replaces flake8/pylint) | `[tool.ruff]` in pyproject.toml |
| black | Opinionated auto-formatter | `[tool.black]` |
| pytest | Test runner/fixtures | `[tool.pytest.ini_options]` |
| mypy | Static type checking | `[tool.mypy]` |

Commands:
```
ruff check --fix .
black --check .
pytest -k "pattern" -v
```

### Type Hints & Docstrings
- Always annotate function signatures: `def fetch(id: int) -> dict[str, Any]:`
- Use Google or NumPy docstring style consistently across a project — exam tests recognizing malformed/missing docstrings, not memorizing one style verbatim.
- Run `mypy` in CI to catch type mismatches before runtime.

### Common Exam Traps
- Bare `except:` or `except Exception: pass` = always wrong.
- Unpinned dependencies described as 'reproducible' = wrong.
- setup.cfg / Pipfile chosen over pyproject.toml for new tool config = usually wrong (pyproject.toml is current standard).
- Confusing `logger.error` with `logger.exception` (traceback capture) is a frequently missed distinction.
