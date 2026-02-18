# 03 – Security Level Targets

## 1. Purpose

This document defines how Security Level Targets (SL-T) are determined, documented, and validated within the **IEC62443 Compliance as Code** repository.

It establishes:

- How Security Levels are derived from risk assumptions  
- How SL-T is assigned per zone and conduit  
- How Achieved Security Level (SL-A) is evaluated  
- How traceability to IEC 62443 FR/SR identifiers is maintained  

This document aligns with IEC 62443-3-2 (risk assessment) and IEC 62443-3-3 (system security requirements).

---

## 2. Security Level Model

IEC 62443 defines Security Levels (SL) based on the capability of a threat actor the system is designed to resist.

This repository models:

- **SL-T** → Target Security Level  
- **SL-A** → Achieved Security Level (validated)  

Security Levels are assigned **per zone and per conduit**, not globally.

---

## 3. Security Level Definitions (High-Level)

Security Levels are interpreted generically as:

| SL | Protection Against |
|----|--------------------|
| SL 1 | Casual or coincidental violation |
| SL 2 | Intentional violation using simple means |
| SL 3 | Intentional violation using sophisticated means |
| SL 4 | Intentional violation using highly sophisticated means with extended resources |

This repository references SL levels structurally and does not reproduce IEC normative text.

---

## 4. SL-T Determination Method

Security Level Targets are derived from:

- Risk assumptions (`04-risk-assumptions.md`)  
- Threat capability model  
- Impact severity (safety, availability, financial, regulatory)  
- Exposure and connectivity  

Derivation logic:
Threat Capability
+
Impact Severity
+
Exposure Surface
↓
Security Level Target (SL-T)

SL-T must be:

- Explicitly documented  
- Justified against risk assumptions  
- Approved via pull request review  

---

## 5. Zone-Level Security Targets

Each defined zone must declare:

- Target Security Level (SL-T)  
- Rationale  
- Applicable Functional Requirements (FRs)  
- Evidence references  

### Example (Template)

| Zone | Description | SL-T | Rationale | Evidence Ref |
|------|------------|------|-----------|--------------|
| Enterprise / IT | Corporate IT systems | SL 2 | External exposure, credential risk | EVID-### |
| Boundary / DMZ | Intermediary trust zone | SL 3 | Segmentation enforcement | EVID-### |
| Supervisory | HMI / Historian | SL 3 | Operational impact | EVID-### |
| Control | PLC / Field devices | SL 3 or 4 | Safety & availability critical | EVID-### |

Actual values must be justified via documented risk assumptions.

---

## 6. Conduit-Level Security Targets

Conduits inherit constraints from connected zones but may require elevated protection.

Each conduit must define:

- Source zone  
- Destination zone  
- Required SL capability  
- Control mappings (FR/SR references)  
- Evidence IDs  

Example:

| Conduit ID | From | To | Required SL | FR Coverage | Evidence |
|------------|------|----|-------------|-------------|----------|
| C-01 | IT | DMZ | SL 3 | FR1, FR2, FR6 | EVID-001 |
| C-05 | Supervisory | Control | SL 3/4 | FR5, FR3 | EVID-010 |

All conduits must enforce FR5 (Restricted Data Flow) at minimum.

---

## 7. Functional Requirement Coverage by SL

Security Levels are validated by ensuring required FR/SR coverage is implemented.

Each zone must demonstrate:

- FR1 – Identification & Authentication  
- FR2 – Use Control  
- FR3 – System Integrity  
- FR4 – Data Confidentiality (if applicable)  
- FR5 – Restricted Data Flow  
- FR6 – Timely Response to Events  
- FR7 – Resource Availability  

Control coverage is verified through:

- `controls/controls-catalog.yml`  
- `mapping/mapping-template.csv`  
- Automation validation outputs  

---

## 8. Achieved Security Level (SL-A)

SL-A represents the validated implementation state.

SL-A is determined by:

- Control implementation status  
- Automation validation results  
- Evidence completeness  
- Drift detection status  

If required controls are:

- **Planned** → SL-A < SL-T  
- **In Progress** → SL-A < SL-T  
- **Implemented & Verified** → SL-A may equal SL-T  

SL-A must never exceed demonstrable evidence.

---

## 9. Validation Mechanism

Security Level validation includes:

1. Requirement-to-control mapping completeness  
2. Automation verification success  
3. Evidence artifact presence  
4. Drift detection status  

Validation workflow:
Control Mapping Check
↓
Automation Verification
↓
Evidence Generated
↓
SL-A Determined

This process is enforced via CI/CD pipelines.

---

## 10. SL Change Control

Security Level changes require:

- Updated risk assumptions (`04-risk-assumptions.md`)  
- Updated control mappings  
- Updated automation coverage  
- Peer-reviewed pull request  

Security Levels must not change implicitly.

---

## 11. Public Repository Constraints

Because this is a public repository:

- Real risk scoring data is excluded  
- Actual system SL assignments may be abstracted  
- Evidence artifacts contain metadata only  
- No proprietary IEC content is reproduced  

This document defines the structure for SL modeling, not operational risk detail.

---

## 12. Summary

This Security Level Target model ensures:

- SL-T is explicitly defined per zone and conduit  
- SL-A is measurable and evidence-based  
- Control implementation aligns to FR/SR identifiers  
- Compliance posture is continuously validated  
- Security levels are version-controlled and reviewable  

Security Levels are therefore:

**Risk-informed, explicitly documented, automation-validated, and continuously evaluated.**