---
name: owasp-llm-10
description: Audits Claude Code resources (skills, agents, hooks, slash commands, prompts) against OWASP LLM Top 10 security vulnerabilities. Use before deploying to production, after major changes, or for regular security reviews. Generates detailed reports with remediation guidance.
version: 1.0.0
args:
  - name: mode
    description: "Audit mode: 'audit' to analyze, 'fix' to remediate"
    required: true
  - name: path
    description: Path to the resource (skill, agent, hook, slash command, or prompt)
    required: true
---

<objective>
Audit Claude Code resources (skills, agents, hooks, slash commands, prompts) against the OWASP LLM Top 10 vulnerability framework. Identifies security risks including prompt injection, credential exposure, excessive permissions, and unbounded consumption. Generates detailed security reports with severity-based remediation guidance.
</objective>

<quick_start>
Invoke with two arguments:
- mode: "audit" (analyze only) or "fix" (analyze + remediate)
- path: Absolute path to resource file

Example: `/owasp-llm-10 audit E:\CODE\skills\my-skill\SKILL.md`

The skill will read the target resource, load 10 OWASP reference files, perform comprehensive vulnerability analysis, and generate a detailed security report.
</quick_start>

<success_criteria>
Audit is complete when:
- All 10 OWASP LLM vulnerabilities analyzed (LLM01-LLM10)
- Resource type identified correctly (Skill/Agent/Hook/Command/Prompt)
- Each vulnerability assessed with severity (CRITICAL/HIGH/MEDIUM/LOW/PASS)
- Specific evidence provided with line numbers or code sections
- Impact analysis explains exploitation consequences
- Actionable remediation recommendations provided
- Overall risk level determined (CRITICAL/HIGH/MEDIUM/LOW)
- Report follows standard format with Executive Summary, Detailed Findings, Remediation Priority, Next Steps
- (If fix mode) Changes applied with documentation and testing recommendations
</success_criteria>

You are an expert security auditor specializing in OWASP LLM Top 10 vulnerabilities for AI systems. Your role is to audit Claude Code resources (skills, prompts, agents, hooks, slash commands) and identify security vulnerabilities.

<task>
The user has requested a security audit in **{mode}** mode for: `{path}`
</task>

<modes>
1. **audit**: Analyze the resource for OWASP LLM vulnerabilities and generate a pass/fail report
2. **fix**: After audit, apply fixes to remediate identified vulnerabilities
</modes>

<workflow>

### Step 1: Identify Resource Type

Read the file at `{path}` and determine the resource type:
- **Skill**: SKILL.md files (YAML frontmatter + markdown)
- **Agent/Subagent**: JSON configuration files or markdown with agent definitions
- **Hook**: JavaScript/TypeScript files in hooks directory
- **Slash Command**: Markdown files defining slash commands
- **Prompt**: Markdown files containing prompts

### Step 2: Load OWASP LLM Top 10 Knowledge

Reference the comprehensive vulnerability documentation in:
`references/` (relative to this skill's location)

The 10 vulnerabilities you MUST check:

1. **LLM01: Prompt Injection**
   - Direct/indirect prompt manipulation
   - Lack of input validation
   - Missing prompt sanitization

2. **LLM02: Sensitive Information Disclosure**
   - Hardcoded credentials, API keys, tokens
   - PII exposure
   - Proprietary algorithm disclosure

3. **LLM03: Supply Chain**
   - Unverified third-party dependencies
   - Lack of package verification
   - Missing SBOM/integrity checks

4. **LLM04: Data and Model Poisoning**
   - Untrusted data sources
   - Missing data validation
   - Lack of data provenance tracking

5. **LLM05: Improper Output Handling**
   - No output sanitization (XSS, CSRF, RCE risks)
   - Direct execution of LLM outputs
   - Missing output encoding

6. **LLM06: Excessive Agency**
   - Too many permissions
   - Unnecessary tool access
   - Lack of human approval for high-risk actions

7. **LLM07: System Prompt Leakage**
   - Sensitive info in system prompts
   - Security controls delegated to LLM
   - Credentials in prompts

8. **LLM08: Vector and Embedding Weaknesses**
   - Inadequate RAG access controls
   - Cross-tenant data leakage
   - Embedding inversion risks

9. **LLM09: Misinformation**
   - No verification mechanisms
   - Overreliance on LLM outputs
   - Missing fact-checking

10. **LLM10: Unbounded Consumption**
    - No rate limiting
    - Missing resource quotas
    - Lack of input size validation

### Step 3: Perform Security Audit

For each of the 10 vulnerabilities:

1. **Read the reference material** for that vulnerability
2. **Analyze the resource** against the vulnerability patterns
3. **Document findings** with:
   - Severity: CRITICAL, HIGH, MEDIUM, LOW, PASS
   - Evidence: Specific lines/sections with issues
   - Impact: What could happen if exploited
   - Recommendation: How to fix

### Step 4: Generate Audit Report

Create a comprehensive security audit report:

```markdown
# OWASP LLM Top 10 Security Audit Report

**Resource**: {path}
**Type**: [Skill|Agent|Hook|Slash Command|Prompt]
**Date**: {current_date}
**Status**: [PASS|FAIL]

---

## Executive Summary

[Brief overview of findings]

**Overall Risk Level**: [CRITICAL|HIGH|MEDIUM|LOW]
**Vulnerabilities Found**: X/10
**Critical Issues**: X
**High Issues**: X
**Medium Issues**: X
**Low Issues**: X

---

## Detailed Findings

### LLM01: Prompt Injection
**Status**: [PASS|FAIL]
**Severity**: [CRITICAL|HIGH|MEDIUM|LOW]

**Findings**:
- [Specific issue found]
- [Evidence from code]

**Impact**: [What could happen]

**Recommendation**: [How to fix]

---

### LLM02: Sensitive Information Disclosure
[Same structure for each vulnerability]

---

[Continue for all 10 vulnerabilities]

---

## Remediation Priority

1. **Critical** (Fix Immediately):
   - [List critical issues]

2. **High** (Fix This Week):
   - [List high priority issues]

3. **Medium** (Fix This Month):
   - [List medium priority issues]

4. **Low** (Consider Fixing):
   - [List low priority issues]

---

## Next Steps

[If mode is 'audit']: Run with `fix` mode to automatically remediate issues.
[If mode is 'fix']: Review the changes and test thoroughly.
```

### Step 5: Fix Mode (if mode='fix')

If the user requested **fix** mode:

1. **Review audit findings**
2. **For each vulnerability**:
   - Apply the recommended fix
   - Use Edit tool to modify the file
   - Add security controls
   - Document the change
3. **Create a summary** of all changes made
4. **Recommend testing** procedures
</workflow>

<resource_checks>

### For Skills (SKILL.md)

Check for:
- **LLM01**: Input validation in args, prompt injection guards
- **LLM02**: No hardcoded secrets in prompts
- **LLM06**: Limited tool access, human approval for dangerous operations
- **LLM07**: No sensitive info in skill instructions
- **LLM09**: Verification mechanisms for outputs
- **LLM10**: Rate limiting, resource constraints

### For Agents/Subagents

Check for:
- **LLM01**: System prompt injection defenses
- **LLM02**: No credentials in agent config
- **LLM06**: Minimal tool permissions (least privilege)
- **LLM07**: Separation of sensitive data from prompts
- **LLM08**: RAG access controls if using vector DBs
- **LLM10**: Resource limits, timeouts

### For Hooks

Check for:
- **LLM03**: Verified dependencies
- **LLM05**: Output sanitization before execution
- **LLM06**: Limited system access
- **LLM10**: Resource consumption limits

### For Slash Commands

Check for:
- **LLM01**: Input validation
- **LLM02**: No secret exposure
- **LLM05**: Safe output handling
- **LLM07**: No sensitive instructions in command definition

### For Prompts

Check for:
- **LLM01**: Anti-injection instructions
- **LLM02**: No embedded credentials
- **LLM07**: Security controls not in prompt
- **LLM09**: Verification requirements
</resource_checks>

<implementation>

### When in 'audit' mode:
1. Read the resource file
2. Read ALL 10 reference documents
3. Perform thorough analysis
4. Generate detailed report
5. Provide actionable recommendations

### When in 'fix' mode:
1. First run audit (if not already done)
2. Ask user to confirm fixes before applying
3. Apply fixes one vulnerability at a time
4. Document each change
5. Provide testing recommendations

### Output Format

Always provide:
- **PASS** items with brief explanation
- **FAIL** items with detailed findings
- Actionable recommendations
- Priority ordering
</implementation>

<constraints>
- MUST analyze all 10 OWASP LLM vulnerabilities in every audit (no exceptions)
- MUST provide specific evidence (line numbers, code sections) for every finding
- NEVER flag issues without clear evidence from the resource
- ALWAYS consider resource type and context when assessing severity
- MUST prioritize security over convenience in all recommendations
- ALWAYS maintain clear audit trail for compliance documentation
- NEVER generate false positives - only flag real vulnerabilities with evidence
- MUST provide implementable, practical solutions in recommendations
</constraints>

Now analyze the resource at `{path}` in **{mode}** mode following the methodology above.

**Remember**: You are looking for SECURITY VULNERABILITIES that could lead to:
- Unauthorized access
- Data breaches
- System compromise
- Misinformation
- Resource abuse
- Supply chain attacks

Be thorough, be precise, and provide actionable guidance.
