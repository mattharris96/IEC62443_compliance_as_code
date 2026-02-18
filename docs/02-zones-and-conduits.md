# Zones & Conduits (Template)

## Purpose
Document your zones, conduits, trust boundaries, and the controls applied to each conduit.

## Diagram (Mermaid)

```mermaid
flowchart LR
  %% Zones as subgraphs; conduits as labeled edges.

  subgraph Z_IT["Zone: Enterprise / IT (Example)"]
    IT_ID["Identity Services"]
    IT_OPS["IT Ops / Tooling"]
  end

  subgraph Z_DMZ["Zone: Boundary / DMZ (Example)"]
    DMZ_JUMP["Access Broker / Jump Service"]
    DMZ_MFT["Managed File Transfer Gateway"]
    DMZ_MON["Monitoring Relay"]
  end

  subgraph Z_SUP["Zone: OT Supervisory (Example)"]
    SUP_HMI["Supervisory / HMI"]
    SUP_HIST["Historian / Data Services"]
  end

  subgraph Z_CTRL["Zone: OT Control (Example)"]
    CTRL_PLC["Controllers / PLCs"]
    CTRL_IO["Remote I/O / Field Gateways"]
  end

  %% Conduits (examples)
  IT_ID -->|"C-01: Auth (restricted services, strong auth, audit logging)"| DMZ_JUMP
  IT_OPS -->|"C-02: Admin access (jump-only, approvals, session logging)"| DMZ_JUMP
  DMZ_MFT -->|"C-03: File transfer (allowlist, integrity checks, malware policy)"| SUP_HIST
  DMZ_MON -->|"C-04: Telemetry (least privilege, integrity, retention)"| SUP_HMI
  SUP_HMI -->|"C-05: Supervisory→Control (protocol allowlist, segmentation, monitoring)"| CTRL_PLC
  SUP_HIST -->|"C-06: Data replication (directional controls, integrity)"| SUP_HMI
```

## Conduit Register (template)

| Conduit ID | From Zone   | To Zone  | Purpose           | Allowed Services | Control Intent                     | Evidence IDs |
| ---------- | ----------- | -------- | ----------------- | ---------------- | ---------------------------------- | ------------ |
| C-01       | IT          | Boundary | Auth              | e.g., 443/LDAPS  | strong auth, least privilege, logs | EVID-###     |
| C-05       | Supervisory | Control  | Control protocols | allowlist only   | segmentation, monitoring           | EVID-###     |

## Note this is a public repo therefore:

*   Keep diagrams generic and sanitized.
*   Store sensitive diagrams/evidence in private storage and reference them via Evidence IDs only.
