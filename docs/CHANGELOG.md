# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial commit message validation script supporting both custom `[TYPE] - description` and conventional commits formats
- Pre-commit hooks configuration for centralized repository usage  
- Comprehensive documentation and setup guides
- Example configurations for different project types
- Automated GitHub releases via GitHub Actions workflow
- Universal .cursorrules for development best practices across all projects

### Enhanced
- GitHub Actions workflow with pinned versions using SHA commitments for security
- Automatic semantic versioning based on commit message patterns
- Release notes generation with recent commit history

### Technical Details
- Bash script for commit message validation with dual format support
- Pre-commit hooks integration for external repository usage
- Documentation structure following professional standards with docs/ directory organization 