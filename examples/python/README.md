## Python Project with Ruff Configuration

### Setup for Python Projects

Create a `.mega-linter.yml` file in your Python project root:

```yaml
# .mega-linter.yml for Python projects with Ruff
VALIDATE_ALL_CODEBASE: false
PYTHON_RUFF_ENABLED: true
PYTHON_RUFF_CONFIG_FILE: pyproject.toml
DISABLE: COPYPASTE,SPELL
PYTHON_RUFF_ARGS: "--fix"
```

### Complete Python Project Workflow Example

Create `.github/workflows/lint.yml`:

```yaml
name: MegaLinter Python
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  megalinter:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      issues: write
      pull-requests: write
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run MegaLinter with Ruff
        uses: jgeofil/_mega-linter@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          apply-fixes: 'true'
          apply-fixes-mode: 'commit'
          apply-fixes-event: 'pull_request'

      - name: Upload linting reports
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: megalinter-reports
          path: megalinter-reports/
```

### Python Project Configuration with Ruff in `pyproject.toml`

```toml
[tool.ruff]
line-length = 100
target-version = "py311"

[tool.ruff.lint]
select = [
    "E",      # pycodestyle errors
    "W",      # pycodestyle warnings
    "F",      # pyflakes
    "I",      # isort
    "B",      # flake8-bugbear
    "C4",     # flake8-comprehensions
    "UP",     # pyupgrade
    "ARG",    # flake8-unused-arguments
    "SIM",    # flake8-simplify
]
ignore = [
    "E501",   # line too long (handled by formatter)
]

[tool.ruff.lint.isort]
known-first-party = ["myproject"]

[tool.ruff.per-file-ignores]
"__init__.py" = ["F401"]
"tests/*" = ["ARG001", "ARG002"]
```

### Example: Python Project Structure

```
my_python_project/
├── .mega-linter.yml
├── .github/
│   └── workflows/
│       └── lint.yml
├── pyproject.toml
├── src/
│   └── myproject/
│       ├── __init__.py
│       ├── main.py
│       └── utils.py
├── tests/
│   ├── __init__.py
│   └── test_main.py
└── README.md
```

### Running Locally

To test the linting locally before pushing:

```bash
# Install Ruff
pip install ruff

# Check for linting issues
ruff check .

# Automatically fix issues
ruff check --fix .

# Format your code
ruff format .
```

### What Ruff Checks

With the configuration above, Ruff will check for:
- **E/W**: PEP 8 style violations
- **F**: Undefined names and unused imports
- **I**: Import ordering (via isort integration)
- **B**: Common bugs and design problems
- **C4**: Comprehension improvements
- **UP**: Python version upgrades
- **ARG**: Unused function arguments
- **SIM**: Code simplification opportunities

### Tips for Python Projects

1. **Exclude directories**: Add to `.mega-linter.yml`:
   ```yaml
   PYTHON_RUFF_LINTER_RULES_PATH: .
   ```

2. **Configure per-file ignores**: Different rules for tests vs. source code (already configured in example)

3. **Use with pre-commit hooks**: Add to `.pre-commit-config.yaml`:
   ```yaml
   - repo: https://github.com/astral-sh/ruff-pre-commit
     rev: v0.1.0
     hooks:
       - id: ruff
         args: [--fix]
       - id: ruff-format
   ```
