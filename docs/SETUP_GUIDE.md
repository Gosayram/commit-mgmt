# Setup Guide

This guide provides detailed instructions for setting up and using the commit management tools in your projects.

## Prerequisites

### System Requirements

- Git version 2.0 or higher
- Python 3.6 or higher (for pre-commit framework)
- Bash shell (for commit message validation script)

### Installing Pre-commit

#### macOS
```bash
# Using Homebrew
brew install pre-commit

# Using pip
pip install pre-commit
```

#### Linux (Ubuntu/Debian)
```bash
# Using pip
pip install pre-commit

# Using apt (if available)
sudo apt install pre-commit
```

#### Windows
```bash
# Using pip
pip install pre-commit

# Using chocolatey
choco install pre-commit
```

### Verify Installation
```bash
pre-commit --version
```

## Project Setup

### Step 1: Create Pre-commit Configuration

Create a `.pre-commit-config.yaml` file in your project root:

```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main  # or specific version tag
    hooks:
      - id: commit-msg-format
```

### Step 2: Install Hooks

```bash
# Install commit-msg hook
pre-commit install --hook-type commit-msg

# Install pre-commit hook (if you have other hooks)
pre-commit install

# Install all hook types
pre-commit install --install-hooks
```

### Step 3: Test Setup

Test with a sample commit message:

```bash
# Create a test file
echo "test" > test.txt
git add test.txt

# Try committing with correct format
git commit -m "[TEST] - verify commit message validation"

# Try committing with incorrect format (should fail)
git commit -m "invalid commit message"
```

## Advanced Configuration

### Using Specific Versions

For production environments, always pin to specific versions:

```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: v1.0.0  # specific version tag
    hooks:
      - id: commit-msg-format
```

### Combining with Other Hooks

```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main
    hooks:
      - id: commit-msg-format

  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
```

### Language-Specific Hooks

#### Python Projects
```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main
    hooks:
      - id: commit-msg-format

  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black

  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort
```

#### JavaScript/TypeScript Projects
```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main
    hooks:
      - id: commit-msg-format

  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.0.0
    hooks:
      - id: prettier
```

#### Go Projects
```yaml
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main
    hooks:
      - id: commit-msg-format

  - repo: https://github.com/tekwizely/pre-commit-golang
    rev: v1.0.0-beta.5
    hooks:
      - id: go-fmt
      - id: go-imports
      - id: go-vet-mod
```

## Team Setup

### Repository Template

Create a template repository with pre-configured `.pre-commit-config.yaml`:

1. Create a new repository or use existing template
2. Add `.pre-commit-config.yaml` with your organization's standards
3. Include setup instructions in README
4. Add to organization templates

### CI/CD Integration

#### GitHub Actions

Create `.github/workflows/pre-commit.yml`:

```yaml
name: Pre-commit

on:
  pull_request:
  push:
    branches: [main]

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - uses: pre-commit/action@v3.0.0
```

#### GitLab CI

Add to `.gitlab-ci.yml`:

```yaml
pre-commit:
  image: python:3.9
  stage: test
  before_script:
    - pip install pre-commit
  script:
    - pre-commit run --all-files
```

## Migration from Local Scripts

### Step 1: Remove Local Scripts

If you were using local commit message validation:

```bash
# Remove local script
rm scripts/check-commit-msg.sh

# Update .pre-commit-config.yaml
# Remove local repo configuration
# Add remote repo configuration
```

### Step 2: Update Configuration

Replace local repo configuration:

```yaml
# OLD - Local configuration
repos:
  - repo: local
    hooks:
      - id: custom-commit-msg
        name: Custom Commit Format
        entry: scripts/check-commit-msg.sh
        language: script
        stages: [commit-msg]

# NEW - Remote configuration
repos:
  - repo: https://github.com/Gosayram/commit-mgmt
    rev: main
    hooks:
      - id: commit-msg-format
```

### Step 3: Reinstall Hooks

```bash
# Uninstall old hooks
pre-commit uninstall

# Install new hooks
pre-commit install --hook-type commit-msg
```

## Troubleshooting Setup

### Common Issues

#### Hook Not Running
```bash
# Check if hooks are installed
ls -la .git/hooks/

# Reinstall hooks
pre-commit install --hook-type commit-msg
```

#### Permission Errors
```bash
# Fix file permissions
chmod +x .git/hooks/commit-msg
```

#### Network Issues
```bash
# Update hooks manually
pre-commit autoupdate

# Clear cache
pre-commit clean
```

#### Version Conflicts
```bash
# Check current configuration
pre-commit --version

# Update pre-commit
pip install --upgrade pre-commit
```

### Debugging

#### Test Hook Manually
```bash
# Test specific hook
pre-commit run commit-msg-format --hook-stage commit-msg

# Test with sample message
echo "[TEST] - sample message" | pre-commit run commit-msg-format --hook-stage commit-msg
```

#### Verbose Output
```bash
# Run with verbose output
pre-commit run --verbose commit-msg-format --hook-stage commit-msg
```

#### Check Configuration
```bash
# Validate configuration file
pre-commit validate-config

# Show configuration
cat .pre-commit-config.yaml
```

## Best Practices

### Version Management
- Always pin to specific versions in production
- Test new versions in development environments first
- Use semantic versioning for your own pre-commit configurations

### Team Adoption
- Document setup process in your README
- Provide example configurations for different project types
- Include troubleshooting steps for common issues
- Consider organization-wide pre-commit configuration templates

### Maintenance
- Regularly update hook versions
- Monitor hook performance impact
- Review and update commit message standards as needed
- Collect feedback from team members 