# AIops-tools

> **Governed AI operations tooling for infrastructure** — unbypassable audit, budget, and undo built into every tool.

AI agents are great at infrastructure ops, right up until something goes wrong in
production. **AIops-tools** is a family of MCP servers + CLIs that wrap real
infrastructure platforms with a **governance harness**. Each tool delivers the
operation accurately and efficiently and records every step; whether a write is
permitted is the agent's judgement or the connecting account's permissions — not
the tool's. So an agent's actions are:

- **Audited** — every operation, over MCP **and** the CLI, logged to a local SQLite trail (who / what / when), secret-redacted. There is no unaudited entry point.
- **Bounded** — a runaway-loop breaker + optional per-process call/time ceilings (no more "one operation, 26k tokens"). A safety backstop, not an authorization gate.
- **Reversible** — write operations record an inverse **undo token** wherever a clean inverse exists.
- **Safe by default** — destructive ops need double confirmation + `--dry-run`; all API text is sanitized.

Every tool is **self-contained** (the harness is bundled — no shared runtime dependency) and ships on **PyPI**, the **MCP Registry**, and **ClawHub**.

## Published tools

| Tool | Platform | Install | MCP tools |
|------|----------|---------|:--------:|
| [**proxmox-aiops**](https://github.com/AIops-tools/Proxmox-AIops) | Proxmox VE — VMs, LXC, snapshots, cluster, storage, backups, HA, pools, firewall; node-pressure & guest-health RCA | `pip install proxmox-aiops` | 43 |
| [**veeam-aiops**](https://github.com/AIops-tools/Veeam-AIops) | Veeam Backup & Replication — jobs, restore, repositories, sessions, infrastructure; job-failure & repository-capacity RCA | `pip install veeam-aiops` | 25 |
| [**k8s-aiops**](https://github.com/AIops-tools/K8s-AIops) | Kubernetes — k3s / EKS / GKE / AKS (workloads, batch, config, storage, networking, rollouts); pod-health & workload-readiness RCA | `pip install k8s-aiops` | 55 |
| [**network-aiops**](https://github.com/AIops-tools/Network-AIops) | Network devices via NAPALM — Cisco IOS/NX-OS/IOS-XR, Arista EOS, Juniper Junos + NetBox; interface-health & BGP-neighbor RCA | `pip install network-aiops` | 33 |
| [**fabric-aiops**](https://github.com/AIops-tools/Fabric-AIops) | Network **controllers** — Cisco Meraki, Cisco Catalyst Center, Arista CloudVision, Ubiquiti UniFi (org→network→device); uplink loss/latency RCA, fleet health score, config-template drift, guarded remediation | `pip install fabric-aiops` | 34 |
| [**truenas-aiops**](https://github.com/AIops-tools/TrueNAS-AIops) | TrueNAS SCALE storage — pools, datasets, snapshots, disks, alerts, services; pool-health & alert/capacity RCA | `pip install truenas-aiops` | 25 |
| [**endpoint-aiops**](https://github.com/AIops-tools/Endpoint-AIops) | Managed-endpoint fleets (thin clients / VDI) — login-storm & patch/config-drift analysis, inventory, guarded remediation | `pip install endpoint-aiops` | 13 |
| [**nutanix-aiops**](https://github.com/AIops-tools/Nutanix-AIops) | Nutanix Prism Central (v4) — clusters, VMs (AHV + ESXi), storage, network, snapshots/DR, alerts, LCM; cluster-health & alert-triage RCA; auto ETag + pagination | `pip install nutanix-aiops` | 51 |
| [**ceph-aiops**](https://github.com/AIops-tools/Ceph-AIops) | Ceph via ceph-mgr Dashboard REST — HEALTH_WARN root-cause analysis, OSD/PG/pool/RBD/CephFS/RGW, recovery, capacity | `pip install ceph-aiops` | 37 |
| [**inference-aiops**](https://github.com/AIops-tools/Inference-AIops) | GPU inference clusters (vLLM + Ray Serve/Jobs) — latency/utilization RCA, replica scaling, drain, model lifecycle, cost | `pip install inference-aiops` | 39 |
| [**monitoring-aiops**](https://github.com/AIops-tools/Monitoring-AIops) | SolarWinds Orion (SWIS/SWQL) + Paessler PRTG + Zabbix — canned SWQL, alert dedup/rollup, health, maintenance windows | `pip install monitoring-aiops` | 42 |
| [**compliance-aiops**](https://github.com/AIops-tools/Compliance-AIops) | **Meta-tool** — turns the audit trails these tools already write into framework-mapped (HIPAA/PCI-DSS/SOC 2/GDPR), hash-chain-sealed evidence bundles | `pip install compliance-aiops` | 18 |
| [**ai-guardian**](https://github.com/AIops-tools/AI-Guardian) | On-endpoint local-LLM (Ollama) observability + governance — model allow/deny policy, provenance drift, a deterministic secrets/PII/jailbreak prompt scanner, and route-through guarding | `pip install ai-guardian-aiops` | 20 |
| [**postgres-aiops**](https://github.com/AIops-tools/Postgres-AIops) | PostgreSQL DBA-ops — slow-query / bloat / blocking-lock RCA, indexes, vacuum/analyze, replication lag, guarded remediation | `pip install postgres-aiops` | 35 |
| [**observability-aiops**](https://github.com/AIops-tools/Observability-AIops) | Self-hosted observability — Prometheus + Grafana: firing-alert & scrape-target RCA, alert noise/flap analysis, silences, dashboards | `pip install observability-aiops` | 39 |
| [**firewall-aiops**](https://github.com/AIops-tools/Firewall-AIops) | OPNsense + pfSense firewalls — gateway-health / rule-shadow / blocked-traffic RCA, guarded rule & alias writes | `pip install firewall-aiops` | 35 |
| [**container-host-aiops**](https://github.com/AIops-tools/Container-Host-AIops) | Docker + Portainer container hosts (non-Kubernetes) — restart-loop / resource-pressure / image-&-volume-bloat RCA, guarded lifecycle writes | `pip install container-host-aiops` | 38 |
| [**mysql-aiops**](https://github.com/AIops-tools/MySQL-AIops) | MySQL + MariaDB DBA-ops — slow-query / replication-lag / blocking-lock RCA, index & table maintenance, guarded remediation | `pip install mysql-aiops` | 35 |
| [**proxy-aiops**](https://github.com/AIops-tools/Proxy-AIops) | Reverse proxies — Traefik / Caddy / HAProxy: route & backend health RCA, certificate visibility, guarded config writes | `pip install proxy-aiops` | 28 |
| [**queue-aiops**](https://github.com/AIops-tools/Queue-AIops) | Middleware — Redis + RabbitMQ: queue-depth / consumer-lag / memory-pressure RCA, guarded queue & key operations | `pip install queue-aiops` | 28 |
| [**minio-aiops**](https://github.com/AIops-tools/MinIO-AIops) | MinIO object storage — bucket / capacity / replication health, policy & lifecycle visibility, guarded bucket writes | `pip install minio-aiops` | 31 |
| [**xcpng-aiops**](https://github.com/AIops-tools/XCPng-AIops) | XCP-ng via Xen Orchestra — VMs, snapshots, hosts, pools, storage repositories, guarded lifecycle writes | `pip install xcpng-aiops` | 29 |
| [**identity-aiops**](https://github.com/AIops-tools/Identity-AIops) | SSO / IAM — Keycloak + Authentik: realm / client / user health, login-failure analysis, guarded identity writes | `pip install identity-aiops` | 29 |
| [**cicd-aiops**](https://github.com/AIops-tools/CICD-AIops) | Self-managed CI — GitLab + Gitea: pipeline-failure RCA, runner health, job & artifact hygiene, guarded pipeline operations | `pip install cicd-aiops` | 28 |

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
