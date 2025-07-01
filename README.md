# Commit Management Tools

A centralized repository for commit message validation and management tools that can be used across multiple projects.

## Features

- **Commit Message Validation**: Ensures consistent commit message formatting across projects
- **Dual Format Support**: Supports both custom `[TYPE] - description` and conventional commits format
- **Pre-commit Integration**: Easy integration with pre-commit framework
- **Centralized Management**: No need to copy scripts to individual projects

## Supported Commit Message Formats

### Format 1: Custom Format
```
[TYPE] - description
```

**Allowed Types:**
- `ADD` - Adding new features or functionality
- `CI` - Continuous integration changes
- `FEATURE` - New feature implementation
- `BUGFIX` - Bug fixes
- `FIX` - General fixes
- `INIT` - Initial setup or initialization
- `DOCS` - Documentation changes
- `TEST` - Test-related changes
- `REFACTOR` - Code refactoring
- `STYLE` - Code style changes
- `CHORE` - Maintenance tasks

**Examples:**
```
[ADD] - user authentication system
[FIX] - resolve database connection timeout
[DOCS] - update API documentation
```

### Format 2: Conventional Commits
```
type: description
type(scope): description
```

**Allowed Types:**
- `feat` - New features
- `fix` - Bug fixes
- `docs` - Documentation changes
- `style` - Code style changes
- `refactor` - Code refactoring
- `test` - Test changes
- `chore` - Maintenance tasks
- `ci` - CI/CD changes
- `build` - Build system changes
- `perf` - Performance improvements
- `revert` - Revert changes

**Examples:**
```
feat: add user authentication system
fix(database): resolve connection timeout
docs: update API documentation
chore: update dependencies to latest versions
```

## Usage in Your Projects

### Prerequisites

1. Install [pre-commit](https://pre-commit.com/):
   ```bash
   pip install pre-commit
   # or
   brew install pre-commit
   ```

### Setup

1. Create or update `.pre-commit-config.yaml` in your project root:

   ```yaml
   repos:
     # Commit message validation from centralized repository
     - repo: https://github.com/Gosayram/commit-mgmt
       rev: main  # Use specific version tag in production
       hooks:
         - id: commit-msg-format

     # Other hooks (optional examples)
     - repo: https://github.com/pre-commit/pre-commit-hooks
       rev: v4.4.0
       hooks:
         - id: trailing-whitespace
         - id: end-of-file-fixer
         - id: check-yaml
         - id: check-json
   ```

2. Install the pre-commit hooks:
   ```bash
   pre-commit install --hook-type commit-msg
   ```

3. Test the setup (optional):
   ```bash
   pre-commit run --hook-stage commit-msg --all-files
   ```

### Using Specific Versions

For production environments, it's recommended to pin to specific versions:

```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: v1.0.2  # Use specific version tag
    hooks:
      - id: commit-msg-format
```

## Testing Commit Messages

You can test commit messages manually using the script:

```bash
# Clone this repository
git clone https://github.com/Gosayram/commit-mgmt.git
cd commit-mgmt

# Test a commit message
echo "[ADD] - new feature implementation" | ./scripts/check-commit-msg.sh /dev/stdin

# Test conventional commit format
echo "feat: add new feature implementation" | ./scripts/check-commit-msg.sh /dev/stdin
```

## Development

### Local Testing

To test changes locally before pushing:

1. Create a test commit message file:
   ```bash
   echo "[TEST] - testing commit validation" > test_commit.txt
   ```

2. Run the validation script:
   ```bash
   ./scripts/check-commit-msg.sh test_commit.txt
   ```

### Contributing

1. Follow the commit message format defined in this repository
2. Ensure all scripts are executable (`chmod +x`)
3. Test changes locally before submitting pull requests
4. Update documentation for any new features or changes

## Troubleshooting

### Common Issues

1. **Permission Denied Error**
   ```bash
   chmod +x scripts/check-commit-msg.sh
   ```

2. **Pre-commit Not Found**
   ```bash
   pip install pre-commit
   # or
   brew install pre-commit
   ```

3. **Hook Not Running**
   ```bash
   pre-commit install --hook-type commit-msg
   ```

4. **Testing Hook Manually**
   ```bash
   pre-commit run commit-msg-format --hook-stage commit-msg
   ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Automated Releases

This repository uses GitHub Actions to automatically create releases when changes are made to:

- `scripts/` directory (commit message validation script)
- `.pre-commit-hooks.yaml` file

### Release Versioning

The release workflow automatically determines the next version based on commit messages:

- **Major version** (v1.0.0 → v2.0.0): Breaking changes (commits with `!` or `BREAKING CHANGE`)
- **Minor version** (v1.0.0 → v1.1.0): New features (`feat`, `feature`, `[ADD]`, `[FEATURE]`)
- **Patch version** (v1.0.0 → v1.0.1): Bug fixes, documentation, and other changes

### Version History

Each release includes:
- Automatically generated release notes with recent commits
- Installation instructions for the specific version
- Links to documentation and examples

## Documentation

- [Setup Guide](docs/SETUP_GUIDE.md) - Detailed setup instructions
- [Changelog](docs/CHANGELOG.md) - Version history and changes  
- [Example Configuration](example.pre-commit-config.yaml) - Ready-to-use pre-commit config

## Support

For issues, questions, or contributions, please open an issue in this repository. 