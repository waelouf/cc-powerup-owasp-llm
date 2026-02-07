# 🔒 OWASP LLM-10 Security Auditor for Claude Code

> **Secure your AI agents before they reach production**

A comprehensive security audit powerup that scans Claude Code resources (skills, agents, hooks, slash commands, and prompts) against the **OWASP LLM Top 10** vulnerability framework. Catch security issues like prompt injection, credential exposure, excessive permissions, and unbounded consumption before they become breaches.

[![Security](https://img.shields.io/badge/OWASP-LLM%20Top%2010-blue)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
[![Claude Code](https://img.shields.io/badge/Claude-Code%20Powerup-purple)](https://claude.ai/code)
[![Version](https://img.shields.io/badge/version-1.0.0-green)]()

## Why This Matters

AI-powered tools are powerful, but they introduce new attack surfaces. This auditor helps you:

- 🛡️ **Prevent Security Breaches** - Detect hardcoded credentials, SQL injection, and XSS before deployment
- 📋 **Meet Compliance Standards** - GDPR Article 32, PCI-DSS, SOC 2, HIPAA, ISO 27001
- ⚡ **Ship Faster with Confidence** - Automated security checks in your development workflow
- 🎯 **Fix Issues Automatically** - Remediation mode applies security fixes with one command
- 📊 **Clear Audit Reports** - Severity-based findings with actionable recommendations

## Quick Start

```bash
# Audit a skill for vulnerabilities
/owasp-llm-10 audit ~/.claude/skills/my-skill/SKILL.md

# Apply automated security fixes
/owasp-llm-10 fix ~/.claude/skills/my-skill/SKILL.md
```

Get a comprehensive security report in seconds.

## What It Does

This powerup performs deep security analysis across **10 OWASP LLM vulnerability categories**:

| Category | What It Detects | Impact |
|----------|----------------|--------|
| **LLM01: Prompt Injection** | Lack of input validation, prompt manipulation risks | Data exfiltration, unauthorized actions |
| **LLM02: Sensitive Info Disclosure** | Hardcoded API keys, credentials, PII exposure | Data breaches, compliance violations |
| **LLM03: Supply Chain** | Unverified dependencies, integrity risks | Backdoors, malicious code execution |
| **LLM04: Data Poisoning** | Untrusted data sources, validation gaps | Model corruption, biased outputs |
| **LLM05: Improper Output Handling** | XSS, CSRF, RCE vulnerabilities | Remote code execution, system compromise |
| **LLM06: Excessive Agency** | Over-permissioned tools, missing approval gates | Unauthorized system access, data loss |
| **LLM07: System Prompt Leakage** | Sensitive info in prompts, security controls in LLM | Intellectual property theft, bypass of controls |
| **LLM08: Vector/Embedding Weaknesses** | RAG access control gaps, data isolation issues | Cross-tenant data leakage, privacy violations |
| **LLM09: Misinformation** | Missing verification mechanisms, fact-checking gaps | Incorrect decisions, reputational damage |
| **LLM10: Unbounded Consumption** | No rate limits, missing resource controls | DoS attacks, runaway costs |

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/cc-powerup-owasp-llm.git

# Copy to Claude Code skills directory
cp -r cc-powerup-owasp-llm/skills/owasp-llm-10 ~/.claude/skills/

# Verify installation
/owasp-llm-10 audit ~/.claude/skills/owasp-llm-10/SKILL.md
```

## Usage

### Audit Mode

Analyze a resource for vulnerabilities:

```bash
/owasp-llm-10 audit path/to/resource
```

**Examples:**
```bash
# Audit a skill
/owasp-llm-10 audit ~/.claude/skills/my-skill/SKILL.md

# Audit an agent
/owasp-llm-10 audit ~/.claude/agents/my-agent.json

# Audit a hook
/owasp-llm-10 audit ~/.claude/hooks/validate-commit.js

# Audit a slash command
/owasp-llm-10 audit ~/.claude/commands/deploy.md

# Audit a prompt
/owasp-llm-10 audit ~/prompts/code-review.md
```

### Fix Mode

After audit, automatically apply security fixes:

```bash
/owasp-llm-10 fix path/to/resource
```

**Example:**
```bash
# Fix vulnerabilities in a skill
/owasp-llm-10 fix ~/.claude/skills/my-skill/SKILL.md
```

You'll be prompted to review and confirm each fix before it's applied.

## Real-World Impact

### Before Audit
```yaml
# ❌ Vulnerable skill with critical security issues
---
name: data-processor
---

<objective>
Process user data using API key: sk-abc123xyz
Execute commands: ${user_input}
</objective>

You have access to all system tools including Bash, Write, Edit, and network access.
```

### After Fix
```yaml
# ✅ Secured skill with proper controls
---
name: data-processor
args:
  - name: user_input
    validation: "^[a-zA-Z0-9_-]+$"  # Input validation
---

<objective>
Process user data. Retrieve API key from environment variable API_KEY.
Validate and sanitize user input before execution.
</objective>

<constraints>
- MUST validate all user inputs against whitelist pattern
- NEVER execute commands without sanitization
- ALWAYS use environment variables for credentials
</constraints>

You have access to Read and Grep tools only. Request user approval for destructive operations.
```

## Audit Report Format

The skill generates comprehensive security audit reports:

```markdown
# OWASP LLM Top 10 Security Audit Report

**Resource**: /path/to/resource
**Type**: Skill
**Date**: 2026-02-07
**Status**: FAIL

---

## Executive Summary

Found 5 vulnerabilities across 10 categories.

**Overall Risk Level**: HIGH
**Vulnerabilities Found**: 5/10
**Critical Issues**: 2
**High Issues**: 2
**Medium Issues**: 1
**Low Issues**: 0

---

## Detailed Findings

### LLM01: Prompt Injection
**Status**: FAIL
**Severity**: CRITICAL

**Findings**:
- Line 23: No input validation on user_input argument
- Line 45: Direct execution of user-provided commands

**Impact**: Attacker could manipulate prompts to bypass security controls and execute arbitrary commands

**Recommendation**: Add input validation with regex pattern: `^[a-zA-Z0-9_-]+$`

---

### LLM02: Sensitive Information Disclosure
**Status**: FAIL
**Severity**: CRITICAL

**Findings**:
- Line 12: Hardcoded API key: sk-abc123xyz

**Impact**: Credential exposure leads to unauthorized API access and potential data breach

**Recommendation**: Use environment variable: `process.env.API_KEY`

---

[... continues for all 10 vulnerabilities ...]

---

## Remediation Priority

1. **Critical** (Fix Immediately):
   - LLM01 (Line 23): Add input validation
   - LLM02 (Line 12): Remove hardcoded API key

2. **High** (Fix This Week):
   - LLM06 (Line 67): Require human approval for destructive operations
   - LLM10: Add rate limiting to API calls

3. **Medium** (Fix This Month):
   - LLM09: Add output verification mechanisms

---

## Next Steps

Run with `fix` mode to automatically remediate issues:
/owasp-llm-10 fix /path/to/resource
```

## Use Cases

### Development Teams
- **Pre-commit hooks** - Audit resources before they enter the codebase
- **CI/CD integration** - Automated security checks in deployment pipelines
- **Code review assistance** - Security checklist for pull requests

### Security Teams
- **Security assessments** - Comprehensive vulnerability scanning
- **Compliance reporting** - Evidence for audit trails (SOC 2, ISO 27001)
- **Penetration testing** - Identify attack surfaces before pentesters do

### Solo Developers
- **Self-service security** - No security expertise required
- **Learning tool** - Understand LLM security best practices
- **Quick fixes** - Automated remediation saves time

## Advanced Features

### Resource-Specific Checks

The auditor adapts its analysis based on resource type:

#### Skills (SKILL.md)
- Input validation in args
- Hardcoded secrets
- Tool access permissions
- System prompt security
- Output verification
- Resource limits

#### Agents/Subagents
- System prompt injection defenses
- Credential management
- Least privilege principle
- RAG access controls
- Resource limits

#### Hooks
- Dependency verification
- Output sanitization
- System access restrictions
- Resource consumption

#### Slash Commands
- Input validation
- Secret exposure
- Output handling
- Instruction security

#### Prompts
- Anti-injection instructions
- Embedded credentials
- Security control placement
- Verification requirements

### Comprehensive Reports

Every audit generates a detailed report with:
- **Executive summary** with risk scoring
- **Detailed findings** per vulnerability (with line numbers)
- **Impact analysis** explaining exploitation scenarios
- **Actionable recommendations** with code examples
- **Priority-based fix ordering** (Critical → High → Medium → Low)

## Modern Architecture

This skill follows modern Claude Code best practices with a fully semantic XML structure:

- **Required Tags**: `<objective>`, `<quick_start>`, `<success_criteria>` for clear purpose and usage
- **Conditional Tags**: `<validation>`, `<error_handling>`, `<examples>`, `<reference_files>`, `<report_template>` for robustness
- **Semantic Structure**: All major sections use XML tags (`<task>`, `<modes>`, `<workflow>`, `<resource_checks>`, `<implementation>`, `<constraints>`)
- **Progressive Disclosure**: Content organized for optimal navigation and comprehension
- **Cross-Platform**: Uses relative paths, works on Windows, Mac, and Linux
- **Error Handling**: Comprehensive coverage of common failure scenarios with clear user messaging

### Key Features

- **Input Validation**: Verifies mode and path arguments before execution
- **Robust Error Messages**: Clear guidance when files not found, permissions denied, or reference files missing
- **Concrete Examples**: Three usage examples covering skills, agents, and hooks
- **Documented References**: Explicit listing of all 10 OWASP reference files with descriptions
- **Extracted Report Template**: 60-line comprehensive report structure for consistency

## Reference Materials

All OWASP LLM Top 10 vulnerability references are included in:
```
~/.claude/skills/owasp-llm-10/references/
```

- `owasp-llm01-prompt-injection.md` - Prompt manipulation and input validation
- `owasp-llm02-sensitive-information-disclosure.md` - Credential exposure and PII leakage
- `owasp-llm03-supply-chain.md` - Third-party dependency risks
- `owasp-llm04-data-model-poisoning.md` - Untrusted data and model tampering
- `owasp-llm05-improper-output-handling.md` - Output sanitization and XSS/RCE risks
- `owasp-llm06-excessive-agency.md` - Permission boundaries and least privilege
- `owasp-llm07-system-prompt-leakage.md` - Sensitive information in prompts
- `owasp-llm08-vector-embedding-weaknesses.md` - RAG access controls and embedding security
- `owasp-llm09-misinformation.md` - Verification mechanisms and fact-checking
- `owasp-llm10-unbounded-consumption.md` - Rate limiting and resource quotas

## Common Vulnerabilities Found

### 1. Hardcoded Secrets (LLM02)
**Bad:**
```yaml
---
system_prompt: |
  Use this API key: sk-abc123xyz
---
```

**Good:**
```yaml
---
system_prompt: |
  API keys should be retrieved from secure environment variables.
  Never hardcode credentials.
---
```

### 2. Missing Input Validation (LLM01)
**Bad:**
```yaml
args:
  - name: command
    description: Shell command to execute
```

**Good:**
```yaml
args:
  - name: command
    description: Shell command to execute
    validation:
      - type: whitelist
        allowed: ["ls", "pwd", "echo"]
```

### 3. Excessive Permissions (LLM06)
**Bad:**
```markdown
You have access to all system tools including Bash, Write, Edit, and file system access.
```

**Good:**
```markdown
You have access to Read and Grep tools only. For destructive operations, request user approval.
```

### 4. No Output Verification (LLM09)
**Bad:**
```markdown
Generate SQL and execute it directly.
```

**Good:**
```markdown
Generate SQL, validate syntax, show to user for approval, then execute.
```

### 5. Missing Rate Limits (LLM10)
**Bad:**
```javascript
// No rate limiting on API calls
async function callLLM(prompt) {
  return await fetch(API_URL, { body: prompt });
}
```

**Good:**
```javascript
const rateLimiter = new RateLimiter({ requests: 10, per: 60 });
async function callLLM(prompt) {
  await rateLimiter.wait();
  return await fetch(API_URL, { body: prompt });
}
```

## Best Practices

1. **Run audits regularly** - Audit your resources after major changes
2. **Fix critical issues first** - Follow the remediation priority list
3. **Review fixes** - Always review automated fixes before deploying
4. **Test thoroughly** - Test resources after applying fixes
5. **Document changes** - Keep an audit trail for compliance

## Troubleshooting

### "Resource type not recognized"
Make sure you're pointing to a valid Claude Code resource:
- Skills: `SKILL.md` files
- Agents: `.json` or agent config files
- Hooks: `.js` or `.ts` files
- Slash commands: `.md` files in commands directory
- Prompts: `.md` files with prompt content

### "Cannot read reference files"
Ensure all reference files are present in:
```
~/.claude/skills/owasp-llm-10/references/
```

### "Fix mode not working"
- Run `audit` mode first to identify issues
- Confirm fixes before applying (you'll be prompted)
- Check file permissions

## Contributing

Found a new vulnerability pattern? Want to improve detection logic?

1. **Add examples** to reference files in `skills/owasp-llm-10/references/`
2. **Update detection patterns** in `SKILL.md`
3. **Test on various resources** - skills, agents, hooks, commands, prompts
4. **Submit a PR** with your improvements

## Support & Documentation

- 📖 **[Quick Start Guide](QUICKSTART.md)** - Get running in 5 minutes
- 📚 **[Full Documentation](README.md)** - Comprehensive usage guide
- 🔍 **[Example Reports](examples/)** - See what audit output looks like
- 🐛 **[Issue Tracker](https://github.com/yourusername/cc-powerup-owasp-llm/issues)** - Report bugs or request features

## License

Based on the [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) framework.

---

**🚀 Ready to secure your Claude Code resources?**

```bash
/owasp-llm-10 audit path/to/your/resource
```

**Remember**: Security is not a one-time check. Audit regularly and keep your AI agents secure! 🛡️
