# SECURITY.md

# Security Policy

## Reporting Security Vulnerabilities

We take security seriously and appreciate responsible disclosure of security issues.

### Scope

This security policy applies to:

- **This framework documentation** - Security issues in guidance, examples, or recommendations
- **Reference implementations** - Vulnerabilities in code examples provided in this repository

**Out of Scope:**

- Third-party MCP implementations
- Vulnerabilities in specific vendor products
- Issues in your deployment (consult your security team)

### Reporting Process

**For security issues in this framework:**

1. **Contact:** Via [GitHub Issues](https://github.com/scottnorton-io/platform0) (mark as security advisory) or [LinkedIn](https://linkedin.com/in/scottnorton-io/)
2. **Subject Line:** "SECURITY: [Brief Description]"
3. **Include:**
    - Description of the issue
    - Potential impact
    - Steps to reproduce (if applicable)
    - Suggested remediation (if available)

**Do not:**

- Open public GitHub issues for security vulnerabilities
- Share vulnerability details on social media or forums
- Exploit the vulnerability beyond proof-of-concept validation

### Response Timeline

- **Initial Response:** Within 48 hours of report
- **Triage Assessment:** Within 7 days
- **Remediation Plan:** Within 14 days for critical issues
- **Public Disclosure:** Coordinated after fix is available

### Severity Classification

**Critical:**

- Framework guidance enables exploitable vulnerabilities
- Recommended controls have fundamental flaws
- Compliance mappings are materially incorrect

**High:**

- Framework examples contain security weaknesses
- Threat model misses significant attack vectors
- Implementation guidance has gaps

**Medium:**

- Documentation ambiguity could lead to misconfiguration
- Examples lack important security context
- Control recommendations need enhancement

**Low:**

- Minor documentation clarifications
- Non-security improvements

### Remediation Process

1. **Validate:** Confirm the security issue
2. **Develop Fix:** Update framework guidance, examples, or documentation
3. **Review:** Security review of proposed changes
4. **Test:** Validate fix addresses the issue
5. **Release:** Publish updated framework version
6. **Notify:** Inform reporters and community

### Disclosure Timeline

We follow a **90-day coordinated disclosure** timeline:

- **Day 0:** Vulnerability reported
- **Day 7:** Triage complete, severity assigned
- **Day 14-30:** Fix developed and tested
- **Day 30-60:** Updated framework version released
- **Day 60-90:** Public disclosure with credit to reporter

**Early disclosure** may occur if:

- The issue is already public
- Active exploitation is detected
- Reporter and maintainer agree

**Extended timeline** may be needed for:

- Complex issues requiring significant rework
- Coordination with multiple affected parties
- Critical issues requiring careful communication

### Security Advisories

Security updates will be published:

- In [CHANGELOG.md](http://CHANGELOG.md) with "Security" section
- As GitHub Security Advisories (when applicable)
- In framework documentation with clear version indicators

### Recognition

Security researchers who responsibly disclose vulnerabilities will be:

- Credited in security advisories (unless anonymity requested)
- Acknowledged in [CONTRIBUTORS.md](http://CONTRIBUTORS.md)
- Recognized in release notes

### Example Report Template

```markdown
Subject: SECURITY: [Brief Description]

## Vulnerability Details
**Type:** [e.g., Insecure guidance, Missing control, Incorrect compliance mapping]
**Severity:** [Your assessment: Critical/High/Medium/Low]
**Affected Section:** [Framework section, page, or example]

## Description
[Clear description of the security issue]

## Impact
[Potential consequences of following the flawed guidance]

## Steps to Reproduce
1. [If applicable, how someone might encounter this issue]
2. [Step-by-step demonstration]

## Suggested Fix
[Your recommended remediation, if available]

## References
[Supporting documentation, similar vulnerabilities, etc.]
```

### Out-of-Band Vulnerabilities

If you discover vulnerabilities in **actual MCP implementations** (not this framework):

1. **Report to the vendor** responsible for the implementation
2. **Follow their security disclosure process**
3. **Allow appropriate remediation time** (typically 90 days)
4. **After coordinated disclosure**, consider contributing lessons learned to this framework

### Security Best Practices for Contributors

When contributing to this framework:

- **Review for security implications** before submitting
- **Validate code examples** for vulnerabilities
- **Test configurations** in isolated environments
- **Cite sources** for threat intelligence and attack patterns
- **Consider edge cases** and failure modes
- **Document assumptions** and prerequisites

### Questions?

For non-security questions about this framework, use:

- GitHub Discussions for general questions
- GitHub Issues for bug reports or enhancements
- Email for private inquiries

---

**Last Updated:** 2025-12-14

**Version:** 1.0

**Maintainer:** Scott Norton ([GitHub](https://github.com/scottnorton-io) • [LinkedIn](https://linkedin.com/in/scottnorton-io/))