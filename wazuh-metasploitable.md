---
title: "Wazuh + Metasploitable SOC Lab"
layout: single
permalink: /projects/wazuh-metasploitable/
author_profile: true
---

**Status: In progress**  
**Environment:** VirtualBox  
**Planned components:** Wazuh, Kali Linux, Metasploitable 2

## 1. Overview

This project documents the development of an isolated cybersecurity home lab for practicing security monitoring and investigation. Wazuh will serve as the central monitoring platform, Kali Linux will be used for authorized testing, and Metasploitable 2 will act as an intentionally vulnerable target.

The goal is to learn how to build the environment, validate network connectivity, generate controlled activity, and investigate the logs or alerts that are actually available.

## 2. Objectives

- Deploy and access the Wazuh dashboard.
- Configure the virtual machines on a suitable isolated lab network.
- Verify connectivity between the systems.
- Identify services exposed by the lab target.
- Determine what relevant events are collected by Wazuh.
- Investigate available alerts and document limitations.
- Recommend defensive controls based on verified observations.

## 3. Architecture

Planned layout:

```text
                    VirtualBox
                        |
              Isolated Cyber Lab Network
                 /         |         \
                /          |          \
           Kali Linux     Wazuh    Metasploitable 2
           Test host      SIEM      Vulnerable target
```

The exact adapter configuration and IP addresses will be documented after connectivity is confirmed.

## 4. Environment and setup notes

| Component | Purpose | Progress |
|---|---|---|
| Wazuh VM | Central security monitoring | Installed; dashboard connectivity being checked |
| Kali Linux VM | Authorized testing and diagnostics | To be connected to the lab network |
| Metasploitable 2 VM | Intentionally vulnerable target | To be deployed/configured |
| VirtualBox network | Isolated communication between VMs | To be validated |

### Safety

Metasploitable is intentionally vulnerable. Keep it on an isolated host-only or appropriately configured internal lab network. Do not bridge it to a production network or expose it directly to the public Internet. Use NAT only when you understand which traffic is permitted; a NAT Network can allow connected VMs to communicate, but the configuration should be verified.

## 5. Planned workflow

### Step 1 — Verify Wazuh

Record the Wazuh VM's IP address and check the relevant services. Once reachable, open the dashboard using HTTPS and confirm that the login page loads.

Example diagnostic commands inside the Wazuh VM:

```bash
ip address
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

Service names and availability can vary by deployment. Record the actual output rather than assuming every service is running.

### Step 2 — Configure and test the virtual network

- Put the lab VMs on the intended isolated network.
- Check each VM's IP address and subnet.
- Test connectivity between the systems where permitted.
- Confirm the Wazuh dashboard is reachable from the intended browser/VM.
- Record errors and how they were resolved.

### Step 3 — Identify target services

After Metasploitable is configured and reachable, use a basic service scan from Kali within the isolated lab:

```bash
nmap -sV <METASPLOITABLE-IP>
```

Replace the placeholder with the target's actual lab IP. Save sanitized output and explain what the discovered services indicate.

### Step 4 — Investigate monitoring coverage

Review what data Wazuh actually receives. Do not assume a network scan will automatically create a Wazuh alert: Wazuh primarily analyses data sources configured for collection, and visibility depends on log sources, agents, rules, and configuration. Document whether the activity was visible, which logs were available, and any monitoring gaps.

### Step 5 — Record findings

For each verified observation, document:
- What activity was performed.
- What evidence was collected.
- What Wazuh did or did not show.
- Why the observation matters.
- What defensive improvement may help.

## 6. Evidence gallery

Screenshots will be added after I capture them from my own environment.

| Evidence to capture | What it should demonstrate |
|---|---|
| VirtualBox network settings | The intended isolated network configuration |
| Wazuh dashboard | Successful dashboard access |
| VM network addresses | The lab systems' actual addresses and subnet |
| Nmap output | Services observed on the authorized lab target |
| Wazuh alerts or event search | Actual events available for investigation |
| Investigation notes | Reasoning, findings, and recommendations |

Before publishing, redact passwords, tokens, public IPs where inappropriate, and any sensitive information.

## 7. Findings and lessons learned

**To be completed after testing.**

This section will record the actual connectivity outcome, monitoring visibility, any configuration changes, and lessons learned. I will not claim a detection or successful incident investigation until it has been observed and supported by evidence.

## 8. Next steps

- [ ] Resolve Wazuh dashboard connectivity.
- [ ] Confirm IP addressing and subnet for each VM.
- [ ] Deploy Metasploitable 2 safely.
- [ ] Verify connectivity from Kali.
- [ ] Perform controlled service enumeration.
- [ ] Review relevant logs and Wazuh alerts.
- [ ] Capture and sanitize screenshots.
- [ ] Write findings and remediation recommendations.

[← Back to projects](/projects/) · [Browse all labs](/labs/)
