# Phase 1 — Network Design & VM Provisioning
=

## Objectives

- Create an isolated virtual lab network (VMnet2)
- Provision all 5 virtual machines with correct specs and adapters
- Verify VM-to-VM connectivity before any software installation

## Network Design

| VM | IP Address | Subnet | Gateway | Adapters |
|---|---|---|---|---|
| OPNsense (FW) | 192.168.100.1 | /24 | — | NAT + VMnet2 |
| Wazuh SIEM | 192.168.100.10 | /24 | 192.168.100.1 | VMnet2 |
| n8n SOAR | runs on Wazuh VM | /24 | 192.168.100.1 | VMnet2 |
| Victim VM | 192.168.100.50 | /24 | 192.168.100.1 | VMnet2 |
| Kali Attacker | 192.168.100.99 | /24 | 192.168.100.1 | VMnet2 |

## VM Specifications

| VM | OS | RAM | vCPU | Disk |
|---|---|---|---|---|---|
| OPNsense | FreeBSD 64-bit | 1 GB | 2 | 16 GB |  
| Wazuh | Official OVA 4.14.5 | 6 GB | 4 | 50 GB | 
| Victim | Ubuntu 22.04 Server | 1 GB | 2 | 20 GB | 
| Kali | Kali Linux 64-bit | 2 GB | 2 | 40 GB | 

## Network Notes

- VMnet2 configured as Host-only, subnet 192.168.100.0/24, DHCP disabled
- n8n will run as a Docker container on the Wazuh OVA to save RAM
- Total VM RAM usage: ~10 GB leaving ~6 GB for Windows host



## Issues Encountered & Solutions

| Issue | Cause | Solution |
|---|---|---|
| touch command not found | Windows PowerShell doesn't support Linux commands | Used New-Item PowerShell cmdlet instead |
| Limited host RAM (16 GB) | Not enough for 5 full VMs | Installed n8n as Docker container on Wazuh OVA |

