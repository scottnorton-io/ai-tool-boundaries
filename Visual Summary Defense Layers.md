# Visual Summary: Defense Layers

This page provides a comprehensive visual reference for the defense-in-depth architecture of the MCP security framework.

💡 **How to use this page:** This is your visual reference sheet. Bookmark it and return whenever you need to explain MCP security visually. Each diagram is production-ready for presentations.

---

## 🎯 One-Page Visual Summary

### The 3-Second Pitch

**5 layers** of defense → **5 threat types** mitigated → **3 compliance frameworks** satisfied

### The 30-Second Pitch

MCP introduces critical security risks (prompt injection, data exfiltration, credential theft). This framework provides **defense-in-depth** across network, authentication, authorization, validation, and audit layers. Result: **Production-ready AI integration** with **compliance-ready evidence**.

---

## Complete Defense Architecture

```mermaid
graph TB
    subgraph "Layer 1: Network Segmentation"
        A[Internet] --> B[Firewall]
        B --> C[DMZ]
        C --> D[MCP Gateway]
    end
    
    subgraph "Layer 2: Authentication"
        D --> E[Certificate Validation]
        E --> F[mTLS Handshake]
        F --> G[Identity Verification]
    end
    
    subgraph "Layer 3: Authorization"
        G --> H[Tool Allowlist Check]
        H --> I[Permission Validation]
        I --> J[Rate Limit Check]
    end
    
    subgraph "Layer 4: Validation"
        J --> K[Schema Validation]
        K --> L[Type Checking]
        L --> M[Injection Detection]
    end
    
    subgraph "Layer 5: Audit & Monitoring"
        M --> N[Audit Event Generation]
        N --> O[SIEM Integration]
        O --> P[Alert Management]
    end
    
    subgraph "Protected Resources"
        M --> Q[API Services]
        Q --> R[(Databases)]
    end
    
    style A fill:#ff6b6b
    style D fill:#ffd93d
    style E fill:#4ecdc4
    style F fill:#4ecdc4
    style G fill:#4ecdc4
    style H fill:#6bcf7f
    style I fill:#6bcf7f
    style J fill:#6bcf7f
    style K fill:#95e1d3
    style L fill:#95e1d3
    style M fill:#95e1d3
    style N fill:#ffe66d
    style O fill:#ffe66d
    style P fill:#ffe66d
    style Q fill:#d4edda
    style R fill:#d4edda
```

## Control Effectiveness Matrix

```mermaid
graph TB
    subgraph "Threats"
        T1[Prompt Injection]
        T2[Credential Theft]
        T3[Data Exfiltration]
        T4[Tool Chaining]
        T5[Overprivileged Access]
    end
    
    subgraph "Primary Controls"
        C1[Schema Validation]
        C2[Tool Allowlisting]
        C3[Parameter Constraints]
        C4[Audit Logging]
        C5[Data Redaction]
    end
    
    subgraph "Effectiveness"
        E1[High]
        E2[High]
        E3[Medium]
        E4[High]
        E5[Medium]
    end
    
    T1 -.->|Mitigated by| C1
    T1 -.->|Mitigated by| C3
    C1 --> E1
    C3 --> E3
    
    T2 -.->|Mitigated by| C4
    C4 --> E4
    
    T3 -.->|Mitigated by| C3
    T3 -.->|Mitigated by| C5
    C5 --> E2
    
    T4 -.->|Mitigated by| C2
    T4 -.->|Mitigated by| C4
    C2 --> E2
    
    T5 -.->|Mitigated by| C2
    
    style T1 fill:#ff6b6b
    style T2 fill:#ff6b6b
    style T3 fill:#ff6b6b
    style T4 fill:#ff6b6b
    style T5 fill:#ff6b6b
    style C1 fill:#95e1d3
    style C2 fill:#95e1d3
    style C3 fill:#95e1d3
    style C4 fill:#95e1d3
    style C5 fill:#95e1d3
    style E1 fill:#d4edda
    style E2 fill:#d4edda
    style E3 fill:#fff3cd
    style E4 fill:#d4edda
    style E5 fill:#fff3cd
```

## Data Flow with Security Controls

```mermaid
flowchart LR
    A[AI Agent] -->|1. Tool Request| B[MCP Gateway]
    B -->|2. Authenticate| C{Valid<br/>Certificate?}
    C -->|No| D[❌ Reject]
    C -->|Yes| E[Tool Access Layer]
    E -->|3. Authorize| F{Tool<br/>Allowed?}
    F -->|No| G[❌ Deny]
    F -->|Yes| H{Schema<br/>Valid?}
    H -->|No| I[❌ Reject]
    H -->|Yes| J[API Service]
    J -->|4. Execute| K[(Database)]
    K -->|5. Return Data| L[Redaction Engine]
    L -->|6. Filter| M[Clean Response]
    M -->|7. Deliver| A
    
    E -.->|Log| N[Audit Log]
    J -.->|Log| N
    L -.->|Log| N
    
    style A fill:#4ecdc4
    style D fill:#ff6b6b
    style G fill:#ff6b6b
    style I fill:#ff6b6b
    style K fill:#95e1d3
    style M fill:#d4edda
    style N fill:#ffe66d
```

## Risk-Control Mapping

| Risk Level | Threat Category | Primary Controls | Residual Risk |
| --- | --- | --- | --- |
| 🔴 Critical | Prompt Injection | Schema Validation + Type Enforcement + Semantic Analysis | 🟡 Low |
| 🔴 Critical | Data Exfiltration | Parameter Constraints + Output Redaction + Rate Limits | 🟡 Low |
| 🟠 High | Credential Theft | mTLS + Short-lived Certs + Secret Rotation | 🟢 Very Low |
| 🟠 High | Tool Chaining | Tool Allowlisting + Audit Correlation + Anomaly Detection | 🟡 Low |
| 🟠 High | Overprivileged Access | Least Privilege + Regular Reviews + Usage Monitoring | 🟢 Very Low |
| 🟡 Medium | Schema Bypass | Input Validation + Additional Properties: False | 🟢 Very Low |
| 🟡 Medium | Rate Limit Evasion | Multi-dimensional Limits + Circuit Breakers | 🟢 Very Low |

## Security Posture Progression

```mermaid
graph LR
    A[Baseline:<br/>No MCP Security] --> B[Phase 1:<br/>Basic Controls]
    B --> C[Phase 2:<br/>Enhanced Controls]
    C --> D[Phase 3:<br/>Operational Maturity]
    D --> E[Phase 4:<br/>Production Ready]
    E --> F[Phase 5:<br/>Continuous Improvement]
    
    subgraph "Risk Level"
        R1[🔴 Critical]
        R2[🟠 High]
        R3[🟡 Medium]
        R4[🟢 Low]
        R5[🟢 Very Low]
    end
    
    A -.-> R1
    B -.-> R2
    C -.-> R3
    D -.-> R4
    E -.-> R5
    F -.-> R5
    
    style A fill:#ff6b6b
    style B fill:#ffd93d
    style C fill:#fff3cd
    style D fill:#d1ecf1
    style E fill:#d4edda
    style F fill:#95e1d3
```

## Compliance Control Coverage

```mermaid
graph TB
    subgraph "MCP Security Framework"
        F[AI Tool Boundaries Framework]
    end
    
    subgraph "SOC 2 TSC"
        S1[CC6.1 Access]
        S2[CC6.2 Authorization]
        S3[CC6.3 Removal]
        S4[CC7.2 Monitoring]
        S5[CC7.3 Threat Eval]
        S6[CC8.1 Change Mgmt]
    end
    
    subgraph "ISO 27001"
        I1[A.9.1 Access Control]
        I2[A.9.2 User Mgmt]
        I3[A.9.4 System Access]
        I4[A.12.4 Logging]
        I5[A.14.2 Dev Security]
        I6[A.16.1 Incidents]
    end
    
    subgraph "GDPR"
        G1[Art 5.1.b Purpose]
        G2[Art 5.1.c Minimization]
        G3[Art 5.2 Accountability]
        G4[Art 25 By Design]
    end
    
    F --> S1
    F --> S2
    F --> S3
    F --> S4
    F --> S5
    F --> S6
    
    F --> I1
    F --> I2
    F --> I3
    F --> I4
    F --> I5
    F --> I6
    
    F --> G1
    F --> G2
    F --> G3
    F --> G4
    
    style F fill:#4ecdc4
    style S1 fill:#d4edda
    style S2 fill:#d4edda
    style S3 fill:#d4edda
    style S4 fill:#d4edda
    style S5 fill:#d4edda
    style S6 fill:#d4edda
    style I1 fill:#d1ecf1
    style I2 fill:#d1ecf1
    style I3 fill:#d1ecf1
    style I4 fill:#d1ecf1
    style I5 fill:#d1ecf1
    style I6 fill:#d1ecf1
    style G1 fill:#fff3cd
    style G2 fill:#fff3cd
    style G3 fill:#fff3cd
    style G4 fill:#fff3cd
```