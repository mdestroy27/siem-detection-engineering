# SIEM Detection Engineering

**Cross-platform security detection engineering using Elastic Security and ArcSight ESM.**

## Overview

This repository is an independent cybersecurity engineering portfolio focused on designing, implementing, documenting, and validating security detection use cases across enterprise SIEM platforms.

The project demonstrates a structured approach to detection engineering, covering the complete lifecycle from threat identification and telemetry requirements to detection implementation, testing, tuning, and investigation guidance.

## Objectives

- Develop reusable, platform-independent detection specifications.
- Implement detection logic using Elastic Security and ArcSight ESM.
- Explore KQL, ES|QL, ArcSight filters, and correlation rules.
- Map detection capabilities to MITRE ATT&CK.
- Evaluate false positives and detection effectiveness.
- Build synthetic security datasets for repeatable testing.
- Develop Python tools to automate detection validation.

## Technology Stack

| Technology | Purpose |
|---|---|
| Elastic Security | SIEM detection implementation |
| KQL | Elastic query-based detection |
| ES\|QL | Elastic event analysis and correlation |
| ArcSight ESM | SIEM filtering and correlation |
| MITRE ATT&CK | Adversary technique mapping |
| Python | Detection engineering automation |
| Git / GitHub | Version control and collaboration |
| Linux | Development environment |

## Repository Structure

```text
detections/
  specifications/       Vendor-neutral detection specifications
  elastic/kql/          Elastic KQL detections and exception guidance
  elastic/esql/         Elastic ES|QL detections
  arcsight/             ArcSight filters and rule conditions
datasets/
  events/               Synthetic event data (JSONL)
  whitelists/           Independent allowlists used by detections
mitre/                  MITRE ATT&CK references and coverage
```

Each detection's specification describes the behavior independently of a SIEM. Platform-specific rule logic is stored under the relevant platform directory; synthetic events and allowlists are kept separately under `datasets/`.

## Detection Engineering Methodology

Each detection will follow a consistent engineering process:

1. Identify the threat scenario.
2. Define the detection objective.
3. Identify required telemetry and data sources.
4. Define the platform-independent detection logic.
5. Implement the detection in supported SIEM platforms.
6. Map the detection to MITRE ATT&CK.
7. Validate using synthetic security events.
8. Analyze false positives and tune detection logic.
9. Document investigation and response recommendations.

## Platform Support

| Platform | Implementation |
|---|---|
| Elastic Security | KQL and ES\|QL |
| ArcSight ESM | Filters and correlation rules |

Detection specifications are maintained independently of platform-specific implementations to support portability and maintainability.

## Testing and Validation

Synthetic events under `datasets/events/` illustrate expected alert and non-alert behavior. Allowlist examples under `datasets/whitelists/` are reference data; SIEM rules must be configured to evaluate the applicable lists. Validate field mappings and rule behavior in the target SIEM before deployment.

## Project Scope

This is an independent educational and professional portfolio project.

All detection scenarios, datasets, and examples are developed independently. No confidential employer information, proprietary security configurations, or sensitive production data are included.

## Author

**Marty Brou**
Cybersecurity Professional | Detection Engineer | SIEM & Security Operations

GitHub: [@mdestroy27](https://github.com/mdestroy27)

### Professional Background

- 8 years of Security Operations Center (SOC) experience.
- 7 years of hands-on ArcSight SIEM experience.
- Development and maintenance of 50+ security detection use cases.
- Experience in SIEM architecture, log parsing, integrations, correlation rules and SOC automation.
- Hands-on experience with multiple SIEM, EDR/XDR and Cloud Security platforms.
- Currently expanding expertise in Elastic Security and cross-platform detection engineering.

### Security Technologies

| Domain | Technologies |
|---|---|
| SIEM | ArcSight ESM, Elastic Security |
| EDR / XDR | Microsoft Defender for Endpoint, HarfangLab |
| Cloud Security | Wiz |
| Automation & Scripting | Python, Bash |
| Operating Systems | Linux, Windows |
| Threat Detection | MITRE ATT&CK, Detection Engineering |

### Areas of Interest

Detection Engineering | SIEM Architecture | Security Analytics | Threat Detection | Cloud Security | SOC Automation

---

*This repository represents independent technical work and professional development. All examples are independently developed using synthetic or publicly available data.*
