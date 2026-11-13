# Contributing Guidelines

Thank you for your interest in this SIEM Detection Engineering project.

This repository follows a structured approach to developing, documenting, and validating security detections across Elastic Security and ArcSight ESM.

## Contribution Principles

All contributions should:

- Use synthetic or publicly available security data.
- Avoid confidential employer information and production data.
- Follow MITRE ATT&CK mapping conventions.
- Include clear detection objectives and technical requirements.
- Document potential false positives.
- Include investigation recommendations.
- Provide validation evidence where possible.

## Detection Specification Requirements

Every detection should document:

1. Unique detection identifier.
2. Detection name and objective.
3. Threat scenario.
4. Required log sources.
5. Required event fields.
6. Detection logic and thresholds.
7. MITRE ATT&CK mapping.
8. Severity and risk rationale.
9. False-positive scenarios.
10. Investigation recommendations.
11. Testing and validation results.

## Platform Implementations

Elastic implementations should identify the applicable query language and required ECS fields.

ArcSight implementations should document the relevant event fields, filters, correlation logic, aggregation and suppression requirements.

Platform-specific limitations should be explicitly documented.

## Testing Requirements

Where applicable, contributions should include:

- Positive test cases.
- Negative test cases.
- Synthetic test events.
- Expected detection outcomes.
- Actual validation results.

Do not claim successful validation without supporting evidence.

## Pull Requests

Contributions should explain:

- What changed.
- Why the change is necessary.
- Which detection scenarios are affected.
- How the changes were tested.

All contributions should maintain the project's focus on reusable, transparent and technically defensible detection engineering.
