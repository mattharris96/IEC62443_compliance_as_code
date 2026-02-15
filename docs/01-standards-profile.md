# 01 – Standards Profile

## 1. Purpose

This document defines the IEC 62443 profile adopted by this repository.

It clarifies:
- Which parts of the IEC 62443 series are in scope
- How Functional Requirements (FRs) and System Requirements (SRs) are referenced
- How Security Levels (SLs) are modeled
- How requirements are mapped to controls, automation, and evidence

This file does not reproduce IEC 62443 text.
It references requirement identifiers only.

## 2. Standards in Scope

This repository aligns with the following parts of the IEC 62443 series:
- IEC 62443-2-x – Security program requirements
- IEC 62443-3-2 – System risk assessment and security level determination
- IEC 62443-3-3 – System security requirements and security levels
- IEC 62443-4-x – Component and secure development lifecycle requirements

Primary system design alignment is with:

	IEC 62443-3-3 — security requirements structured by
Functional Requirements (FRs) and Security Levels (SLs)

## 3. Functional Requirement (FR) Structure

IEC 62443-3-3 organizes system security requirements into seven Functional Requirements:

FR ID	Functional Area
FR1	Identification and Authentication Control
FR2	Use Control
FR3	System Integrity
FR4	Data Confidentiality
FR5	Restricted Data Flow
FR6	Timely Response to Events
FR7	Resource Availability

This repository references FR and SR identifiers only (e.g., FR1, SR 1.1).

Requirement statements are implemented via:
- Control definitions (controls/controls-catalog.yml)
- Zone & conduit definitions (docs/02-zones-and-conduits.md)
- Automation roles (Ansible)
- Evidence IDs (evidence/evidence-index.md)

## 4. Security Level (SL) Profiling

Security Levels are determined per zone and conduit based on:
- Risk assumptions (see 04-risk-assumptions.md)
- Threat capability model
- Impact tolerance
- Regulatory or business requirements

Security Levels are expressed as:

SL-T  → Target Security Level
SL-A  → Achieved Security Level (validated via automation)

Security Level targets must be:
- Explicit per zone
- Traceable to risk assumptions
- Validated through automated checks where feasible

No implicit SL inheritance is permitted between zones.

## 5. Zone & Conduit Interpretation

This repository interprets IEC 62443-3-3 through a zone-and-conduit model.
- Zones = trust boundaries
- Conduits = explicitly authorized communication paths
- Each conduit must reference applicable FR/SR identifiers
- Each conduit must reference Evidence IDs

Example linkage:

FR5 (Restricted Data Flow)
   ↓
CTRL-FLOW-001
   ↓
Firewall Policy Model
   ↓
Ansible Enforcement Role
   ↓
EVID-010

All data flows between zones must be:
- Explicitly declared
- Allowlisted
- Logged where applicable
- Mapped to FR5 and related SRs

## 6. Control Profiling Model

Controls are defined in:

controls/controls-catalog.yml

Each control includes:
- Control ID
- Intent statement (repository-authored)
- Requirement IDs (FR/SR identifiers only)
- Implementation references
- Evidence types

Example:

requirement_ids: ["FR1", "SR 1.1"]

Controls must:
- Be implementation-neutral where possible
- Avoid vendor-specific assumptions
- Support machine-verifiable validation

## 7. Mapping Methodology

Traceability is maintained via:

Requirement_ID → Control_ID → Implementation_Ref → Evidence_ID

Mapping artifacts:
- mapping/mapping-template.csv
- Control catalog YAML
- Evidence index

Status tracking fields include:
- Planned
- In Progress
- Implemented
- Verified

## 8. Assurance Model

The standards profile assumes:
- Controls are implemented via automation where possible
- Validation occurs in CI/CD
- Drift detection is enforced
- Evidence is generated programmatically where feasible

Compliance posture is therefore:

	Continuously evaluated, not point-in-time assessed.

## 9. Public Repository Constraints

Because this is a public repository:
- Only requirement IDs are referenced
- No proprietary IEC text is reproduced
- All diagrams are sanitized
- Evidence artifacts are referenced by ID only

Sensitive compliance artifacts must be stored in secure systems.

## 10. Profile Boundaries

This standards profile:

✔ Defines structure for IEC 62443 alignment  
✔ Enables repeatable compliance engineering  
✔ Supports traceable automation  

It does not:

✖ Perform risk assessment (see 04-risk-assumptions.md)  
✖ Guarantee certification  
✖ Replace formal audit  
