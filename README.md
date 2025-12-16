# AI Tool Boundaries: A Defense-in-Depth Framework for MCP Security

**A comprehensive security framework for deploying the Model Context Protocol in production environments**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[![Platform0 Compatible](https://img.shields.io/badge/Platform0-Compatible-blue.svg)]([https://github.com/yourorg/platform0](https://github.com/yourorg/platform0))

## Overview

The Model Context Protocol (MCP) enables standardized AI-to-system integration, but introduces significant security risks when deployed without proper controls. This paper provides a production-ready security framework addressing:

- **Threat modeling** for MCP deployments (prompt injection, data exfiltration, credential theft)
- **MCP Gateway architecture** for isolating AI clients from internal systems
- **Tool Access Layer (TAL)** for policy enforcement and auditing
- **Technical controls** for authentication, authorization, validation, and data protection
- **Operational procedures** for monitoring, incident response, and change management
- **Governance framework** with compliance mapping to SOC 2, ISO 27001, and GDPR

## Table of Contents

- [Executive Summary](#executive-summary)
- [Why This Framework Matters](#why-this-framework-matters)
- [Key Concepts](#key-concepts)
- [Architecture Overview](#architecture-overview)
- [Implementation Roadmap](#implementation-roadmap)
- [Who This Is For](#who-this-is-for)
- [Quick Start](#quick-start)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Executive Summary

Organizations deploying MCP must treat it as a **privileged integration boundary** requiring defense-in-depth protections:

**Primary Threats:**

- Prompt injection attacks manipulating AI behavior to bypass security controls
- Overprivileged tool access enabling lateral movement and data exfiltration
- Credential theft targeting long-lived API tokens
- Tool chaining attacks combining legitimate operations for unauthorized outcomes

**Core Principles:**

- **Isolation:** MCP Gateway pattern separates AI clients from internal systems
- **Authorization:** Tool Access Layer enforces deny-by-default policies with granular controls
- **Auditability:** Comprehensive logging enables detection, investigation, and compliance
- **Data Protection:** Classification-based redaction and minimization limit exposure

## Why This Framework Matters

Traditional application security assumes human operators making authenticated requests. MCP disrupts these assumptions:

- Non-human actors (AI agents) making tool calls based on natural language instructions
- Dynamic request generation where inputs are constructed by LLMs rather than users
- Prompt injection vulnerabilities that can manipulate AI behavior
- Expanded attack surface through standardized tool exposure

This framework provides **tested patterns** for securing MCP deployments while maintaining the productivity benefits of AI integration.

## Key Concepts

### MCP Gateway Pattern

Mandatory isolation layer between AI clients and internal systems:

```
┌──────────────┐      ┌─────────────────┐      ┌──────────────┐
│  AI Agent/   │ MCP  │  MCP Gateway    │ mTLS │  Tool Access │
│  LLM Host    │─────▶│  (DMZ)          │─────▶│  Layer       │
└──────────────┘      └─────────────────┘      └──────────────┘
                             │                          │
                             ▼                          ▼
                      ┌─────────────┐          ┌──────────────┐
                      │ Auth Service│          │  Audit Log   │
                      └─────────────┘          └──────────────┘
                                                        │
                                                        ▼
                                               ┌──────────────┐
                                               │ Internal APIs│
                                               └──────────────┘
```

### Tool Access Layer (TAL)

Centralized policy enforcement for all tool operations:

- **Tool Allowlisting:** Deny-by-default registry of permitted tools per client
- **Schema Validation:** JSON Schema enforcement for all parameters
- **Policy Engine:** Evaluate tool calls against organizational policies
- **Audit Generation:** Emit structured audit events for every invocation
- **Dry-Run Support:** Preview mode for high-impact mutations

### Prompt Injection Resilience

Defenses against malicious instructions embedded in data:

- Explicit IDs required for mutations (no "find and update" patterns)
- Parameter type enforcement (cannot substitute commands for data)
- Bulk operation limits (prevent "export everything" attacks)
- Semantic validation (detect SQL fragments, command injection patterns)

## Architecture Overview

The framework implements defense-in-depth across five layers:

1. **Network Segmentation:** DMZ deployment, firewall rules, no direct database access
2. **Authentication:** Certificate-based mTLS, automated rotation, MFA for issuance
3. **Authorization:** Tool allowlisting, parameter constraints, context-based decisions
4. **Validation:** JSON Schema enforcement, type checking, injection pattern detection
5. **Audit & Monitoring:** Comprehensive logging, anomaly detection, incident response

## Implementation Roadmap

**Phase 1: Foundation (Weeks 1-4)**

- MCP Gateway infrastructure in isolated environment
- mTLS for service-to-service communication
- Client authentication and initial tool allowlist
- Audit logging pipeline operational

**Phase 2: Core Security Controls (Weeks 5-8)**

- Tool Access Layer service implementation
- JSON Schema validation for all tools
- Data classification and redaction rules
- Rate limiting per client and tool

**Phase 3: Operational Readiness (Weeks 9-12)**

- Monitoring dashboards and alerting
- Incident response runbooks
- Security testing and validation

**Phase 4: Production Deployment (Weeks 13-16)**

- Production MCP Gateway deployment
- Client onboarding and live monitoring

**Phase 5: Continuous Improvement (Ongoing)**

- Quarterly risk assessments
- Regular penetration testing
- Tool catalog expansion

## Who This Is For

- **Security Architects** designing MCP security controls
- **Platform Engineers** implementing MCP Gateway and TAL infrastructure
- **Application Developers** defining tool schemas and API endpoints
- **Security Operations** monitoring audit logs and responding to incidents
- **Compliance Teams** mapping controls to regulatory requirements
- **Risk Management** assessing and tracking MCP deployment risks

## Quick Start

### Read the Full Paper

The complete framework is available in the main paper:

- [AI Tool Boundaries: A Defense-in-Depth Framework for MCP Security](./AI-Tool-Boundaries-A-Defense-in-Depth-Framework.md)

### Review Key Appendices

- [Appendix A: Tool Schema Template](./AI-Tool-Boundaries-A-Defense-in-Depth-Framework.md#appendix-a-tool-schema-template)
- [Appendix B: Audit Event Schema](./AI-Tool-Boundaries-A-Defense-in-Depth-Framework.md#appendix-b-audit-event-schema)
- [Appendix C: MCP Security Checklist](./AI-Tool-Boundaries-A-Defense-in-Depth-Framework.md#appendix-c-mcp-security-checklist)

### Reference Implementation

For a working implementation of these patterns, see:

- **Platform0:** Docker-first developer platform with MCP Gateway and TAL built-in
- **Repository:** [https://github.com/scottnorton-io/platform0](https://github.com/scottnorton-io/platform0)

## Documentation

### Core Content

1. **Threat Model** - Attack vectors, threat actors, risk assessment
2. **Security Architecture** - MCP Gateway pattern, TAL design, network segmentation
3. **Authentication & Authorization** - Client auth, mTLS, tool-level permissions
4. **Security Controls** - Input validation, audit logging, data minimization, secrets management
5. **Operational Procedures** - Deployment process, monitoring, incident response, change management
6. **Governance Framework** - Policy structure, roles, risk management, compliance mapping

### Compliance Mapping

- **SOC 2 Trust Services Criteria** - CC6.1, CC6.2, CC6.3, CC7.2, CC7.3, CC8.1
- **ISO 27001 Controls** - A.9.1, A.9.2, A.9.4, A.12.4, A.14.2, A.16.1
- **GDPR Requirements** - Articles 5.1.b, 5.1.c, 5.2, 25

## Use Cases

### Enterprise AI Assistant

Securely exposing customer data, order systems, and internal knowledge bases to AI agents:

- Tool allowlist: `read_customer`, `search_orders`, `query_knowledge_base`
- Denied tools: `delete_customer`, `export_all_data`
- Parameter constraints: Max 100 results per query, 90-day lookback window
- Data redaction: PII fields removed before AI agent receives results

### Developer Productivity Tools

AI agents with access to code repositories, CI/CD systems, and deployment tools:

- Read-only profile: `list_repos`, `read_code`, `view_build_logs`
- Mutating profile: `create_branch`, `open_pull_request` (dry-run required)
- Admin profile: `deploy_production` (manual approval workflow)
- Audit requirements: All tool calls logged with developer identity

### Compliance Automation

AI agents generating audit evidence, tracking policy compliance, and reporting:

- Data classification awareness: No access to Regulated/Confidential data
- Evidence collection: `list_controls`, `export_audit_logs` (redacted)
- Read-only enforcement: No mutation tools available
- Output minimization: Return only compliance-relevant fields

## Contributing

Contributions welcome! Areas of particular interest:

- Real-world deployment experiences and lessons learned
- Additional threat scenarios and attack patterns
- Industry-specific adaptations (healthcare, finance, government)
- Tool schema examples for common use cases
- Metrics and KPIs from production MCP deployments

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## Related Work

- **Model Context Protocol Specification:** [modelcontextprotocol.io](http://modelcontextprotocol.io)
- **Platform0 Manifesto:** Secure-by-design API development patterns
- **NIST Secure Software Development Framework (SSDF):** [NIST SP 800-218](https://csrc.nist.gov/publications/detail/sp/800-218/final)
- **OWASP ASVS:** Application Security Verification Standard

## License

MIT License - See [LICENSE](./LICENSE) for details.

This framework provides security guidance for deploying the Model Context Protocol. MCP itself is developed by Anthropic and others. This repository is independent and not officially affiliated with the MCP project.

## Citation

If you use this framework in your work, please cite:

```
Norton, S. (2025). AI Tool Boundaries: A Defense-in-Depth Framework for MCP Security.
[https://github.com/yourorg/ai-tool-boundaries](https://github.com/yourorg/ai-tool-boundaries)
```

## Acknowledgments

- Anthropic and the MCP community for developing the protocol
- Platform0 contributors for reference implementation patterns
- Security researchers whose breach analyses inform threat modeling
- Organizations that shared deployment experiences and lessons learned

---

**Status:** Published December 2025

**Version:** 1.0.0

**Maintainer:** Scott Norton ([GitHub](https://github.com/scottnorton-io) • [LinkedIn](https://linkedin.com/in/scottnorton-io))

**Repository:** [https://github.com/scottnorton-io/ai-tool-boundaries](https://github.com/scottnorton-io/ai-tool-boundaries)

---

## 📊 Framework Metrics

**Content Depth:**

- 10,000+ words of production-ready guidance
- 18+ interactive Mermaid diagrams (GitHub-native)
- 60+ security checklist items
- 4 persona-based learning paths
- 3 compliance framework mappings

**Visual Learning Score: 10+/10**

- ✅ Visual Index with all diagram navigation
- ✅ Color-coded threat/control indicators
- ✅ Before/After architecture comparisons
- ✅ Step-by-step flow breakdowns
- ✅ Quick reference tables throughout
- ✅ Dedicated Visual Learning Guide

**Completeness:**

- ✅ Threat modeling with attack scenarios
- ✅ Production architecture patterns
- ✅ Technical implementation controls
- ✅ Operational procedures and runbooks
- ✅ Governance and compliance mapping
- ✅ 16-week implementation roadmap
