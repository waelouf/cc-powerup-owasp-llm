# OWASP LLM-10 Quick Start Guide

Get started with the OWASP LLM Top 10 security auditor in 5 minutes.

## Installation

The skill is already installed at:
```
C:\Users\waelo\.claude\skills\owasp-llm-10\
```

## Basic Usage

### 1. Audit a Skill

```bash
/owasp-llm-10 audit ~/.claude/skills/my-skill/SKILL.md
```

This will:
- Scan the skill for all 10 OWASP LLM vulnerabilities
- Generate a comprehensive audit report
- Provide pass/fail status for each vulnerability
- Give actionable recommendations

### 2. Fix Vulnerabilities

After auditing, apply automated fixes:

```bash
/owasp-llm-10 fix ~/.claude/skills/my-skill/SKILL.md
```

You'll be asked to confirm fixes before they're applied.

## Quick Test

Try the skill on the example vulnerable skill:

```bash
/owasp-llm-10 audit ~/.claude/skills/owasp-llm-10/examples/vulnerable-skill-example.md
```

You'll see a report showing 8 vulnerabilities with detailed findings.

## What to Look For

The skill checks for these critical issues:

### 🔴 Critical Issues

1. **Hardcoded Credentials** (LLM02)
   - API keys, passwords, tokens in code
   - **Fix**: Use environment variables

2. **No Input Validation** (LLM01)
   - Direct execution of user input
   - **Fix**: Add sanitization and validation

3. **SQL Injection** (LLM05)
   - Direct SQL execution without parameterization
   - **Fix**: Use parameterized queries

4. **Excessive Permissions** (LLM06)
   - Unrestricted tool access
   - **Fix**: Apply least privilege

### 🟠 High Priority

5. **System Prompt Leakage** (LLM07)
   - Sensitive info in prompts
   - **Fix**: Externalize sensitive data

6. **No Output Sanitization** (LLM05)
   - Raw LLM outputs executed directly
   - **Fix**: Validate and sanitize outputs

7. **No Rate Limiting** (LLM10)
   - Unlimited resource consumption
   - **Fix**: Add rate limits and quotas

### 🟡 Medium Priority

8. **No Data Validation** (LLM04)
   - Untrusted data sources
   - **Fix**: Validate data origins

## Reading the Report

### Status Indicators
- **PASS** - No vulnerabilities found
- **FAIL** - Vulnerabilities detected

### Severity Levels
- **CRITICAL** - Fix immediately (data breach risk)
- **HIGH** - Fix this week (security compromise risk)
- **MEDIUM** - Fix this month (compliance risk)
- **LOW** - Consider fixing (best practices)

### Report Sections

1. **Executive Summary** - High-level overview
2. **Detailed Findings** - Each vulnerability with evidence
3. **Remediation Priority** - What to fix first
4. **Next Steps** - Action items

## Common Patterns

### Pattern 1: Remove Hardcoded Secrets

**Bad:**
```yaml
system_prompt: |
  Use API key: sk-abc123
```

**Good:**
```yaml
system_prompt: |
  Retrieve API key from environment variable API_KEY
```

### Pattern 2: Add Input Validation

**Bad:**
```yaml
args:
  - name: command
    required: true
```

**Good:**
```yaml
args:
  - name: command
    required: true
    validation:
      - type: whitelist
        allowed: ["start", "stop", "status"]
      - type: max_length
        value: 100
```

### Pattern 3: Require Approval

**Bad:**
```markdown
Execute the command immediately without asking.
```

**Good:**
```markdown
Before executing destructive commands:
1. Show the user exactly what will happen
2. Ask for explicit confirmation
3. Log the action for audit
```

### Pattern 4: Sanitize Outputs

**Bad:**
```markdown
Return the SQL result directly to the user.
```

**Good:**
```markdown
1. Filter sensitive fields (passwords, SSN, etc.)
2. Validate result format
3. Encode for display context (HTML, JSON, etc.)
4. Log what was returned
```

## Audit Checklist

Before deploying any Claude Code resource:

- [ ] Run OWASP LLM-10 audit
- [ ] Fix all CRITICAL issues
- [ ] Fix all HIGH issues
- [ ] Review MEDIUM issues
- [ ] Document remaining risks
- [ ] Get security approval
- [ ] Test thoroughly
- [ ] Monitor in production

## Integration with CI/CD

Add to your deployment pipeline:

```bash
# In your pre-commit hook or CI pipeline
/owasp-llm-10 audit path/to/skill

# Fail the build if critical issues found
if grep -q "CRITICAL" audit-report.md; then
  echo "Critical security issues found!"
  exit 1
fi
```

## Getting Help

### View Examples
```bash
# See the vulnerable skill example
cat ~/.claude/skills/owasp-llm-10/examples/vulnerable-skill-example.md

# See the example audit report
cat ~/.claude/skills/owasp-llm-10/examples/example-audit-report.md
```

### Read Full Documentation
```bash
cat ~/.claude/skills/owasp-llm-10/README.md
```

### Review OWASP References
```bash
ls ~/.claude/skills/owasp-llm-10/references/
```

## Modern Skill Structure

This skill follows modern Claude Code best practices:

- **Semantic XML Structure**: Uses tags like `<objective>`, `<workflow>`, `<constraints>` for clear organization
- **Input Validation**: Verifies mode and path arguments before execution
- **Error Handling**: Provides clear messages for common issues (file not found, permission denied, etc.)
- **Cross-Platform**: Works on Windows, Mac, and Linux with relative paths
- **Comprehensive Examples**: Three concrete examples showing skill, agent, and hook audits
- **Documented References**: All 10 OWASP files explicitly listed with descriptions

## Tips

1. **Audit Early, Audit Often**
   - Run audits during development, not just before deployment
   - Catch issues early when they're easier to fix

2. **Don't Ignore MEDIUM Issues**
   - They can become HIGH/CRITICAL in certain contexts
   - Consider your specific threat model

3. **Review Automated Fixes**
   - Always review changes before committing
   - Fixes are suggestions, not guarantees

4. **Keep References Updated**
   - OWASP updates vulnerability definitions
   - Check for updates quarterly

5. **Document Exceptions**
   - If you can't fix something, document why
   - Include compensating controls

## Next Steps

1. **Audit Your Skills**
   ```bash
   /owasp-llm-10 audit ~/.claude/skills/your-skill/SKILL.md
   ```

2. **Fix Critical Issues**
   ```bash
   /owasp-llm-10 fix ~/.claude/skills/your-skill/SKILL.md
   ```

3. **Review and Test**
   - Test the skill after fixes
   - Verify functionality wasn't broken

4. **Set Up Regular Audits**
   - Schedule monthly security reviews
   - Audit after major changes

5. **Train Your Team**
   - Share example reports
   - Review common vulnerabilities
   - Establish secure coding standards

---

**Ready to start?**

```bash
/owasp-llm-10 audit path/to/your/resource
```

**Questions?** Check the full README:
```bash
cat ~/.claude/skills/owasp-llm-10/README.md
```
