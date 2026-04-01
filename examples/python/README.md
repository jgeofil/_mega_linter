# Python Project with Ruff Configuration

### Setup for Python Projects

Create a `.mega-linter.yml` file in your Python project root:

```yaml
# .mega-linter.yml for Python projects with Ruff
VALIDATE_ALL_CODEBASE: false
PYTHON_RUFF_ENABLED: true
PYTHON_RUFF_CONFIG_FILE: pyproject.toml
DISABLE: COPYPASTE,SPELL

# Optional: Configure Ruff-specific settings
PYTHON_RUFF_CLI_LINT_MODE: projects
PYTHON_RUFF_ARGS: "--fix"
```
