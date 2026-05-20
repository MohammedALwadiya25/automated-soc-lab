# Phase 1 — Network Design & VM Provisioning

**Status:** 🔄 In progress

## Objectives

- Create an isolated virtual lab network (VMnet2)
- Provision all 5 virtual machines with correct specs and adapters
- Verify VM-to-VM connectivity before any software installation

## Network Design

| VM | IP Address | Subnet | Gateway | Adapters |
|---|---|---|---|---|
| OPNsense (FW) | 192.168.100.1 | /24 | — | NAT + VMnet2 |
| Wazuh SIEM | 192.168.100.10 | /24 | 192.168.100.1 | VMnet2 |
| n8n SOAR | 192.168.100.20 | /24 | 192.168.100.1 | VMnet2 |
| Victim VM | 192.168.100.50 | /24 | 192.168.100.1 | VMnet2 |
| Kali Attacker | 192.168.100.99 | /24 | 192.168.100.1 | VMnet2 |

## VM Specifications

| VM | OS | RAM | vCPU | Disk |
|---|---|---|---|---|
| OPNsense | FreeBSD 64-bit | 2 GB | 2 | 16 GB |
| Wazuh | Ubuntu 22.04 LTS | 8 GB | 4 | 80 GB |
| n8n | Ubuntu 22.04 LTS | 2 GB | 2 | 20 GB |
| Victim | Ubuntu 22.04 LTS | 2 GB | 2 | 20 GB |
| Kali | Kali Linux 2024 | 2 GB | 2 | 40 GB |

## Steps Completed

- [ ] VMnet2 created in VMware Virtual Network Editor
- [ ] OPNsense VM created
- [ ] Wazuh VM created
- [ ] n8n VM created
- [ ] Victim VM created
- [ ] Kali VM created
- [ ] All VMs boot successfully

## Screenshots

<!-- Add your screenshots here after each step -->
<!-- Example: ![VMnet2 config](../../screenshots/phase-1/vmnet2-config.png) -->

## Issues Encountered & Solutions

<!-- Document any problems you hit and how you solved them -->
<!-- This section is gold for your graduation report -->

| Issue | Cause | Solution |
|---|---|---|
| — | — | — |

## Completion Date

<!-- Fill in when phase is done -->