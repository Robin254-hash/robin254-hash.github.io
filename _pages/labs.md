---
title: "Labs & Challenges"
layout: single
permalink: /labs/
author_profile: true
---

This page documents my hands-on cybersecurity learning. Each write-up aims to explain the objective, my approach, the tools used, what I observed, challenges I encountered, and what I learned.

I distinguish between completed learning modules and work that is still in progress. Screenshots and command output will be added as I capture and verify them.

## Home lab

### 🛡️ Wazuh + Metasploitable SOC Lab
**Focus:** SIEM, virtual networking, security monitoring, reconnaissance, alert investigation  
**Status:** In progress

I am building an isolated VirtualBox lab with Wazuh, Kali Linux, and Metasploitable 2. The next steps are to resolve dashboard connectivity, confirm communication between the lab VMs, and test which events can be collected and investigated.

[Read the lab plan and progress →](/projects/wazuh-metasploitable/)

## Hack The Box Academy

### 🪟 Windows Fundamentals
**Focus:** Windows environment, processes, services, users, and system information  
**Status:** Completed learning module

Practiced navigating a Windows environment and reviewing system information that can support troubleshooting and security analysis.

### 🐧 Linux Fundamentals
**Focus:** Linux CLI, files, permissions, processes, services, and networking  
**Status:** Completed learning module

Practiced common terminal commands, file and directory navigation, permissions, process and service checks, and basic network inspection.

### 🌐 Introduction to Web Applications
**Focus:** Front-end and back-end components, web servers, application logic, and databases  
**Status:** Completed learning module

Built a foundational understanding of how browser requests interact with web servers, application logic, and databases, and why each layer matters when assessing web security.

### 🚀 Getting Started
**Focus:** Penetration-testing workflow, enumeration, exploitation concepts, and privilege escalation  
**Status:** In progress / notes being developed

Working through the stages of a controlled assessment, interpreting tool output, researching unfamiliar commands, and documenting both successful steps and dead ends.

### 🌐 Introduction to Networking
**Focus:** Networking concepts, subnetting, services, vendor-specific information, key exchange, and cryptography  
**Status:** Notes in progress

Developing a stronger foundation in how systems communicate and how networking and cryptographic concepts support security.

### 🔎 Vulnerability Assessment
**Focus:** Vulnerability scanning, Nessus, interpreting findings, and remediation  
**Status:** Notes in progress

Learning how vulnerability assessment tools identify potential weaknesses and how findings should be reviewed rather than treated as confirmed exploitable vulnerabilities.

## TryHackMe

### 🐍 Python Basics
**Focus:** Python fundamentals for automation and problem-solving  
**Status:** Learning notes

### 🕵️ Passive Reconnaissance
**Focus:** Gathering information from publicly available sources  
**Status:** Learning notes

### 🧠 Threat Intelligence Tools
**Focus:** Exploring threat-intelligence resources and interpreting indicators and context  
**Status:** Learning notes

## My write-up format

Each detailed write-up will use this structure:

1. **Objective** — what the exercise was intended to teach.
2. **Approach** — the steps I took and why.
3. **Tools and commands** — what I used and what the output meant.
4. **Evidence** — screenshots or sanitized output captured from my own lab.
5. **Challenges** — errors, dead ends, and how I investigated them.
6. **Lessons learned** — what I can explain or do better after the exercise.
7. **Security relevance** — how the lesson applies to monitoring, investigation, or defensive practice.

*Training notes are for learning and portfolio documentation. Any testing against vulnerable systems is performed only in authorized, isolated environments.*
