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
| ES|QL | Elastic event analysis and correlation |
| ArcSight ESM | SIEM filtering and correlation |
| MITRE ATT&CK | Adversary technique mapping |
| Python | Detection engineering automation |
| Git / GitHub | Version control and collaboration |
| Linux | Development environment |

## Repository Structure

```text
detections/       Detection specifications and SIEM implementations
datasets/         Synthetic security logs and schemas
tests/            Positive and negative detection tests
mitre/            MITRE ATT&CK coverage and analysis
scripts/          Python automation and validation
documentation/    Engineering methodology and technical guides
templates/        Reusable detection templates
```

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
| Elastic Security | KQL and ES|QL |
| ArcSight ESM | Filters and correlation rules |

Detection specifications are maintained independently of platform-specific implementations to support portability and maintainability.

## Testing and Validation

Detection logic will be evaluated using synthetic datasets and controlled test scenarios.

Validation will cover:

- Expected detection behavior.
- Negative test scenarios.
- Required telemetry availability.
- False-positive considerations.
- Detection limitations and tuning requirements.

Implementation and validation status will be explicitly documented.

## Project Scope

This is an independent educational and professional portfolio project.

All detection scenarios, datasets, and examples are developed independently. No confidential employer information, proprietary security configurations, or sensitive production data are included.

## Author

Independent SIEM and Detection Engineering Portfolio.

**Focus:** Detection Engineering | SIEM | Elastic Security | ArcSight | Security Analytics

---

*This repository is continuously evolving as new detection scenarios, implementations, and validation capabilities are developed.*
