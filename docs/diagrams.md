# diagrams/

# Mermaid Diagram Files

Standalone diagram files for reuse across documentation, presentations, and GitHub.

## Available Diagrams

1. [mcp-gateway-architecture.mermaid](diagrams/mcp-gateway-architecture%20mermaid%20e5461680d60f4f5a9af99f471a4102c7.md) - Three-zone isolation pattern
2. [tal-request-flow.mermaid](diagrams/tal-request-flow%20mermaid%20e88e53ee73e64256a4394a2b83d8782a.md) - Complete request sequence
3. [network-segmentation.mermaid](diagrams/network-segmentation%20mermaid%2025a177e72cce441a8932492122b81be2.md) - DMZ deployment architecture
4. [authorization-flow.mermaid](diagrams/authorization-flow%20mermaid%2054ea44778e4348a5a06897a7a50242e4.md) - Decision tree with 6 gates
5. [threat-landscape.mermaid](diagrams/threat-landscape%20mermaid%2054e151e988234a0fab301593453eae13.md) - Attack vectors and outcomes
6. [compliance-coverage.mermaid](diagrams/compliance-coverage%20mermaid%205e34f83277d242de952bc2750b93a5c6.md) - SOC 2, ISO 27001, GDPR mapping
7. [defense-layers.mermaid](diagrams/defense-layers%20mermaid%201b132d36f056467daad5e9ed79bf34e5.md) - 5-layer security architecture
8. [monitoring-architecture.mermaid](diagrams/monitoring-architecture%20mermaid%20da4f5b57b2554d3a981b0f3558e511ff.md) - SIEM integration and alerting
9. [phased-deployment.mermaid](diagrams/phased-deployment%20mermaid%206611de0855864d74a4c7c8ce0015e086.md) - 16-week implementation Gantt chart

## Usage

Each `.mermaid` file can be:

- Embedded directly in GitHub markdown
- Exported as SVG/PNG via [Mermaid Live Editor](https://mermaid.live)
- Used in documentation generators (MkDocs, Docusaurus, Hugo)

## Color Coding

All diagrams use consistent semantic colors:

- 🔴 Red (`#ff6b6b`): Threats, untrusted zones, critical risks
- 🟠 Orange (`#ffd93d`): Medium risks, DMZ zones, warnings
- 🟡 Yellow (`#ffe66d`): Logging, monitoring, informational
- 🟢 Green (`#95e1d3`): Trusted zones, approved actions, low risk
- 🔵 Blue (`#4ecdc4`): Security controls, authentication, enforcement

[compliance-coverage.mermaid](diagrams/compliance-coverage%20mermaid%205e34f83277d242de952bc2750b93a5c6.md)

[defense-layers.mermaid](diagrams/defense-layers%20mermaid%201b132d36f056467daad5e9ed79bf34e5.md)

[monitoring-architecture.mermaid](diagrams/monitoring-architecture%20mermaid%20da4f5b57b2554d3a981b0f3558e511ff.md)

[phased-deployment.mermaid](diagrams/phased-deployment%20mermaid%206611de0855864d74a4c7c8ce0015e086.md)

[mcp-gateway-architecture.mermaid](diagrams/mcp-gateway-architecture%20mermaid%20e5461680d60f4f5a9af99f471a4102c7.md)

[tal-request-flow.mermaid](diagrams/tal-request-flow%20mermaid%20e88e53ee73e64256a4394a2b83d8782a.md)

[network-segmentation.mermaid](diagrams/network-segmentation%20mermaid%2025a177e72cce441a8932492122b81be2.md)

[authorization-flow.mermaid](diagrams/authorization-flow%20mermaid%2054ea44778e4348a5a06897a7a50242e4.md)

[threat-landscape.mermaid](diagrams/threat-landscape%20mermaid%2054e151e988234a0fab301593453eae13.md)