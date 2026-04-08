# CDM Mapping Corpus — Validated Pattern Examples from Insurance Questionnaires

This reference contains human-validated CDM mapping patterns derived from cyber insurance carrier questionnaires.
These serve as precedent examples for consistent classification of new questions.

**Status**: v3 — Sanitized: question identifiers removed, patterns generalized for public use.

## Table of Contents
1. [How to Use This File](#how-to-use-this-file)
2. [Governance Domain](#governance-domain)
3. [Identity and Access Management](#identity-and-access-management)
4. [Network Security](#network-security)
5. [Endpoint and Device Security](#endpoint-and-device-security)
6. [Data Protection and Privacy](#data-protection-and-privacy)
7. [Email and Anti-Phishing](#email-and-anti-phishing)
8. [Asset Management and Vulnerability](#asset-management-and-vulnerability)
9. [Backup and Recovery](#backup-and-recovery)
10. [Third Party Risk](#third-party-risk)
11. [Operational Technology](#operational-technology)
12. [Common Patterns Summary](#common-patterns-summary)
13. [Corrections and Lessons Learned](#corrections-and-lessons-learned)

## How to Use This File

When mapping a new question, find the most similar validated pattern in the relevant domain section.
The CDM mapping should follow the same pattern unless the question's specific wording changes
the asset class or function being targeted.

Each entry shows: `Question pattern → CDM Mapping (rationale)`

## Governance Domain

### Enterprise-Wide Governance (all-assets Govern pattern)
These questions ask about organization-wide security programs, frameworks, or policies.

- Framework/standards adherence (ISO, NIST, SOC2) → all-assets Govern (compliance framework governance)
- Risk-based security assessments → all-assets Govern (risk assessment is governance)
- Formal security policies (existence, scope) → all-assets Govern (policies govern all assets)
- Incident response plan existence → all-assets Respond (IR plan = response readiness)
- IR plan testing/tabletop exercises → all-assets Respond (testing response capability)
- InfoSec as business priority, management support, budget allocation for security → all-assets Govern
- Information security policy (definition, review, communication) → all-assets Govern
- Risk management framework and assessments → all-assets Govern
- Enterprise risk register (existence, maintenance, review) → all-assets Govern
- Security audit program existence → all-assets Govern
- "Who performs security audits" → NOT CDM (detail, not a control)
- Security audit frequency → all-assets Govern
- Privacy audit for compliance with privacy policy → Data-Protect (about the privacy policy which protects data)
- "Who performs privacy audits" → Data-Protect (supplements the privacy audit question)
- Privacy audit frequency → Data-Protect (supplements the privacy audit question)
- "Are audit recommendations always followed" → Data-Govern (governance of privacy-related follow-through)
- Procedure/playbook update frequency → all-assets Respond (the ultimate goal of updating playbooks is your ability to Respond — CDM focuses on what ultimately benefits)

### Personnel Security (Users-Govern)
- Employee onboarding security procedures → Users-Govern
- Background checks before hiring → Users-Identify (you need to identify who your users are before making them users — background checks are about identifying the person)
- Onboarding/offboarding procedures → Users-Govern

### Security Awareness Training (Users-Govern, Users-Protect)
Training questions span both Govern (the program management) and Protect (the protective effect on users).

- Security awareness training program existence → Users-Protect, Users-Govern
- General security awareness training for all employees → Users-Protect, Users-Govern (training protects users + frequency is governance)
- Training for contractors → Users-Identify, Users-Protect (must identify contractors first, then protect them)
- Training frequency → Users-Govern (frequency of enforcement is governance)
- Role-specific security education → Users-Govern, Users-Protect
- Proactive security culture → Users-Govern, Users-Protect
- Training on strong passwords and MFA → Users-Protect, Users-Identify (training protects, but ultimate beneficiary is MFA → Users-Identify)
- Training on data handling best practices → Users-Govern, Data-Protect (program existence = govern, but benefits data protection)
- Training on unintentional data exposure → Users-Govern, Data-Protect
- Training on recognizing/reporting security weaknesses → Users-Govern (broad scope, keep simple)
- Training on keeping patches up to date → Users-Govern, Devices-Protect, Applications-Protect (benefits patching)
- Training on transmitting sensitive data over public networks → Users-Govern, Data-Protect
- Training on exposure/social engineering → Users-Govern, Users-Protect
- Social engineering awareness training → Users-Govern, Users-Protect

### IT/Security Budget
- IT/Security budget allocation → NOT CDM (budget is underwriting/administrative, not a cyber defense control)

### Centralized Governance
- Centralized security across subsidiaries → all-assets Govern
- Dedicated security team/CISO → all-assets Govern

### Privacy and Data Governance
- Privacy policy legal compliance → Data-Govern
- Privacy/data collection governance (consent, retention, purpose limitation) → Data-Govern
- Privacy disclosure on website → Data-Govern (NOT Applications-Govern — even though a website is technically an app, the privacy disclosure governs data management, not the application itself)
- Data classification policy (existence, levels, scope, enforcement) → Data-Govern
- Privacy governance framework → Data-Govern, Users-Govern

### Change Management
- Change management/CAB process → Devices-Govern, Applications-Govern

### Critical Infrastructure Hosting
- "Are critical systems and applications hosted centrally" → Applications-Protect, Devices-Protect (this is about protecting systems/devices, NOT governance or user-related)

## Identity and Access Management

### MFA (Users-Identify)
The human mapper consistently maps MFA presence/coverage questions to Users-Identify.
The reasoning: MFA questions in insurance questionnaires ask about the SCOPE and EXISTENCE of MFA
(do you have it? where is it deployed?) — that's identifying the state of identity controls.

- MFA for email access → Users-Identify
- MFA for remote network access → Users-Identify
- MFA for admin/privileged access → Users-Identify
- MFA for cloud services → Users-Identify
- MFA type detail (what kind of MFA) → Users-Identify

ALL MFA questions — whether about presence, coverage, or enforcement — map to Users-Identify.
MFA is fundamentally an identification mechanism: the second factor (something you have,
something you are) verifies the person is who they claim to be. Even enforcing MFA is about
making identification mandatory, not building a protective barrier. If MFA fails, you've lost
confidence in WHO is authenticating, not lost a wall. Biometrics make this especially clear:
a fingerprint or face scan is literally about identifying the person.

### Password and Credential Management
- LAPS/credential rotation for local admin → Devices-Protect
- Privileged account password rotation → Users-Identify
- Service account password rotation → Devices-Protect

### Access Control
- IAM program existence → Users-Govern
- Role-based access definitions → Users-Govern
- Access termination on employee exit → Users-Govern, Devices-Protect
- Formal access provisioning process → Users-Govern, Users-Identify (formal process = govern, but requires ability to identify different types of users)
- Inactive account disablement → Users-Identify (must identify active vs inactive accounts; a stale account means you can't identify who's behind it)
- Physical/logical access restrictions → Devices-Protect, Networks-Protect
- Geofencing → Users-Identify, Networks-Protect (identify where users are and whether they should be there; the network is what's being protected from unauthorized locations)
- Session timeout/auto-locking → Devices-Protect (this protects the DEVICE, not the user — it's about enterprise asset protection)
- Domain admin access restrictions → Users-Protect

### Account Inventory
- Service account inventory → Users-Identify
- Active Directory usage → Users-Identify

### Default Credentials
- "Do you use default/standard passwords" → Users-Identify, Devices-Protect (you identify users with passwords; default ones prevent identification; ultimately protects devices)
- Processes to disable default accounts on hardware/software → Devices-Protect, Applications-Protect (disabling default accounts protects devices and applications)

## Network Security

### Firewall and Segmentation
- Firewall protection → Networks-Protect
- Cloud firewall → Networks-Protect
- Network segmentation (firewall rules) → Networks-Protect
- Managed firewall service → Networks-Protect
- Segmentation controls, port management → Networks-Protect
- Remote access segmentation from core → Networks-Protect

### Remote Access
- Remote access controls → Networks-Protect
- MFA for remote/VPN/cloud access → Users-Identify

### Cloud Security
- Formal cloud security policy → Networks-Govern

### Monitoring and Detection
- SOC (24/7 monitoring) → all-assets Detect
- SIEM centralized logging → all-assets Detect
- Continuous monitoring → all-assets Detect
- Admin behavior monitoring → Users-Detect
- Log centralization → all-assets Detect
- UEBA coverage → Devices-Detect, Users-Detect
- Ransomware encryption alerting → Data-Detect
- USB activity monitoring → Devices-Detect
- Policy defining which audit logs are maintained → Devices-Govern, Networks-Govern (this is a POLICY, so it's Govern, and it governs device/network logging)

### Network Access Control
- NAC → Networks-Protect
- Unauthorized asset prevention on network → Devices-Identify, Networks-Protect (you identify the assets first, then protect the network from unauthorized ones)

### DLP and Data-in-Transit
- DLP deployment → Data-Protect
- Removable media controls → Data-Protect
- Removable media autorun controls → Devices-Protect

### Vulnerability Testing
- Penetration testing → Devices-Protect, Applications-Protect, Networks-Protect (per CDM book p40: pen testing VALIDATES protection controls, it doesn't discover structural weaknesses like vuln scanning does. Pen test = PROTECT; BAS = DETECT; Red team = RESPOND)

### Web/Email Filtering
- Email filtering → Networks-Protect (filtering is a network-path protection)
- Web filtering → Networks-Protect

### Redundancy
- Network redundancy → Networks-Recover

## Endpoint and Device Security

### NGAV/Antimalware
- NGAV deployment → Devices-Protect
- Application allowlisting → Devices-Protect
- NGAV blocking configuration → Devices-Protect

### EDR
EDR is a nuanced mapping that depends on what the question emphasizes:
- EDR deployment (detection + response capability) → Devices-Detect, Devices-Respond
- EDR blocking configuration → Devices-Detect, Devices-Protect
- EDR blocking malware → Devices-Protect

### Application Isolation
- Application isolation → Devices-Protect
- Application isolation technology type → Devices-Protect (application isolation protects the DEVICE from rogue application behavior, not the application itself)

### Hardening
- Hardened baselines/CIS benchmarks → Devices-Protect
- Secure configuration management for software assets → Applications-Protect, Devices-Protect (software assets = applications, but ultimately protects the device too)

### Physical Security
- Physical server security → Devices-Protect

### Security Measures (Broad)
- "Describe security measures for data confidentiality/integrity" → Data-Protect (the question is about protecting data, not devices/networks)

### DLP Detail
- "Select type of sensitive information DLP is used for" → Data-Protect, Data-Identify (CDM-relevant — identifies what data types and protects them)

### Log Retention
- "How long is log data maintained" → Data-Identify (log data retention is about knowing what data you have)

## Data Protection and Privacy

### Data Inventory
- PII/PHI/PCI record counts → Data-Identify
- Data in custody → Data-Identify
- Payment card data on network → Data-Identify
- Card-present transactions → Data-Identify
- Banking/ACH data records → Data-Identify
- Records on children → Data-Identify, Users-Identify
- Sensitive information inventory → Data-Identify

### Encryption
- Encryption controls (at rest, in transit, key management) → Data-Protect

### Data Processing and Sharing
- Outsourced PCI processing → Data-Identify
- Third party data processing → Data-Govern, Data-Identify
- Third party processing inventory → Data-Govern, Data-Identify
- Payment processor identification → Data-Identify

### Consent and Privacy
- Data sharing consent → Users-Govern
- Parental consent for minor data → Data-Govern, Users-Govern
- PII sharing consent → Data-Govern

### POS Security
- POS device security → Devices-Protect
- POS antimalware → Devices-Protect

### Breach Detection
- PII breach logging → Data-Detect

### Access Termination
- PII access termination on exit → Users-Protect

## Email and Anti-Phishing

### Email Security Controls
- Email filtering, DMARC, SPF → Networks-Protect

### Training and Simulation
- Social engineering awareness → Users-Govern, Users-Protect
- Financial transaction staff training (keeping knowledge current) → Users-Protect (asks about keeping users' knowledge current, not about having a program; like keeping AV definitions updated)
- Phishing simulation and remediation → Users-Identify, Users-Protect (simulation = vulnerability scanning for users per CDM book p33-34/p62/p79 = IDENTIFY; remediation/retraining of those who fail = PROTECT, like patching a discovered vulnerability)
- Phishing awareness → Users-Protect (training/awareness = patching user vulnerabilities)
- Phishing test coverage (% of population) and failure rate (%) → Users-Identify (these are metrics about the phishing SIMULATION program, which is vulnerability scanning for users; coverage % = what proportion of users are being scanned; failure rate % = what proportion have identified vulnerabilities. Per CDM book p33-34: phishing simulations are explicitly "vulnerability scanning for users" under IDENTIFY)

### Suspicious Email Reporting
- Suspicious email reporting process → Users-Govern, Users-Protect, Devices-Protect (documented process = Govern; enables users to self-protect by not clicking; ultimately protects the device from compromise)

### Wire Transfer Controls
- Wire transfer verification → Users-Govern, Users-Protect, Data-Govern
- Financial transaction access scope (who can initiate/approve) → Users-Identify

## Asset Management and Vulnerability

### Asset Inventory
- Hardware/software asset inventory → Devices-Identify, Applications-Identify
- Asset inventory coverage → Devices-Identify, Applications-Identify
- Data asset inventory → Data-Identify

### Vulnerability Management
- Vulnerability scanning (general) → Devices-Identify, Applications-Identify
- Internal vulnerability scanning → Devices-Identify, Applications-Identify
- External vulnerability scanning coverage → Devices-Identify, Applications-Identify
- Unpatched vulnerability inventory → Devices-Identify, Applications-Identify

### Patching
- Patching (OS + apps) → Devices-Protect, Applications-Protect
- Patching scope → Devices-Protect, Applications-Protect

### EOL Management
- EOL identification → Devices-Identify, Applications-Identify
- EOL decommission → Devices-Govern, Devices-Protect

### Software Management
- Software version currency → Applications-Identify
- Authorized software enforcement → Applications-Protect
- Unauthorized software detection → Applications-Detect
- Third-party vulnerability remediation (e.g., Log4j-style supply chain) → Applications-Identify, Applications-Protect, Devices-Protect (identify which third-party apps bundle the vuln; protect the apps and the devices underneath from RCE)

### Asset Governance
- Asset ownership, classification, lifecycle → Devices-Govern, Applications-Govern

## Backup and Recovery

### BCP/DR Plans
- Business continuity plan → all-assets Recover
- DR plan → all-assets Recover
- DR test frequency → all-assets Recover
- BCP/DRP components → all-assets Recover
- DR communication plan → all-assets Recover

### Backup Protection
- Backup security (offline, immutable, separated) → Data-Protect
- "How many backup copies AND prevention from same-event impact" → Data-Recover, Data-Protect (two statements in one: "how many copies" = right of boom, recovery capability; "prevent copies from being affected by same event" = left of boom, protecting backup integrity)

### Backup Restoration
- Backup restoration testing → Data-Recover
- Cloud/off-site backup → Data-Recover

### DR Configuration
- DR system configuration → Devices-Recover, Applications-Recover, Networks-Recover, Data-Recover (DR systems encompass servers, software, connectivity, and data — can't configure DR for just one in isolation)

### Power and Bandwidth
- Alternate/backup power → Devices-Recover
- Alternative bandwidth → Networks-Recover

## Third Party Risk

### Vendor Governance
- Vendor assessment program → all-assets Govern (third-party risk spans all asset classes: their users, apps, devices, networks, and your data)
- Vendor security assessments → all-assets Govern
- Third party risk management program (including onboarding, ongoing monitoring, offboarding, review cadence) → all-assets Govern (managing third-party InfoSec risk encompasses their users/access, applications, devices, network connections, and data handling)

### Vendor Inventory
- Critical vendor inventory → all-assets Identify (vendors touch all asset classes)
- Critical system dependencies → Applications-Identify, Devices-Identify
- Critical application identification → Applications-Identify

### Vendor Access
- MFA for vendor access → Users-Identify (MFA verifies the vendor is who they claim to be)

### Vendor Contingency
- Vendor contingency plans → all-assets Recover
- Alternative critical systems → Applications-Recover

### Software QC
- Software testing procedures → Applications-Protect

### M&A Security
- M&A integration and segmentation → Networks-Protect, Devices-Protect

## Operational Technology

### OT Identification
- OT system inventory → Devices-Identify
- OT usage identification → Devices-Identify

### OT Protection
- OT controls are mapped similarly to their IT equivalents, with the asset class typically being Devices

### OT Recovery
- OT backup → Data-Recover
- OT backup protection → Data-Recover
- Manual workaround capability → Devices-Recover

## Common Patterns Summary

| Pattern | CDM Mapping | Example |
|---|---|---|
| Security framework/standard | all-assets Govern | ISO 27001, NIST CSF, SOC2 adherence |
| Formal enterprise policy | all-assets Govern | Information security policy |
| Risk assessment program | all-assets Govern | Annual risk assessments |
| IR plan and testing | all-assets Respond | Tabletop exercises, IR plan |
| Log enablement/configuration | all-assets Protect | Enabling logging captures evidence (CDM book p17) |
| Log analysis/monitoring (SOC/SIEM) | all-assets Detect | 24/7 SOC, centralized log analysis |
| BCP/DR plans | all-assets Recover | Business continuity, DR |
| MFA coverage/presence | Users-Identify | Do you require MFA for X? |
| Password/credential mgmt | Users-Identify or Devices-Protect | Rotation maintains identity trustworthiness; local admin rotation protects devices |
| Training/awareness program | Users-Govern, Users-Protect | Security awareness, training content |
| Phishing simulations | Users-Identify | Vuln scanning for users (CDM book p33-34) |
| Phishing sim metrics (% coverage, failure rate) | Users-Identify | Measuring vuln scan coverage/findings |
| Penetration testing | Devices-Protect, Apps-Protect, Networks-Protect | Validates protection controls (CDM book p40) |
| BAS (Breach & Attack Simulation) | all-assets Detect | Validates detection controls (CDM book p41) |
| Red team exercises | all-assets Respond | Validates response controls (CDM book p41) |
| Data record inventory | Data-Identify | PII/PHI/PCI record counts |
| Encryption | Data-Protect | At-rest, in-transit encryption |
| Patching | Devices-Protect, Applications-Protect | OS and app patching |
| Network segmentation | Networks-Protect | VLAN, firewall rules |
| EDR (detection emphasis) | Devices-Detect, Devices-Respond | EDR alerting, investigation |
| EDR (blocking emphasis) | Devices-Protect | EDR auto-quarantine |
| Backup security | Data-Protect | Offline, immutable backups |
| Backup restoration | Data-Recover | Restoration testing |
| Third party governance | all-assets Govern | Vendor risk mgmt spans all asset classes |
| Privacy policy/compliance | Data-Govern | GDPR, CCPA compliance |
| Personnel controls (background checks) | Users-Identify | Background checks = identifying who the person is |
| Personnel controls (onboarding/offboarding) | Users-Govern | Processes for managing user lifecycle |
| Wire transfer controls | Users-Govern, Users-Protect, Data-Govern | Verification procedures |
| Vulnerability scanning | Devices-Identify, Applications-Identify | External/internal scans |
| Physical security | Devices-Protect | Server room access controls |

## Corrections and Lessons Learned

These corrections come from human expert review. Each one documents a mapping error and the
reasoning behind the correction. These are critical for understanding CDM mapping principles.

### Lesson 1: CDM focuses on what ULTIMATELY BENEFITS from the control
When mapping, don't stop at the surface action — ask "what ultimately benefits?" For example,
updating IR playbooks looks like governance (Govern), but the ultimate beneficiary is your
ability to Respond. So it maps to Respond, not Govern.

### Lesson 2: Budget/financial questions are NOT CDM
IT/Security budget allocation is an administrative/underwriting concern, not a cyber defense
control. Unless the CDM book specifically addresses budget as a function, avoid mapping it.

### Lesson 3: Privacy/website disclosures govern DATA, not Applications
A website privacy disclosure governs data management policies. Even though a website is
technically an application, the CDM mapping should reflect what's being governed (data), not
the medium (the application).

### Lesson 4: Data classification details ARE CDM (Data-Identify), even if they ask about %/frequency
Questions about "what % of data is classified" or "how often is classification updated" are
about Data-Identify, not just metadata. The core element is data classification = identification.

### Lesson 5: Training questions have nuanced mappings based on what the training benefits
Not all training is just "Users-Govern, Users-Protect." The mapping depends on what the
training ultimately protects:
- Training on passwords/MFA → Users-Protect, Users-Identify (benefits MFA coverage)
- Training on data handling → Users-Govern, Data-Protect (benefits data protection)
- Training on patches → Users-Govern, Devices-Protect, Applications-Protect
- Training on sensitive data transmission → Users-Govern, Data-Protect
- Training on reporting incidents → Users-Govern (broad, keep simple)
- Training frequency → Users-Govern (governance of the program)

**Critical distinction: Govern vs Protect for training**
- "Do you have a training program?" / "How often is training conducted?" = **Govern** (program existence/cadence)
- "Are staff with access to X trained?" / "Is their knowledge up to date?" = **Protect** (the user's current state of readiness)
- "Do employees who fail training get retrained?" = **Protect** (remediation keeps the user patched, like updating AV definitions)
Think of it like devices: "Do you have a patch management program?" = Govern. "Are your devices patched?" = Protect. Same logic applies to Users and training.

### Lesson 6: Contractor training requires Users-Identify first
"Does training apply to contractors?" maps to Users-Identify, Users-Protect — you need to
identify contractors before you can protect them.

### Lesson 7: Background checks = Users-Identify, not Users-Govern
Background checks before hiring are about identifying who the person is before making them
a user. This is Users-Identify, not Users-Govern.

### Lesson 8: "Who performs X" detail questions may not be CDM
"Who performs the audits?" is a detail/metadata question — not a control itself. However,
if the audit relates to a specific CDM domain (like privacy audits → Data-Protect), the
surrounding detail questions inherit that domain mapping.

### Lesson 9: Privacy audits → Data-Protect, not all-assets Govern
Privacy audits ensure compliance with a privacy POLICY. The policy protects DATA. So privacy
audit questions map to Data-Protect (the audit) and Data-Govern (the follow-through).

### Lesson 10: "Hosted centrally" is about protecting systems, not governance
"Are critical systems hosted centrally?" is about Applications-Protect, Devices-Protect —
protecting systems through centralized hosting. NOT Users-Govern or any Identify function.

### Lesson 11: Security measures for data → Data-Protect
When a question says "describe security measures to protect confidentiality and integrity of
data," that's Data-Protect. Don't over-expand to Devices-Protect and Networks-Protect just
because security measures could theoretically involve those.

### Lesson 12: Unauthorized asset prevention = Identify THEN Protect
"Controls to prevent unauthorized assets joining the network" requires TWO steps: first
Devices-Identify (identify the assets), then Networks-Protect (protect the network). Not
just Devices-Protect, Networks-Protect.

### Lesson 13: Application isolation protects DEVICES, not applications
Application isolation technology protects the device from rogue application behavior. The
asset being defended is the Device, not the Application. → Devices-Protect.

### Lesson 14: DLP type detail IS CDM-relevant
"Select the type of sensitive information for which DLP is used" is CDM-relevant: Data-Protect,
Data-Identify. It identifies what data types exist and protects them.

### Lesson 15: Secure config for software assets = Applications-Protect + Devices-Protect
Software assets ARE applications. Secure configuration of software → Applications-Protect,
but it ultimately also protects the device on which the app sits → Devices-Protect.

### Lesson 16: Audit log POLICY = Govern (not Detect)
A policy defining which audit logs are maintained is Govern (it's a policy). The actual logging
and monitoring is Detect, but the policy about it is Devices-Govern, Networks-Govern.

### Lesson 17: Log retention duration = Data-Identify
How long you maintain log data is about knowing what data you have → Data-Identify.

### Lesson 18: Default passwords → Users-Identify + Devices-Protect
"Do you use default passwords?" has two facets: passwords identify users (Users-Identify —
default passwords mean you CAN'T identify who's who), and eliminating defaults protects
devices (Devices-Protect).

### Lesson 19: Disabling default accounts protects Devices AND Applications
Disabling default accounts on hardware AND software → Devices-Protect, Applications-Protect
(the question explicitly calls out both hardware and software).

### Lesson 20: Access provisioning process = Users-Govern + Users-Identify
A formal approval process for granting access privileges requires both governance (the process)
and identification (distinguishing different types of users for appropriate access levels).

### Lesson 21: Session timeout protects DEVICES, not users
Session timeout/locking on enterprise assets is about Devices-Protect. The asset being
defended is the device, not the user.

### Lesson 22: Password rotation is Users-Identify, not Users-Protect
Password rotation maintains the trustworthiness of the identification mechanism. If a password
goes stale and is compromised, you can no longer reliably identify WHO is behind the account —
that's an identification failure, not a protection failure. The credential IS the identity assertion;
rotating it keeps that assertion meaningful. Compare with default passwords (Lesson 18): both
stale and default passwords erode your ability to correctly attribute identity.
**Exception**: Local admin password rotation (LAPS) is Devices-Protect because the ultimate
beneficiary is the device (preventing lateral movement), not the identity.
**General principle**: When a credential's primary purpose is to establish WHO someone is,
controls that maintain credential integrity are Identify. When the credential's purpose is to
guard access to a specific asset (device, application), the control protects that asset.

### Lesson 23: Inactive account disablement is Users-Identify, not Users-Protect
Disabling inactive accounts after N days is an identification activity on two levels: (1) you must
identify which accounts are active vs inactive — that's inventory/enumeration; (2) if a stale
account stays enabled and gets compromised, the failure is that you can no longer identify who
is behind that credential — the legitimate user isn't even there anymore. This is the same
pattern as Lesson 22 (password rotation): stale credentials erode identity trustworthiness.
**Contrast with default account disablement**: Disabling default accounts on
hardware/software is Devices-Protect and Applications-Protect because the ultimate beneficiary
is the device or application being hardened, not the identity.
**General principle**: Account lifecycle management (active/inactive status) is fundamentally
an identity inventory problem. "Who is still here?" is an Identify question.

### Lesson 24: Geofencing is Users-Identify + Networks-Protect, not Users-Protect
Geofencing doesn't protect users — it protects the NETWORK from access originating in
unauthorized locations. The Users component is Identify, not Protect: you need to identify
where users are geolocated and whether they should be there. This is another instance of the
Identify-then-Protect pattern (see Lesson 12): identify the entity first (Users-Identify), then
protect the asset that benefits (Networks-Protect).
**General principle**: When a control restricts access based on user attributes (location, role,
status), the user-side of the mapping is usually Identify (determining who/where/what the
user is), while the Protect maps to whatever asset is being shielded from unauthorized access.

### Lesson 25: Follow the exploit chain to the ultimate impact
A question about ensuring third-party providers addressed a specific vulnerability (e.g., Log4j)
touches multiple CDM cells. Trace the full chain: (1) You need to identify which third-party
applications contain the vulnerability → Applications-Identify; (2) The vulnerability lives in
application code, so hardening the supply chain → Applications-Protect; (3) Follow the exploit
to its ultimate impact — e.g., Log4Shell enables RCE on the machine → Devices-Protect;
(4) The question asks about a "process or procedure" for third parties, which could also signal
Applications-Govern.
**General principle**: When a question references a specific vulnerability or exploit, trace the
kill chain to its ultimate impact to determine the full CDM mapping. Don't stop at the asset
where the vulnerability lives — ask what gets compromised if exploited. Also: third-party
software visibility (knowing what libraries/components are bundled) is fundamentally an
Identify problem.

### Lesson 26: User reporting processes are Protect, not Detect
A process for users to report suspicious emails is NOT Users-Detect. Users are not sensors —
they're making a judgment call to NOT engage with something sketchy, which is a self-protective
action. The mapping is: Users-Govern (documented process exists) + Users-Protect (enables
users to self-protect by choosing not to click) + Devices-Protect (the ultimate beneficiary — the
machine doesn't get compromised via malicious link/attachment).
**General principle**: When a user takes an action to avoid a threat (reporting, not clicking,
escalating), that's Protect behavior, not Detect. Detect implies a technical sensing capability
that identifies an event has occurred. Users choosing to disengage from a threat are protecting
themselves and the assets underneath them.

### Lesson 27: Compound questions can straddle the boom line
Some questions contain multiple statements that span Left and Right of Boom. Example: "How
many backup copies do you take (Right of Boom — recovery capability) AND what measures
prevent multiple copies from being affected by the same event (Left of Boom — protecting
backup integrity)?" Map each statement independently: the recovery aspect → Recover; the
prevention aspect → Protect. Both map to the same asset (Data) but different functions.
**General principle**: When a question contains "and" or multiple clauses, decompose it. Each
clause may map to a different CDM function, potentially on different sides of the boom line.
Look for prevention/hardening language (Protect) vs restoration/continuity language (Recover)
within the same question.

### Lesson 28: Physical infrastructure questions map to Devices, not Networks
Alternate power for equipment, racking, firmware updates on switches/routers — these are all
Devices questions, even when the equipment's purpose is to create networks. Networks are an
abstraction of device configuration: a switch is a Device that runs software creating network
paths, but the device exists physically regardless of whether a network exists logically.
Also: when a question implies you need to identify something (e.g., "critical equipment") as a
prerequisite to answering, but the question itself is about something else (e.g., powering it),
map the question's primary concern, not the implied prerequisite. Not every question that
touches identification needs an Identify mapping.

### Lesson 29: Third-party risk management is all-assets Govern
When a question asks about managing third-party information security risks — whether during
onboarding, ongoing monitoring, review cadence, or offboarding — it spans ALL asset classes
under Govern. Third parties touch everything: their users access your systems, their applications
integrate with yours, their devices may connect to your network, their network connections
create attack surface, and they handle your data. Scoping third-party governance to just
Users + Applications misses Devices, Networks, and Data.
For reference, consult NIST SP 800-161 (Cybersecurity Supply Chain Risk Management) or
equivalent information security policies on third-party risk.
**General principle**: When a question is about a broad organizational risk management process
(third-party risk, information security risk, enterprise risk), default to all-assets for the
relevant function unless the question explicitly narrows the scope to specific asset classes.

### Lesson 30: ALL MFA is Users-Identify — no exceptions for enforcement
MFA — whether asked about presence, coverage, type, or enforcement — is always Users-Identify.
MFA is fundamentally an identification mechanism: the second factor verifies the person is who
they claim to be. Even "enforcing" MFA is making identification mandatory, not building a
protective barrier. If MFA fails or isn't in place, you've lost confidence in WHO is
authenticating — that's an identification failure, not a protection failure. Biometrics
(fingerprint, face scan) make this especially clear: they literally identify the person.
This supersedes any prior distinction between "do you have MFA" (Identify) and "do you enforce
MFA" (Protect). Both are Identify.
**General principle**: Any authentication mechanism — passwords, MFA, biometrics, certificates
— is fundamentally about establishing identity. Controls that strengthen, maintain, or enforce
authentication are Identify, not Protect.

### Lesson 31: Phishing simulations are vulnerability scanning for users = IDENTIFY
Per CDM book (p33-34, p62 Figure 20, p79 Figure 35, p81): phishing simulations are explicitly
the equivalent of vulnerability scanning but for the Users asset class. They discover structural
weaknesses (users who would click) — that's IDENTIFY, not PROTECT. The training/retraining
that follows a failed simulation is the remediation = PROTECT (patching the user vulnerability).
**Metrics about phishing simulations** — coverage % (what proportion of users are scanned) and
failure rate % (what proportion of scanned users have vulnerabilities) — are IDENTIFY metrics
because they measure the output of a vulnerability scanning program.
- Phishing simulation frequency/cadence → Users-Identify
- Phishing test coverage (% of population) → Users-Identify
- Phishing test failure rate (%) → Users-Identify
- Phishing awareness training → Users-Protect (remediation)
- Retraining employees who fail → Users-Protect (remediation)
**General principle**: When a control is analogous to vulnerability scanning for any asset class,
it maps to IDENTIFY. Metrics about that scanning program (coverage, frequency, findings rate)
are also IDENTIFY. The remediation of findings = PROTECT.

### Lesson 32: Pen testing = PROTECT, BAS = DETECT, Red team = RESPOND
Per CDM book (p40-41), these three testing methodologies validate different security functions:
- **Penetration testing** validates PROTECTION controls — it tests whether your defenses hold.
  Maps to Devices-Protect, Applications-Protect, Networks-Protect (depending on scope).
- **Breach and Attack Simulation (BAS)** validates DETECTION controls — it tests whether your
  monitoring catches simulated attacks. Maps to all-assets Detect.
- **Red team exercises** validate RESPONSE controls — they test whether your team can detect,
  respond to, and contain a realistic adversary. Maps to all-assets Respond.
This is NOT the same as vulnerability scanning (which = IDENTIFY). Vulnerability scanning
discovers structural weaknesses; pen testing tests whether those weaknesses can be exploited
despite your protection controls.
**General principle**: Security testing methodologies map to the function they validate, not the
function they resemble. Pen test validates Protect; BAS validates Detect; Red team validates Respond.

### Lesson 33: Logging has a dual nature — enablement = PROTECT, analysis = DETECT
Per CDM book (p17): the ACT of logging (capturing, enabling, configuring log collection) is
a PROTECT activity — you're ensuring evidence will exist if something happens. The ANALYSIS
of those logs (monitoring, correlating, alerting, investigating) is a DETECT activity.
- "Do you enable logging on X?" → [Asset]-Protect
- "Do you have a SIEM?" / "What % of logs are fed into SIEM?" → all-assets Detect
- "Do you perform log reviews?" → all-assets Detect
- "Policy defining which logs to maintain" → [Asset]-Govern
- "How long do you retain logs?" → Data-Identify (knowing what data you have)
**General principle**: Capturing/recording data is a protective action (ensuring evidence exists).
Analyzing/monitoring that captured data for events is a detection action.

### Lesson 34: NIST CSF 2.0 places authentication under PR.AA (Protect) — but CDM book disagrees
NIST CSF 2.0 has category PR.AA (Identity Management, Authentication, and Access Control)
under the PROTECT function. This conflicts with CDM book Figure 20 which places MFA under
Users-IDENTIFY. Our skill follows the CDM book's placement: authentication mechanisms are
fundamentally about establishing identity (IDENTIFY), not about protection. When questioned,
cite CDM book p62 Figure 20 and the conceptual argument: if MFA fails, you've lost the ability
to IDENTIFY who is authenticating — that's an identification failure.
NIST SP 800-53's IA family (Identification and Authentication) straddles both concepts in its
name, supporting the view that these activities are identification-centric.
