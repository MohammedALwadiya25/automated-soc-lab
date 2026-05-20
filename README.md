
# Automated SOC Lab — Graduation Project

> A fully automated Security Operations Center (SOC) built on open-source tools,
> designed for detection, correlation, alerting, and automated incident response.

## Architecture Overview

| Component | Role | IP |
|---|---|---|
| OPNsense | Firewall + Router + Suricata IDS/IPS | 192.168.100.1 |
| Wazuh | SIEM (Manager + Indexer + Dashboard) | 192.168.100.10 |
| n8n | SOAR / Automation | 192.168.100.20 |
| Victim VM | Target endpoint (Ubuntu) | 192.168.100.50 |
| Kali Linux | Attacker simulation | 192.168.100.99 |

## SOC Pipeline



Attack → Suricata IDS (OPNsense) → EVE JSON log
↓
Wazuh Agent → Wazuh Manager
↓
Correlation + Rules Engine
↓
n8n Webhook → Workflow
↙           ↘
Gmail alert    Telegram alert




## Project Phases

| Phase | Status | Documentation |
|---|---|---|
| Phase 1 — Network design & VM provisioning | 🔄 In progress | [docs/phase-1](docs/phase-1-network-design/README.md) |
| Phase 2 — OPNsense + Suricata | ⏳ Pending | [docs/phase-2](docs/phase-2-opnsense-suricata/README.md) |
| Phase 3 — Wazuh SIEM | ⏳ Pending | [docs/phase-3](docs/phase-3-wazuh-siem/README.md) |
| Phase 4 — Suricata → Wazuh integration | ⏳ Pending | [docs/phase-4](docs/phase-4-suricata-wazuh-integration/README.md) |
| Phase 5 — n8n SOAR + alerting | ⏳ Pending | [docs/phase-5](docs/phase-5-n8n-soar-alerting/README.md) |
| Phase 6 — Attack simulations | ⏳ Pending | [docs/phase-6](docs/phase-6-attack-simulations/README.md) |

## Tools Used

- **OPNsense** — open-source firewall/router (FreeBSD based)
- **Suricata** — network IDS/IPS engine
- **Wazuh** — open-source SIEM and XDR platform
- **n8n** — open-source workflow automation (SOAR)
- **VMware Workstation** — hypervisor
- **Kali Linux** — penetration testing OS
- **Gmail + Telegram** — alert notification channels

## Environment

- Hypervisor: VMware Workstation
- Network: Isolated Host-Only (VMnet2) — 192.168.100.0/24
- All VMs air-gapped from production networks

## Author

**[Your Name]**
Graduation Project — ALaqsa University— 2026