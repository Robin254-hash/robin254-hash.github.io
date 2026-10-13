---
title: "Wazuh + Metasploitable SOC Lab"
layout: single
permalink: /projects/wazuh-metasploitable/
author_profile: true
---

**Status: Complete**  
**Environment:** VirtualBox  
**Components:** Wazuh, Kali Linux, Metasploitable 2

## 1. Overview

This project involved setting up a small cybersecurity home lab using Wazuh, Kali Linux, and Metasploitable 3. The objective was to understand how a Security Information and Event Management (SIEM) platform can be used to monitor security events and investigate activity generated during controlled security testing.
Kali Linux was used to perform network reconnaissance and authentication testing against Metasploitable 3, an intentionally vulnerable target. Wazuh was used to review the resulting security events and alerts.
The project provided practical exposure to virtual lab networking, Linux commands, service enumeration, security event monitoring, and basic SOC investigation.

## 2. Objectives

- Deploy Wazuh as the central security monitoring platform.
- Configure Metasploitable 3 as an intentionally vulnerable lab target.
- Connect the virtual machines through a suitable VirtualBox network.
- Identify the IP addresses assigned to the lab systems.
- Perform controlled Nmap reconnaissance against the target.
- Conduct an authorized Hydra authentication-testing exercise.
- Review the resulting events and alerts in Wazuh.
- Document the setup process, evidence, and lessons learned.


## 3. Architecture

Layout:

```text
                    VirtualBox
                        |
              Isolated Cyber Lab Network
                 /         |         \
                /          |          \
           Kali Linux     Wazuh    Metasploitable 3
           Test host      SIEM      Vulnerable target
```

### 3.1 Environment and setup notes

| Component | Purpose | 
|---|---|
| Wazuh VM | Central security monitoring |
| Kali Linux VM | Authorized testing and diagnostics |
| Metasploitable 3 VM | Intentionally vulnerable target | 
| Oracle VirtualBox | Runs the Virtual Machines |
| Nmap | Enumeration | 
| Hydra | Controlled authentication Testing |

## Existing environment: 
VirtualBox and Kali Linux were already installed before this project began.

## 5. Downloading and Preparation of VMs
### 5.1 Wazuh
I obtained the Wazuh virtual machine from the official Wazuh documentation:
https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html
The pre-built virtual machine was imported into VirtualBox. After importing it, I reviewed its virtual machine settings, started it, and allowed the Wazuh services to initialize.
The Wazuh deployment includes the components used for security monitoring and analysis: the manager, indexer, and dashboard.

### 5.2 Metaspolitable 3
I obtained Metasploitable 3 from the official Rapid7 project repository:
https://github.com/rapid7/metasploitable3
Metasploitable 3 was prepared as the vulnerable Linux target for the lab. After obtaining the VM, I checked its VirtualBox settings and configured its network adapter to communicate with the other lab systems.

## 6 Network Configuration
The next step was to configure the network so that the lab machines could communicate.
I configured the relevant VirtualBox network adapters to use the laboratory network. I then started the virtual machines and identified their assigned IP addresses.
The following table records the addresses used in my environment. 

| Machine | IP address |
|---|---|
| Wazuh VM | 10.0.2.15 |
| Metasploitable 3 VM |10.0.2.3 | 

### Commands used to identify settings 
```bash
ip address
```
The commands were used to identify the machine names, network interfaces, assigned IP addresses, and available routes.

### Connectivity Verification
```bash
ping -c 4 10.0.2.3
ping 10.0.2.15
```
Successful replies confirmed basic IP connectivity where ICMP traffic was permitted.
Evidence: Insert a screenshot showing the network configuration and successful connectivity tests.

I accessed the Wazuh web interface using the following:
```bash
https://10.0.2.15
```
Which i logged in using the provided credentials

## 7 Checking the Target and Its Services Using Nmap
Before performing the testing activities, I confirmed the target IP address and checked which services were exposed.
From Kali Linux, I ran:
```bash
nmap -sV --top-ports 100 10.0.2.3
```
This command scanned the 100 most common TCP ports and attempted to identify the services and versions running on the target.
The scan output helped me identify the services exposed by the target and provided a baseline for the subsequent investigation.
Evidence: Insert the actual Nmap terminal screenshot, ensuring the target IP and scan output are visible.

## 8. Conducting Controlled Authentication Testing Using Hydra
After the reconnaissance stage, I performed an authorized authentication-testing exercise against a service on Metasploitable 3 using Hydra.
The purpose was to understand how repeated login attempts could generate authentication-related events and how such events might be investigated through a SIEM.
I ran the test only against my intentionally vulnerable lab target using lab test credentials and a controlled wordlist.
Command used: Insert the actual Hydra command you ran, with any passwords or sensitive credentials removed.
For example, a controlled SSH test using a designated lab account and a small test wordlist follows this pattern:
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.2.3
```
This is an example, not a claim that it was the exact command used in my test. The username, wordlist path, service, and target must match the actual exercise.
The results were reviewed to distinguish failed authentication attempts from any reported successful login. 

## 9. Observing Events in Wazuh
After running the Nmap and Hydra exercises, I opened the Wazuh dashboard to review the security events and alerts generated during testing.
I selected the relevant time range and inspected the available alert details, including the rule ID, rule description, severity level, timestamp, and associated agent or IP address where available.
This stage was important because it allowed me to move beyond running testing tools and begin examining the security information available to a monitoring analyst.
The observed results confirmed that Wazuh displayed security alerts associated with activity in my lab. The exact interpretation of each alert depended on the rule that matched and the event information collected.

## 10. Initial Findings
The initial lab exercises provided the following observations:
- The Wazuh virtual machine was deployed, and I could access its dashboard.
- The lab systems were assigned IP addresses and could communicate over the configured network.
- Nmap identified exposed services on the Metasploitable 3 target.
- Hydra was used to conduct controlled authentication testing in the isolated lab.
- Security alerts and event information were visible in Wazuh following the testing activities.
  
Further investigation is needed to establish precisely which events corresponded to each test, whether the target's authentication logs were collected, and whether the alerts provide enough evidence to distinguish normal testing from suspicious activity.

## 11. Challenges and Lessons Learned
One of the main learning areas was understanding the relationship between the testing machine, the target, and the SIEM. Running a command on Kali does not automatically mean that Wazuh will record every packet or action. Visibility depends on the data collected from monitored endpoints and the applicable detection rules.

The exercises also helped me become more familiar with IP addressing, service enumeration, authentication testing, Wazuh agents, and alert details. I learned the importance of examining timestamps, event descriptions, and rule information before deciding what an alert means.
The next stage of the project will focus on improving endpoint log visibility, investigating individual alerts in more detail, and documenting detection and remediation recommendations.

## 12. Conclusion
This project established a practical foundation for learning security monitoring with Wazuh. By using Kali Linux to test an isolated Metasploitable 3 target, I was able to observe security alerts in the Wazuh dashboard and begin examining how testing activity can be investigated. The experience introduced me to the basic workflow of generating activity, reviewing available evidence, and interpreting security events. I will continue developing the lab by validating the source of individual alerts, improving log collection, and documenting further SOC investigations.
