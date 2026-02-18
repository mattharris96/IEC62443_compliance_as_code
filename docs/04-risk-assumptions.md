# 04 – Risk Assumptions

## 1. Purpose

This document defines the baseline risk assumptions used to:
- Determine Security Level Targets (SL-T)
- Justify zone segmentation
- Define conduit restrictions
- Scope control selection
- Support IEC 62443-3-2 alignment

This repository does not perform a full risk assessment.
Instead, it documents the assumed risk model used to engineer controls and automation.

## 2. Risk Assessment Context

IEC 62443-3-2 requires security levels to be derived from risk.

In this repository:
- Risk inputs are modeled conceptually
- Assumptions are documented explicitly
- Security Level Targets are derived from these assumptions
- Controls are mapped to FR/SR identifiers accordingly

Risk determination logic:

Threat Capability
      +
Impact Severity
      +
Exposure Surface
      ↓
Security Level Target (SL-T)

## 3. Threat Model Assumptions

The following baseline adversary capabilities are assumed.

### 3.1 External Adversary

Assume:
- Network-based attack capability
- Credential harvesting attempts
- Malware delivery attempts
- Phishing-based initial access
- Ability to scan exposed services

Do not assume:
- Physical access to OT control networks
- Insider-level privileged access (unless stated)

### 3.2 Insider Threat

Assume:
- Authenticated but potentially misconfigured users
- Privilege escalation attempts
- Misuse of legitimate credentials

Controls must enforce:
- Least privilege (FR2)
- Strong authentication (FR1)
- Logging and monitoring (FR6)

### 3.3 Supply Chain & Maintenance Access

Assume:
- Remote vendor access may be required
- Software updates occur periodically
- Portable media risks may exist

Controls must enforce:
- Restricted conduits (FR5)
- Integrity validation (FR3)
- Session logging and approval workflows

## 4. Impact Assumptions

Risk severity is evaluated across:
- Safety impact
- Operational disruption
- Financial loss
- Regulatory exposure
- Reputational damage

The OT Control Zone is assumed to have:
- High availability requirements
- Safety sensitivity
- Limited tolerance for downtime

Therefore:
- Resource Availability (FR7) controls are critical
- Segmentation from IT networks is mandatory (FR5)

## 5. Trust Boundary Assumptions

The following structural assumptions apply:
- IT and OT environments are separate trust domains
- No implicit trust exists between zones
- All inter-zone communication must traverse a defined conduit
- All conduits must be allowlisted

Zone classification examples:
- Enterprise / IT Zone
- Boundary / DMZ Zone
- Supervisory Zone
- Control Zone

Each zone may have a distinct SL-T.

## 6. Network Exposure Assumptions

Assume:
- Enterprise networks may be connected to external networks
- OT Control networks are not directly internet-facing
- Remote access occurs via controlled jump services
- Monitoring and logging data flows outbound via defined conduits

All flows must:
- Be documented in 02-zones-and-conduits.md
- Map to FR5 (Restricted Data Flow)
- Reference Evidence IDs

## 7. Authentication & Identity Assumptions

Assume:
- Centralized identity services exist
- Unique user identification is required
- Shared credentials are prohibited
- Administrative access requires elevated control

Controls must align to:
- FR1 (Identification & Authentication)
- FR2 (Use Control)

Automation must validate:
- Account configuration
- Password / key policies
- Privilege assignments
- Logging configuration

## 8. Logging & Detection Assumptions

Assume:
- Logging is required for:
- Authentication events
- Administrative access
- Security policy changes
- Zone boundary enforcement events
- Logs must be protected from tampering
- Log retention must be defined

Controls align to FR6.

Evidence must include:
- Configuration extracts (sanitized)
- Sample log outputs (redacted)
- Automation verification results

## 9. Availability & Resilience Assumptions

Assume:
- OT control environments have strict availability constraints
- Backups are required
- Recovery must be testable
- Denial-of-service risk exists

Controls align to FR7.

Automation should validate:
- Backup configuration
- Recovery procedure documentation
- Service health baselines

## 10. Residual Risk Acknowledgement

This repository assumes:
- Risk cannot be eliminated
- Controls reduce likelihood and impact
- Residual risk is formally accepted outside this repository

Risk acceptance decisions are out of scope for this public repository.

## 11. Security Level Target Derivation

Security Level Targets (SL-T) are derived from:
- Threat capability assumptions
- Impact classification
- Exposure model
- Regulatory drivers

SL-T must be:
- Defined per zone
- Documented in 03-security-level-targets.md
- Validated against implemented controls

Achieved Security Level (SL-A) must be supported by:
- Automated validation
- Evidence IDs
- Control mapping status

## 12. Public Repository Constraints

Because this is a public repository:
- Real threat intelligence is not documented
- Real risk scoring is not stored
- No vulnerability details are included
- No production topology is disclosed

This document defines a generic engineering risk baseline only.

## 13. Assumption Review & Change Control

Risk assumptions must be reviewed when:
- New zones are added
- New conduits are introduced
- Security Levels change
- Significant architectural modifications occur
- Regulatory requirements change

All changes must:
- Be proposed via Pull Request
- Update related SL targets
- Update control mappings if necessary
- Maintain traceability

## 14. Summary

This document establishes the risk foundation that drives:
- Security Level Targets
- Control selection
- Zone segmentation
- Conduit enforcement
- Automation validation
- Evidence generation

Risk assumptions are explicit, version-controlled, and reviewable — consistent with compliance-as-code principles.