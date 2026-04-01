# Mega Linter

## Features Overview
- Linter for multiple languages
- Easy configuration
- Support for multiple file types
- Customizable rules

## Usage Examples
1. **Basic Usage**: Run the linter on your project files:
   ```bash
   npx mega-linter
   ```
2. **Create a Pull Request with Fixes**:
   ```bash
   npx mega-linter --fix
   ```
3. **Disable Auto-Fixes**:
   ```bash
   npx mega-linter --no-fix
   ```

## Input Parameters Table
| Parameter                | Description                     |
|--------------------------|---------------------------------|
| `--fix`                  | Automatically fix issues        |
| `--no-fix`               | Run linter without fixing issues|
| `--verbose`              | Show detailed output            |

## Configuration Instructions
1. Create a `.mega-linter.yml` file in your project folder.
2. Define your settings in the configuration file.
3. Customize rules and plugins as required.

## Permissions Required
- Read access to the source files.
- Write access to create a PR with fixes.

## Artifacts Information
- Linter outputs to the terminal.
- If configured, generates a report file in your project directory.

## Multiple Usage Examples for Different Scenarios
### Basic Usage:
- Simply run the command in your project directory to check for linting issues.

### Create PR with Fixes:
- Use `npx mega-linter --fix` to apply automatic fixes and create a pull request.

### Disable Auto-Fixes:
- Run `npx mega-linter --no-fix` to lint the files without applying any changes.

## Additional Resources
- [Official Documentation](https://github.com/oxisto/mega-linter)
- [Community Support](https://community.mega-linter.io)

---

To make this action available for reuse:

1. **Create a release tag**:
   ```bash
   git tag v1
   git push origin v1
   ```

2. **Use it in any project**:
   ```yaml
   - uses: jgeofil/_mega-linter@v1
     with:
       github-token: ${{ secrets.GITHUB_TOKEN }}
   ```
3. **Commit fixes**
   ```yaml
   - uses: jgeofil/_mega-linter@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    apply-fixes: 'true'
    apply-fixes-mode: 'commit'
    ```
