# OWASP LLM Top 10 Security Auditor Powerup

A comprehensive security audit skill for Claude Code that checks your skills, agents, hooks, slash commands, and prompts against the OWASP LLM Top 10 vulnerability framework.

## What It Does

This skill performs deep security audits of Claude Code resources to identify vulnerabilities across all 10 OWASP LLM security categories:

1. **Prompt Injection** - Detects lack of input validation and prompt manipulation risks
2. **Sensitive Information Disclosure** - Finds hardcoded credentials, API keys, and PII exposure
3. **Supply Chain** - Identifies unverified dependencies and integrity risks
4. **Data and Model Poisoning** - Checks for untrusted data sources and validation gaps
5. **Improper Output Handling** - Finds XSS, CSRF, and RCE vulnerabilities
6. **Excessive Agency** - Detects over-permissioned tools and missing approval gates
7. **System Prompt Leakage** - Identifies sensitive info in prompts and misplaced security controls
8. **Vector and Embedding Weaknesses** - Checks RAG access controls and data isolation
9. **Misinformation** - Verifies fact-checking mechanisms and verification requirements
10. **Unbounded Consumption** - Detects missing rate limits and resource controls

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

## Audit Report Format

The skill generates comprehensive security audit reports:

```markdown
# OWASP LLM Top 10 Security Audit Report

**Resource**: /path/to/resource
**Type**: Skill
**Date**: 2026-02-06
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
- No input validation on user-provided arguments
- Missing prompt injection guards

**Impact**: Attacker could manipulate prompts to bypass security controls

**Recommendation**: Add input validation and sanitization for all args

---

[... continues for all 10 vulnerabilities ...]

---

## Remediation Priority

1. **Critical** (Fix Immediately):
   - LLM01: Add input validation
   - LLM02: Remove hardcoded API key on line 45

2. **High** (Fix This Week):
   - LLM06: Require human approval for destructive operations
   - LLM10: Add rate limiting

3. **Medium** (Fix This Month):
   - LLM09: Add output verification mechanisms

---

## Next Steps

Run with `fix` mode to automatically remediate issues:
/owasp-llm-10 fix /path/to/resource
```

## What Gets Checked Per Resource Type

### Skills (SKILL.md)
- Input validation in args
- Hardcoded secrets
- Tool access permissions
- System prompt security
- Output verification
- Resource limits

### Agents/Subagents
- System prompt injection defenses
- Credential management
- Least privilege principle
- RAG access controls
- Resource limits

### Hooks
- Dependency verification
- Output sanitization
- System access restrictions
- Resource consumption

### Slash Commands
- Input validation
- Secret exposure
- Output handling
- Instruction security

### Prompts
- Anti-injection instructions
- Embedded credentials
- Security control placement
- Verification requirements

## Best Practices

1. **Run audits regularly** - Audit your resources after major changes
2. **Fix critical issues first** - Follow the remediation priority list
3. **Review fixes** - Always review automated fixes before deploying
4. **Test thoroughly** - Test resources after applying fixes
5. **Document changes** - Keep an audit trail for compliance

## Reference Materials

All OWASP LLM Top 10 vulnerability references are included in:
```
~/.claude/skills/owasp-llm-10/references/
```

- `owasp-llm01-prompt-injection.md`
- `owasp-llm02-sensitive-information-disclosure.md`
- `owasp-llm03-supply-chain.md`
- `owasp-llm04-data-model-poisoning.md`
- `owasp-llm05-improper-output-handling.md`
- `owasp-llm06-excessive-agency.md`
- `owasp-llm07-system-prompt-leakage.md`
- `owasp-llm08-vector-embedding-weaknesses.md`
- `owasp-llm09-misinformation.md`
- `owasp-llm10-unbounded-consumption.md`

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

1. Add examples to the reference files
2. Update the SKILL.md with new detection patterns
3. Test on various resource types
4. Document in README.md

## License

This skill is based on the OWASP LLM Top 10 framework (https://owasp.org/www-project-top-10-for-large-language-model-applications/)

## Support

For issues or questions:
- Check the reference materials in `/references/`
- Review example audit reports
- Test on the provided examples

---

**Remember**: Security is not a one-time check. Audit regularly and keep your resources secure!
