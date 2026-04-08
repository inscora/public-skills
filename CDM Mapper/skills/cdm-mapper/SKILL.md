---
name: cdm-mapper
description: >
  Map cybersecurity questions, controls, or capabilities onto Sounil Yu's Cyber Defense Matrix
  (5 asset classes x 6 security functions). Use this skill whenever someone asks to classify,
  categorize, or map a security question, control, product, or capability to the CDM framework.
  Also use when analyzing insurance questionnaires, security assessments, compliance checklists,
  or vendor capabilities against the CDM. Trigger on mentions of "Cyber Defense Matrix", "CDM mapping",
  "CDM classification", "asset class", "security function", or any request to place a cybersecurity
  topic into a grid of Devices/Networks/Applications/Data/Users vs Govern/Identify/Protect/Detect/Respond/Recover.
---

# CDM Mapper — Cyber Defense Matrix Classification Skill

This skill maps cybersecurity questions, controls, products, or capabilities onto Sounil Yu's
Cyber Defense Matrix. The CDM is a MECE (mutually exclusive, collectively exhaustive) framework
that combines 5 asset classes with 6 security functions into a 30-cell grid.

Before doing any mapping work, read `references/cdm-framework.md` for the precise definitions
of each asset class and function. If the input involves insurance or assessment questionnaires,
also read `references/mapping-corpus.md` for validated examples of how similar questions have
been mapped by human experts.

## The Grid

|              | Govern | Identify | Protect | Detect | Respond | Recover |
|--------------|--------|----------|---------|--------|---------|---------|
| **Devices**      |        |          |         |        |         |         |
| **Networks**     |        |          |         |        |         |         |
| **Applications** |        |          |         |        |         |         |
| **Data**         |        |          |         |        |         |         |
| **Users**        |        |          |         |        |         |         |

## How to Think About CDM Mapping

Mapping to the CDM requires answering two questions about each item:

1. **What asset class is being acted upon?** (the noun — what is being defended)
2. **What security function is being performed?** (the verb — what defensive action is taken)

### Step 1: Determine if the item is CDM-relevant

Not everything belongs on the CDM. The CDM is about **cyber defense controls** — things an
organization does to defend its digital assets. These items are NOT CDM-relevant:

- Administrative/underwriting information (company name, address, revenue, sector)
- Loss history and claims experience
- Insurance coverage terms and conditions
- Legal liability questions (E&O, IP/media)
- War/terrorism exclusions
- Pure financial metrics (revenue thresholds, deductible amounts)
- IT/Security budget questions (budget allocation is administrative, not a defense control)
- Detail/metadata about a control that's already mapped (e.g., "what vendor do you use for X"
  when X itself is already mapped) — BUT be careful: some "detail" questions ARE CDM-relevant.
  For example, "what % of data is classified" is Data-Identify even though it asks about a
  percentage, because the core element is data classification.

### Step 1b: The "Ultimate Beneficiary" Principle

This is the single most important mapping principle: **always ask what ULTIMATELY BENEFITS
from the control, not just what the surface action is.**

Examples:
- Updating IR playbooks looks like governance → but it ultimately benefits your ability to
  RESPOND → all-assets Respond
- Training on data handling looks like Users-Protect → but it ultimately benefits DATA
  protection → Users-Govern, Data-Protect
- Training on MFA/passwords → ultimately benefits MFA coverage → Users-Protect, Users-Identify
- Application isolation sounds like it protects applications → but it actually protects the
  DEVICE from rogue app behavior → Devices-Protect
- Background checks sound like governance → but they're about IDENTIFYING who the person is
  before making them a user → Users-Identify

### Step 2: Left of Boom vs Right of Boom

This is the most important conceptual split and should be your first branching question.

**Left of Boom** (before a security event occurs):
- **Govern**: Policies, frameworks, compliance, organizational structure, training oversight, budgets, roles, audit programs
- **Identify**: Inventory, enumeration, discovery — knowing what assets exist and their state. Vulnerability scanning fits here (discovering structural weaknesses)
- **Protect**: Applying controls to reduce risk — patching, hardening, encryption, access controls, segmentation, blocking. Remediation of vulnerabilities found through IDENTIFY is a PROTECT action

**Right of Boom** (during/after a security event):
- **Detect**: Monitoring for events, alerting on anomalies, continuous monitoring, noticing that something bad is happening. The exploitation of a vulnerability is DETECTED, not identified
- **Respond**: Actions taken after detection — incident response, containment, forensics, eradication, communication during an incident
- **Recover**: Restoration to normal operations — business continuity, disaster recovery, backup restoration, alternative systems

### Step 3: Pick the Asset Class

Ask: "What thing is being defended or acted upon?"

- **Devices**: Physical or virtual compute — workstations, servers, phones, tablets, IoT, containers, hosts, infrastructure, OS/firmware, switches, routers. Includes the operating system and native software. Network hardware (switches, routers) goes here because they are devices, even though they create networks
- **Networks**: Communication channels, connections, protocols, and paths — NOT the devices themselves. DNS, BGP, email filtering, web filtering, VPCs, VPNs, CDNs. Think "the roads, not the cars"
- **Applications**: Software code separate from the OS/firmware — serverless functions, APIs, microservices, web apps, SaaS. If it's code that runs on a device but isn't part of the device's OS, it's an application
- **Data**: Information at-rest, in-transit, or in-use — databases, S3 buckets, storage blobs, files, PII records, payment card data, encryption of data
- **Users**: People and their associated identities — employees, vendors, customers, and the identity/authentication systems that represent them. MFA, password policies, access reviews, and training all relate to Users

### Step 4: Handle Multi-Cell Mappings

A single question or control can map to multiple cells. Common patterns:

- **"all-assets" patterns**: When a control genuinely spans all asset classes (e.g., a security framework governs everything → Devices-Govern, Applications-Govern, Networks-Govern, Data-Govern, Users-Govern)
- **Dual asset**: Patching covers both OS and apps → Devices-Protect, Applications-Protect
- **Dual function**: EDR can both block (Protect) and alert (Detect) → Devices-Protect, Devices-Detect
- **Cross-domain**: Third-party risk management → Users-Govern, Applications-Govern (governing vendor relationships and the apps they provide)

Only use multi-cell mappings when genuinely warranted. The CDM's power comes from being MECE — resist the temptation to put things in multiple cells just because they seem broadly related. As Sounil Yu writes in the CDM book, it requires discipline to place each capability in one box.

### Key Distinctions That Trip People Up

**IDENTIFY vs DETECT**: IDENTIFY is about discovering structural weaknesses or knowing what exists (inventory, vulnerability scanning). DETECT is about noticing events — something happening in real-time or near-real-time. You IDENTIFY a vulnerability before it's exploited; you DETECT the exploitation.

**PROTECT vs RESPOND**: PROTECT addresses deficiencies found through IDENTIFY (left of boom). RESPOND addresses incidents found through DETECT (right of boom). Patching a vulnerability = PROTECT. Containing a breach = RESPOND. Even if you discover a vulnerability during an incident, the act of patching it is still PROTECT because you're preventing future exploitation.

**PROTECT vs DETECT for security tools**: Many tools do both. A firewall that blocks traffic = PROTECT. A firewall that logs and alerts = DETECT. EDR that auto-quarantines = PROTECT. EDR that alerts on suspicious behavior = DETECT. Ask: "Is this tool preventing something (PROTECT) or noticing something (DETECT)?"

**Govern vs the other functions**: Govern is about the organizational wrapper — policies, procedures, roles, compliance frameworks, audit programs. It's the "management" layer. If a question asks "do you have a policy for X" that's Govern. If it asks "do you do X" that's one of the other five functions. Note: a POLICY about logging is Govern (Devices-Govern, Networks-Govern), but the actual log enablement/configuration is Protect, and log analysis/monitoring is Detect.

**Logging dual nature**: The ACT of logging (enabling, configuring, capturing data) = PROTECT (per CDM book p17). The ANALYSIS of logs (monitoring, correlating, alerting via SIEM/SOC) = DETECT. A policy about which logs to maintain = GOVERN.

**Phishing simulations = Users-IDENTIFY (not Protect)**: Per CDM book (p33-34, p62, p79, p81), phishing simulations are vulnerability scanning for users. They discover who would click — that's identifying structural weaknesses. The training/retraining after failure = Users-PROTECT (patching the vulnerability). Metrics about simulations (coverage %, failure rate %) are IDENTIFY metrics.

**Security testing progression**: Penetration testing = PROTECT (validates protection controls, CDM book p40). BAS = DETECT (validates detection controls, p41). Red team = RESPOND (validates response controls, p41). This is distinct from vulnerability scanning = IDENTIFY.

**Identify-then-Protect pattern**: Many controls involve two steps. "Prevent unauthorized assets from joining the network" requires first Devices-Identify (identifying what's authorized) then Networks-Protect (blocking unauthorized ones). "Default password" questions involve Users-Identify (passwords identify users; defaults prevent identification) and Devices-Protect (eliminating defaults protects devices). When you see a prevention/enforcement control, ask if there's an identification prerequisite.

**Privacy/data questions — follow the data, not the medium**: A website privacy disclosure governs DATA management, not the website-as-application. DLP type selection is about Data-Protect and Data-Identify, not about the DLP tool itself. Always ask: "what asset is ultimately being defended?"

**Training maps to what it ultimately protects**: Training on data handling → Users-Govern + Data-Protect. Training on patching → Users-Govern + Devices-Protect, Applications-Protect. Training on MFA/passwords → Users-Protect + Users-Identify. Don't just default to Users-Govern, Users-Protect for all training.

### Step 5: Use Answer Types as Mapping Signals

When the expected answer format is known (e.g., from a questionnaire with predefined response types), the answer type is a strong signal for the correct CDM mapping. Here's how:

**Yes/No (binary)** — Indicates presence/absence of a control. "Do you have X?" The mapping depends entirely on what X is. These often map to Govern ("do you have a policy"), Protect ("do you enforce X"), or Identify ("do you have an inventory").

**Percentage (%)** — The percentage is neutral — it's just a measurement unit. Map the underlying control, not the format. A percentage measures the degree of implementation of whatever control it references: "What % of assets are inventoried?" → the control is inventory → Identify. "What % of data is classified?" → the control is classification → Data-Identify. "What % of users get phishing tests?" → the control is phishing simulation (vulnerability scanning for users) → Users-Identify. "What % of endpoints have EDR?" → the control is endpoint detection → Devices-Detect. Do not assume all percentages map to one function.

**Frequency (annually, quarterly, etc.)** — Often a Govern signal when asking about program cadence ("How often is training conducted?" = Users-Govern). But can be Recover when asking about testing cadence for DR ("How often is DR tested?" = all-assets Recover). The key is what's being scheduled.

**Multi-select / Checklist** — Typically Identify or Protect. "Select which controls you have" = the controls determine the mapping. "Select your MFA types" = Users-Identify. "Select which BCP components you have" = all-assets Recover.

**Free-text / Description** — Often requires reading the question carefully. "Describe your security measures for data" = Data-Protect. "Describe your IR plan" = all-assets Respond.

**Vendor/Product name** — Usually NOT CDM (it's metadata about who provides a control, not the control itself). Exception: when the vendor choice reveals what type of control exists.

**Numeric count** — Usually Data-Identify. "How many PII records?" = Data-Identify. "How many employees have access?" = Users-Identify.

**Date/Timeline** — Usually NOT CDM or context. "When did you start collecting biometric data?" is context, not a control. But "When was your last pen test?" could inform Identify cadence.

### Step 5b: Use Answer Choices as Mapping Signals

Beyond the answer *type*, the specific **answer choices** (e.g., checkbox options, dropdown values, radio buttons) provided with a question are often strong CDM mapping indicators — sometimes stronger than the question itself.

**How answer choices refine mapping:**

When a question provides predefined options, each option can reveal the asset class or function scope:

- **MFA question with choices like "Email", "VPN", "Cloud Admin Console", "All privileged access"** — The options confirm Users-Identify (types of identity verification) and may reveal scope (network access via VPN → also touches Networks-Protect).

- **"Select your endpoint protection capabilities" with choices like "Anti-malware", "EDR", "Application whitelisting", "Disk encryption"** — Each choice maps differently: Anti-malware/EDR → Devices-Protect and/or Devices-Detect; Application whitelisting → Devices-Protect (or Applications-Protect); Disk encryption → Data-Protect. The choices tell you the question spans multiple CDM cells.

- **"What types of data do you collect?" with choices like "PII", "PHI", "Payment card", "Biometric"** — All choices confirm Data-Identify (knowing what data exists and its classification).

- **"Select your backup methods" with choices like "Full image", "Incremental", "Cloud replication", "Offline/air-gapped"** — All choices confirm Recover (backup type is about restoration capability), with asset scope depending on what's being backed up.

- **"What logging do you perform?" with choices like "Firewall logs", "DNS logs", "Authentication logs", "Application logs"** — Each choice reveals a different asset class under Detect: Firewall/DNS → Networks-Detect; Authentication → Users-Detect; Application → Applications-Detect.

**Key principle:** When answer choices enumerate specific controls or capabilities, map each choice individually to determine if the question spans multiple CDM cells. When choices enumerate instances of the same control type (e.g., different data types for classification), they confirm a single mapping. When choices are not provided, rely on the question text and answer type alone.

## Output Format

For each item being mapped, provide:

```
CDM Mapping: [Asset]-[Function], [Asset]-[Function], ...
Rationale: Brief explanation of why this mapping was chosen
```

Use the format `Asset-Function` with these exact values:
- Assets: `Devices`, `Applications`, `Networks`, `Data`, `Users`
- Functions: `Govern`, `Identify`, `Protect`, `Detect`, `Respond`, `Recover`

For items spanning all assets, list all five explicitly:
`Devices-Govern, Applications-Govern, Networks-Govern, Data-Govern, Users-Govern`

For items that are not CDM-relevant, output:
```
CDM Mapping: NOT CDM
Rationale: [Why — e.g., "Administrative/underwriting question about company revenue"]
```

## Reference Files

- **`references/cdm-framework.md`** — Read this first. Contains the precise CDM definitions from Sounil Yu's book, including asset class boundaries, function definitions, the left/right of boom distinction, and the key disambiguation rules.
- **`references/mapping-corpus.md`** — Read this when mapping insurance questionnaire questions or security assessment items. Contains 300+ human-validated mappings organized by domain, which serve as precedent for consistent classification. This file also contains corrections and lessons learned from mapping errors.
