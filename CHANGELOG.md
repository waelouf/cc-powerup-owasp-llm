# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2026-02-07

### Added
- Initial release of OWASP LLM Top 10 Security Auditor powerup
- Comprehensive security audit skill for Claude Code resources
- Support for auditing 5 resource types: Skills, Agents, Hooks, Slash Commands, and Prompts
- Detection across all 10 OWASP LLM vulnerability categories:
  - LLM01: Prompt Injection
  - LLM02: Sensitive Information Disclosure
  - LLM03: Supply Chain Vulnerabilities
  - LLM04: Data and Model Poisoning
  - LLM05: Improper Output Handling
  - LLM06: Excessive Agency
  - LLM07: System Prompt Leakage
  - LLM08: Vector and Embedding Weaknesses
  - LLM09: Misinformation
  - LLM10: Unbounded Consumption
- Detailed reference documentation for each vulnerability category
- `audit` mode for vulnerability analysis and reporting
- `fix` mode for automated remediation
- Comprehensive audit report generation with:
  - Executive summary with risk levels
  - Detailed findings per vulnerability
  - Remediation priority lists
  - Actionable recommendations
- Example vulnerable skill for testing
- Example audit report demonstrating output format
- Quick start guide for rapid onboarding
- Plugin metadata for Claude Code Powerups marketplace
- Security best practices and common vulnerability patterns
- Troubleshooting guide

### Documentation
- README.md with comprehensive usage instructions
- QUICKSTART.md for 5-minute setup
- CLAUDE.md for technical architecture and development context
- 10 detailed reference files covering each OWASP LLM vulnerability
- Example audit report and vulnerable skill

[Unreleased]: https://github.com/waelouf/cc-powerup-owasp-llm/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/waelouf/cc-powerup-owasp-llm/releases/tag/v1.0.0
