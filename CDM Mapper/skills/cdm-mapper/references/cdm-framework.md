# Cyber Defense Matrix Framework Reference

Source: "Cyber Defense Matrix: The Essential Guide to Navigating the Cybersecurity Landscape" by Sounil Yu (2022, JupiterOne Press). Framework extended with NIST CSF 2.0 Govern function.

## Table of Contents
1. [Overview](#overview)
2. [Asset Classes](#asset-classes)
3. [Security Functions](#security-functions)
4. [Left of Boom vs Right of Boom](#left-of-boom-vs-right-of-boom)
5. [Key Disambiguations](#key-disambiguations)
6. [The Govern Function](#the-govern-function)
7. [Dependency Curves](#dependency-curves)

## Overview

The Cyber Defense Matrix is a MECE (mutually exclusive, collectively exhaustive) representation of the cybersecurity landscape. It combines 5 asset classes (Devices, Networks, Applications, Data, Users) with 6 security functions (Govern, Identify, Protect, Detect, Respond, Recover) to create a 30-cell grid.

The framework's power comes from its structure as a forcing function: it drives strict adherence to consistent functional definitions across all asset classes. You cannot label something IDENTIFY for one asset class and DETECT for a different asset class if the underlying activity is the same.

The CDM is strategic (30,000-foot view), not tactical. It helps organize and understand cybersecurity at a high level. For tactical-level detail, frameworks like MITRE ATT&CK may be more suitable.

## Asset Classes

### Devices
Workstations, servers, phones, tablets, IoT devices, containers, hosts, compute peripherals, storage devices, network devices, web cameras, infrastructure, etc. This class includes the operating system and firmware of these devices, as well as other software that is native or inherent to the device. Networking devices like switches and routers are included here because the devices themselves need to be considered separately from the communication paths they create.

### Networks
The communications channels, connections, and protocols that enable traffic to flow among devices and applications. This does NOT refer to the actual infrastructure (routers, switches) but rather to the paths themselves and the protocols used in those paths. This means areas such as DNS, BGP, email filtering, and web filtering also fall into this category. This class includes VPCs, VPNs, and CDNs.

Think of it as "the roads, not the cars." A router is a Device; the network path it creates is a Network.

**Critical distinction**: Networks are an abstraction of device configuration. A Cisco switch is a Device — it has firmware, an OS, possibly applications, it needs power and patching. Its software ensures connectivity follows rules, which *creates* networks. But the device can exist without a network existing. When a question asks about physical infrastructure (powering equipment, racking hardware, firmware updates on switches), that's Devices — even if the equipment's purpose is to create networks.

### Applications
Software code and applications on the devices, separate from the operating system/firmware. This class includes serverless functions, APIs, and microservices. If it's code that runs on a device but isn't part of the device's native OS/firmware, it's an Application.

### Data
The information residing on (data-at-rest), traveling through (data-in-motion), or processed by (data-in-use) the resources listed above. This class includes databases, S3 buckets, storage blobs, and files. When a question asks about PII, PHI, payment card data, records, or encryption of information — that's Data.

### Users
The people using the resources listed above and their associated identities. This covers employees, vendors, customers, administrators, and the digital identities (accounts, credentials, roles) that represent them in systems.

## Security Functions

### Govern (NIST CSF 2.0 addition)
The organizational context, oversight, and management wrapper around all other functions. Govern includes:
- Security policies and procedures (creation, review, communication)
- Compliance frameworks and standards adherence
- Organizational structure for security (roles, responsibilities, RACI)
- Budget and resource allocation for security
- Training program management (the program itself, not the training content)
- Audit and assessment programs
- Risk management frameworks
- Third-party governance
- Privacy governance and data handling policies
- Personnel security (hiring, onboarding, offboarding processes)
- Change management governance

Key distinction: If a question asks "do you have a POLICY for X" → that's Govern. If it asks "do you DO X" → that's one of the other five functions. Govern is the management layer.

### Identify
Inventory, enumeration, discovery — knowing what assets exist and understanding their state. This is a "left of boom" function focused on structural awareness.

Examples: asset inventory, vulnerability scanning (discovering weaknesses), software inventory, data classification, understanding network topology, account enumeration, MFA coverage assessment, phishing simulations (vulnerability scanning for users — CDM book p33-34, p62 Figure 20).

The CDM book specifically notes: the discovery and enumeration of vulnerabilities is best aligned under IDENTIFY. If the discovery of DATA inventory is IDENTIFY, then the discovery of DEVICES inventory must also be IDENTIFY — the framework enforces consistency.

### Protect
Applying controls to reduce risk BEFORE a security event — a "left of boom" function. During PROTECT, we address deficiencies found through IDENTIFY.

Examples: patching, hardening, encryption, access controls, network segmentation, firewall rules (blocking), application allowlisting, EDR auto-quarantine, backup protection measures, log enablement/configuration (capturing evidence — CDM book p17), penetration testing (validates protection controls — CDM book p40), phishing awareness training (remediation of user vulnerabilities found via simulation — CDM book p34).

The correction of deficiencies found during DETECT or RESPOND is still a PROTECT action, since the intent is to avoid future exploitation.

Note: MFA enforcement is IDENTIFY, not PROTECT — see Identify function above and CDM book p62 Figure 20.

### Detect
Monitoring for and noticing security events — the trigger point between left and right of boom. DETECT is about noticing that something bad is happening or has happened.

Examples: SIEM alerting, IDS alerts, anomaly detection, continuous monitoring, log analysis/monitoring (analyzing captured logs for events), SOC operations, UEBA behavioral alerts, ransomware encryption alerting, BAS/Breach and Attack Simulation (validates detection controls — CDM book p41).

Note: Log enablement/configuration = PROTECT (capturing evidence). Log analysis/monitoring = DETECT (finding events in captured data). This is a critical distinction per CDM book p17.

The CDM book clarifies: the EXPLOITATION of a vulnerability is best aligned under DETECT. You IDENTIFY the vulnerability (structural weakness); you DETECT its exploitation (event).

### Respond
Actions taken AFTER detection — dealing with an active or recently detected security incident. This is a "right of boom" function.

Examples: incident response plan execution, containment, forensics, eradication, breach notification, communication during incidents, legal/regulatory response, breach coaching, red team exercises (validates response controls — CDM book p41).

Key: RESPOND addresses incidents found through DETECT. If DETECT tells you "something bad happened," RESPOND is "here's what we do about it."

### Recover
Restoration to normal operations after an incident. This is a "right of boom" function.

Examples: disaster recovery plan execution, backup restoration, business continuity activation, system rebuilding, communication of recovery status, alternative systems activation, redundancy failover.

## Left of Boom vs Right of Boom

This is the foundational conceptual split borrowed from U.S. military terminology around IEDs.

| Left of Boom | Right of Boom |
|---|---|
| GOVERN, IDENTIFY, PROTECT | DETECT, RESPOND, RECOVER |
| Pre-event activities | Post-event activities |
| Risk management | Incident management |
| Security engineering | Security operations |
| Preventing intrusions | Expelling intrusions |
| Structural awareness | Situational awareness |
| Analyzing state, inventorying assets, discovering weaknesses | Analyzing events, investigating state changes, gathering evidence of exploitation |

"Boom" occurs when a weakness is successfully exploited. Left of boom aims to prevent that exploitation; right of boom aims to deal with its consequences.

## Key Disambiguations

### IDENTIFY vs DETECT
- IDENTIFY = discovering a structural weakness or knowing what exists (inventory). Left of boom.
- DETECT = noticing an event or exploitation. Right of boom trigger.
- Vulnerability scanning → IDENTIFY (you're discovering weaknesses before exploitation)
- IDS alert → DETECT (you're noticing an exploitation attempt)
- Asset inventory → IDENTIFY
- Anomaly detection → DETECT

### PROTECT vs RESPOND
- PROTECT = addressing deficiencies found through IDENTIFY. Left of boom.
- RESPOND = addressing incidents found through DETECT. Right of boom.
- Patching a known vulnerability → PROTECT (even if discovered during an incident)
- Containing an active breach → RESPOND
- Remediating a vulnerability (before exploitation) → PROTECT
- Remediating an incident (active exploitation) → RESPOND

### PROTECT vs DETECT for security tools
Many security tools span both functions. The key question: is the tool PREVENTING something or NOTICING something?
- Firewall blocking traffic → Networks-Protect
- Firewall logging suspicious attempts → Networks-Detect
- EDR auto-quarantining malware → Devices-Protect
- EDR alerting on suspicious behavior → Devices-Detect
- NGAV blocking known malware → Devices-Protect
- NGAV in notify-only mode → Devices-Detect

### Devices vs Networks
- A router (the physical/virtual box) → Devices
- The network path the router creates → Networks
- Firewall appliance (the box) → Devices
- Firewall rules (traffic filtering on the path) → Networks-Protect
- Switch configuration hardening → Devices-Protect
- Network segmentation (the logical separation) → Networks-Protect

### Applications vs Devices
- Operating system patching → Devices-Protect (OS is native to the device)
- Application patching → Applications-Protect (separate from OS)
- Firmware updates → Devices-Protect
- API security → Applications-Protect
- When both are mentioned together (e.g., "patching OS and third-party software") → Devices-Protect, Applications-Protect

## The Govern Function

Govern was added in NIST CSF 2.0 as the sixth function. It wraps around all other functions as the organizational/management layer. Govern applies to the policies, procedures, and oversight of security activities.

### Common Govern patterns:
- **all-assets Govern**: Security frameworks, compliance standards, formal enterprise-wide policies, comprehensive security assessments, enterprise risk registers
- **Users-Govern**: Personnel security (hiring, onboarding, offboarding), employee training programs, awareness program management, role-based responsibility definitions
- **Data-Govern**: Privacy policies, data classification policies, data handling/retention/disposal rules, consent management, regulatory compliance for data
- **Devices-Govern, Applications-Govern**: Change management, asset lifecycle governance, EOL policies
- **Users-Govern, Applications-Govern**: Third-party risk management governance (the program for governing vendor relationships)

## Dependency Curves

The CDM includes dependency curves at the bottom of the grid showing how TECHNOLOGY, PEOPLE, and PROCESS contribute differently across functions:
- Technology plays a greater role in IDENTIFY and PROTECT (left of boom)
- As we move to DETECT, RESPOND, and RECOVER (right of boom), dependency on Technology diminishes and dependency on People grows
- Process has a consistent level of dependency throughout all functions

This is relevant when classifying: controls that are heavily technology-dependent tend to be left-of-boom (IDENTIFY/PROTECT), while controls requiring significant human judgment tend to be right-of-boom (RESPOND/RECOVER).
