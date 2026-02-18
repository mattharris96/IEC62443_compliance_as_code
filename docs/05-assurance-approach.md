# 05 – Assurance Approach

## 1. Purpose

This document defines how assurance is achieved, measured, and demonstrated within the IEC62443 Compliance as Code repository.

Assurance in this context means:
- Controls are implemented as defined
- Controls are validated automatically
- Evidence is generated and traceable
- Compliance posture is continuously evaluated

This approach supports alignment with IEC 62443 system requirements without replacing formal certification processes.

## 2. Assurance Principles

The assurance model is based on the following principles:
- Automate where possible
- Version control everything
- Fail non-compliant configurations early
- Generate machine-verifiable evidence
- Maintain requirement traceability

Compliance is treated as an engineering outcome, not a point-in-time document exercise.

## 3. Assurance Layers

Assurance is achieved across five layers:

### 3.1 Architectural Assurance

Validated through:
- Zone definitions (02-zones-and-conduits.md)
- Explicit conduit declarations
- Security Level Targets (03-security-level-targets.md)
- Peer review of architectural changes

Objective:
Ensure trust boundaries and flows are explicitly defined and justified.

### 3.2 Control Assurance

Controls are defined in:

controls/controls-catalog.yml

Each control must include:
- Requirement IDs (FR/SR)
- Intent statement
- Implementation references
- Evidence types

Validation occurs by:
- Reviewing implementation references
- Executing automation roles
- Generating evidence artifacts

### 3.3 Implementation Assurance (Automation Enforcement)

Controls are implemented and verified using:
- Ansible roles
- Infrastructure-as-Code patterns
- Configuration enforcement tasks
- Drift detection checks

Each automation role should:
	1.	Configure baseline securely
	2.	Verify configuration state
	3.	Produce structured output (JSON/Markdown)

Example enforcement flow:

Apply Configuration
      ↓
Run Validation Checks
      ↓
Produce Compliance Output
      ↓
Store Evidence Reference

### 3.4 CI/CD Pipeline Assurance

All changes must pass automated validation before merge.

Typical workflow:

Code Commit
      ↓
Pull Request
      ↓
Pipeline Validation
      ↓
Policy Linting
      ↓
Control Mapping Check
      ↓
Compliance Report Generated
      ↓
Merge Approval

Pipeline checks may include:
- YAML schema validation
- Control ID verification
- Mapping completeness validation
- Evidence ID format checks
- Automation dry-run validation

Non-compliant changes must fail the pipeline.

### 3.5 Evidence Assurance

This repository stores evidence metadata only.

Evidence artifacts are:
- Generated via automation
- Indexed in evidence/evidence-index.md
- Referenced using Evidence IDs

Evidence types include:
- Configuration extracts (sanitized)
- Policy definitions
- Test results
- Log samples (redacted)
- Change records

Sensitive artifacts must be stored in secure systems.

## 4. Security Level Assurance

Security Levels are validated through:
- Control coverage analysis
- Automated configuration verification
- Mapping completeness review

Security Level model:

SL-T  → Target (defined in 03-security-level-targets.md)
SL-A  → Achieved (validated via automation & evidence)

If required controls are not implemented or validated:
- SL-A cannot equal SL-T
- Status must reflect “Planned” or “In Progress”

## 5. Requirement Traceability Assurance

Traceability chain:

Requirement_ID. 
      ↓. 
Control_ID. 
      ↓. 
Implementation_Ref. 
      ↓. 
Automation Role. 
      ↓. 
Evidence_ID. 

Validation activities include:
- Ensuring every mapped requirement has a Control_ID
- Ensuring every control has implementation references
- Ensuring every implementation produces evidence
- Ensuring mapping file status reflects reality

Mapping file:

mapping/mapping-template.csv

## 6. Drift Detection

Assurance requires ongoing validation.

Drift detection mechanisms may include:
- Scheduled automation runs
- Configuration comparison tasks
- Compliance re-evaluation reports
- Baseline integrity checks

If drift is detected:
- Evidence must reflect deviation
- Status must be updated
- Remediation must be tracked

## 7. Manual Assurance Components

Certain activities remain partially manual:
- Architectural reviews
- Risk assumption updates (04-risk-assumptions.md)
- Security Level Target adjustments
- Audit preparation packaging

Manual activities must still be:
- Version controlled
- Peer reviewed
- Traceable to requirement IDs

## 8. Assurance Metrics

The following indicators may be tracked:
- % of requirements mapped
- % of controls implemented
- % of controls verified automatically
- Number of failed compliance checks
- Drift detection frequency
- Evidence completeness status

Metrics may be generated as:
- Markdown summaries
- JSON reports
- Pipeline artifacts

## 9. Audit Readiness Model

Assurance artifacts are structured to support audit preparation:
- Control catalog
- Mapping file
- Evidence index
- Automation outputs
- Zone/conduit documentation

The repository enables generation of an audit pack outline (see 06-audit-pack-outline.md).

## 10. Public Repository Constraints

Because this is a public repository:
- Evidence files contain metadata only
- Logs and configs must be sanitized
- Real topology data is excluded
- No proprietary IEC text is included

Assurance is demonstrated structurally, not operationally.

## 11. Continuous Improvement

The assurance approach must evolve when:
- New controls are added
- Security Levels change
- New zones or conduits are introduced
- Automation capabilities expand
- Risk assumptions are updated

All updates must:
- Maintain traceability
- Preserve mapping integrity
- Be validated via CI/CD

## 12. Summary

This assurance model ensures that:
- Security controls are explicit
- Enforcement is automated
- Compliance is continuously evaluated
- Evidence is structured and traceable
- Security Levels are measurable
- Architecture and controls remain aligned

Assurance is therefore:

	Continuous, version-controlled, and automation-driven.