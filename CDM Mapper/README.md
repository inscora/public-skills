# CDM Mapper

A Claude skill for mapping cyber insurance questionnaire questions to the [Cyber Defense Matrix](https://cyberdefensematrix.com/) (CDM) — a 5×6 grid of asset classes (Devices, Applications, Networks, Data, Users) and security functions (Govern, Identify, Protect, Detect, Respond, Recover).

See the CDM in action: [cdm.inscora.com](https://cdm.inscora.com)

## Structure

```
CDM Mapper/
├── skills/cdm-mapper/          # The Claude skill
│   ├── SKILL.md                # Core methodology and mapping rules
│   └── references/
│       ├── cdm-framework.md    # CDM framework definitions from the book
│       └── mapping-corpus.md   # Human-validated mapping examples + lessons learned
└── README.md
```

## How the skill works

The CDM Mapper skill teaches Claude how to classify any cyber insurance question into the correct CDM cell(s). It uses a decision tree methodology:

1. **Identify the asset class** — What is the question fundamentally about?
2. **Identify the security function** — What phase of the security lifecycle does it address?
3. **Handle multi-cell mappings** — Questions that span multiple assets or functions get multiple mappings.

The skill references the CDM Book by Sounil Yu as the primary authority, supplemented by NIST CSF 2.0 and NIST SP 800-53.

## Key decisions encoded in the skill

These are non-obvious mappings that were resolved by cross-referencing the CDM Book:

- **MFA** → Users-Identify (not Protect), per CDM Book Figure 20
- **Phishing simulations** → Users-Identify (vulnerability scanning for users), per CDM Book p33-34
- **Phishing training/retraining** → Users-Protect (remediation)
- **Pen testing** → Protect, **BAS** → Detect, **Red team** → Respond (CDM Book p40-41)
- **Log enablement/configuration** → Protect; **Log analysis/monitoring** → Detect

## Usage

Install this skill in Claude Code or Cowork, then ask Claude to map any cybersecurity question, control, or capability to the CDM. For example:

- "Map this insurance question to the CDM: Do you require MFA for all remote access?"
- "Classify these controls against the Cyber Defense Matrix"
- "Where does endpoint detection and response fit on the CDM?"

## Contributing

To improve mappings:

1. Read `SKILL.md` to understand the methodology
2. Review `mapping-corpus.md` for existing validated examples and lessons learned
3. When adding new mappings or correcting existing ones, always cite CDM Book page references

## License

Apache 2.0 — see [LICENSE](../LICENSE).
