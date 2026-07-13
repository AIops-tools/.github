# AIops-tools

> **Governed AI operations tooling for infrastructure** — audit, budget, undo, and graduated approval built into every tool.

AI agents are great at infrastructure ops, right up until something goes wrong in
production. **AIops-tools** is a family of MCP servers + CLIs that wrap real
infrastructure platforms with a **governance harness**, so an agent's actions are:

- **Audited** — every operation logged to a local SQLite trail (who / what / why / when), secret-redacted.
- **Bounded** — per-process token/call budget + a runaway-loop breaker (no more "one operation, 26k tokens").
- **Reversible** — write operations record an inverse **undo token** wherever a clean inverse exists.
- **Graduated** — risk tiers gate writes by environment/tag; the highest tiers require a recorded approver.
- **Safe by default** — destructive ops need double confirmation + `--dry-run`; all API text is sanitized.

Every tool is **self-contained** (the harness is bundled — no shared runtime dependency) and ships on **PyPI**, the **MCP Registry**, and **ClawHub**.

## Published tools

| Tool | Platform | Install | MCP tools |
|------|----------|---------|:--------:|
| [**proxmox-aiops**](https://github.com/AIops-tools/Proxmox-AIops) | Proxmox VE — VMs, LXC, snapshots, cluster, storage, backups, HA, pools, firewall | `pip install proxmox-aiops` | 39 |
| [**veeam-aiops**](https://github.com/AIops-tools/Veeam-AIops) | Veeam Backup & Replication — jobs, restore, repositories, sessions, infrastructure | `pip install veeam-aiops` | 21 |
| [**k8s-aiops**](https://github.com/AIops-tools/K8s-AIops) | Kubernetes — k3s / EKS / GKE / AKS (workloads, batch, config, storage, networking, rollouts) | `pip install k8s-aiops` | 51 |
| [**network-aiops**](https://github.com/AIops-tools/Network-AIops) | Network devices via NAPALM — Cisco IOS/NX-OS/IOS-XR, Arista EOS, Juniper Junos + NetBox | `pip install network-aiops` | 28 |
| [**fabric-aiops**](https://github.com/AIops-tools/Fabric-AIops) | Network **controllers** — Cisco Meraki Dashboard API (org→network→device); uplink loss/latency RCA, fleet health score, config-template drift, guarded remediation | `pip install fabric-aiops` | 32 |
| [**truenas-aiops**](https://github.com/AIops-tools/TrueNAS-AIops) | TrueNAS SCALE storage — pools, datasets, snapshots, disks, alerts, services | `pip install truenas-aiops` | 21 |
| [**endpoint-aiops**](https://github.com/AIops-tools/Endpoint-AIops) | Managed-endpoint fleets (thin clients / VDI) — login-storm & patch/config-drift analysis, inventory, guarded remediation | `pip install endpoint-aiops` | 9 |
| [**nutanix-aiops**](https://github.com/AIops-tools/Nutanix-AIops) | Nutanix Prism Central (v4) — clusters, VMs (AHV + ESXi), storage, network, snapshots/DR, alerts, LCM; auto ETag + pagination | `pip install nutanix-aiops` | 47 |
| [**ceph-aiops**](https://github.com/AIops-tools/Ceph-AIops) | Ceph via ceph-mgr Dashboard REST — HEALTH_WARN root-cause analysis, OSD/PG/pool/RBD/CephFS/RGW, recovery, capacity | `pip install ceph-aiops` | 35 |
| [**inference-aiops**](https://github.com/AIops-tools/Inference-AIops) | GPU inference clusters (vLLM + Ray Serve/Jobs) — latency/utilization RCA, replica scaling, drain, model lifecycle, cost | `pip install inference-aiops` | 30 |
| [**monitoring-aiops**](https://github.com/AIops-tools/Monitoring-AIops) | SolarWinds Orion (SWIS/SWQL) + Paessler PRTG — canned SWQL, alert dedup/rollup, health, maintenance windows | `pip install monitoring-aiops` | 31 |
| [**compliance-aiops**](https://github.com/AIops-tools/Compliance-AIops) | **Meta-tool** — turns the audit trails these tools already write into framework-mapped (HIPAA/PCI-DSS/SOC 2/GDPR), hash-chain-sealed evidence bundles | `pip install compliance-aiops` | 15 |
| [**ai-guardian**](https://github.com/AIops-tools/AI-Guardian) | On-endpoint local-LLM (Ollama) observability + governance — model allow/deny policy, provenance drift, a deterministic secrets/PII/jailbreak prompt scanner, and route-through guarding | `pip install ai-guardian-aiops` | 18 |

> **Industrial / OT?** The OT line (formerly `ot-aiops`) has moved to its own org — **[Industrial-AIOps](https://github.com/industrial-aiops)** — and is now [**`iaiops`**](https://github.com/industrial-aiops/industrial-aiops) (`pip install iaiops`): OPC-UA, Modbus, S7comm, Mitsubishi MC, MTConnect, MQTT/Sparkplug B, EtherNet/IP, EtherCAT, and **SECS/GEM** for semiconductor / display fabs.

## How it works

Each tool exposes **both a CLI and an MCP server** (`<tool> mcp`, stdio transport).
Point any MCP client (Claude, etc.) at it. Configuration and the audit/undo/policy
store live under `~/.<tool>/` (relocatable via `<TOOL>_AIOPS_HOME`). Credentials are
kept in an **encrypted store** (`secrets.enc`, Fernet + master password) — never in
plaintext. A friendly `<tool> init` wizard walks you through first-time setup.

```bash
pip install proxmox-aiops          # or pipx / uv tool install
proxmox-aiops init                 # interactive setup (encrypts your credentials)
proxmox-aiops doctor               # verify connectivity
proxmox-aiops mcp                  # run as an MCP server
```

## License & affiliation

MIT licensed. Community-maintained. **Not affiliated with, endorsed by, or sponsored
by** the vendors of the platforms these tools operate (Proxmox Server Solutions GmbH,
Veeam Software, the CNCF / Kubernetes project, etc.); all trademarks belong to their
respective owners.
