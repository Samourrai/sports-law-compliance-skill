# ⚖️ Sports Law Compliance Skill

A Claude skill for club managers, directors, and sports administrators. It navigates the regulatory frameworks of international and national sports governing bodies — protecting clubs from sanctions, fines, and reputational damage through clear, actionable, cited guidance.

---

## What It Does

Given any sports law situation, the skill:
1. Identifies the relevant governing body and regulation
2. Classifies the request type
3. Delivers a **quick verdict first** (ACT / CONTACT A LAWYER / NOTHING TO DO) in plain language
4. Offers a **full compliance report** on request, suitable for sharing with legal teams or boards

---

## Governing Bodies Covered

| Tier | Bodies |
|------|--------|
| Global arbitration | CAS / TAS |
| Global sport | FIFA, FIBA, World Rugby, World Athletics, ITF/ATP/WTA, ICC, FIVB, WADA, IOC |
| Continental football | UEFA, CAF, CONCACAF, CONMEBOL, AFC, OFC |
| National | Via registry — see `references/registry.md` |

Any governing body can be added at any time using the `ADD GOVERNING BODY` function.

---

## Request Types Handled

| Code | Type | Example |
|------|------|---------|
| COMP | Compliance check | "Can we sign this player?" |
| INTERP | Regulation interpretation | "What does Article 17 RSTP mean?" |
| SANC | Sanction / notice response | "We received a UEFA FSR notice" |
| CONTRACT | Contract / clause review | "Is this sell-on clause valid?" |
| MONITOR | Regulatory research | "What are the new CAF rules this season?" |
| INCIDENT | Live competition incident | "Our opponent fielded an ineligible player — can we protest?" |

---

## Special Functions

### ➕ Add a Governing Body
Say: `"add World Aquatics"` or `"register the FFF"`

The skill searches the body's official site, builds a structured entry in `references/registry.md`, and creates a dedicated reference file if the body has substantial regulations.

> ⚠️ **Persistence**: Changes are session-only in Claude.ai. To make permanent, copy the generated entry into this repository and commit.

### 📚 Add a Precedent
Say: `"add this CAS case"` or paste a case reference

The skill logs it into `references/precedents.md` with topic tags so it gets cited automatically in relevant future queries. Verifies references against cas-crt.org where possible.

> ⚠️ **Persistence**: Same as above — copy and commit to make permanent.

### 🔄 Refresh Regulations
Say: `"refresh UEFA regulations"` or `"update all"`

The skill searches official sources for the current year, compares against version dates in `references/registry.md`, and reports what has changed.

**Recommended schedule**: Run at the start of each season (July) and before each transfer window (January).

> ⚠️ **Persistence**: Same as above — updated content must be committed to Git to persist.

---

## File Structure

```
sports-law/
├── README.md                        ← This file
├── SKILL.md                         ← Main skill brain (load first)
└── references/
    ├── registry.md                  ← Master list of all governing bodies (always check first)
    ├── precedents.md                ← CAS awards and governing body decisions
    ├── football-bodies.md           ← FIFA, UEFA, CAF, confederations
    ├── cas-tas.md                   ← CAS/TAS arbitration procedures
    ├── olympic-wada.md              ← IOC, anti-doping, prohibited list
    ├── other-federations.md         ← FIBA, World Rugby, World Athletics, ITF, etc.
    └── contract-law.md              ← Transfers, agents, image rights, loans
```

---

## Installation

1. Download or clone this repository
2. Install the `.skill` file into your Claude environment
3. The skill will trigger automatically on sports law queries

---

## Contributing

### Adding a Governing Body
Use the standard template in `references/registry.md`. If the body has substantial regulations (more than a few key rules), also create a dedicated `references/[body-slug].md` file following the structure of existing reference files.

### Adding a Precedent
Use the standard template in `references/precedents.md`. Always verify the CAS award reference at [cas-crt.org](https://www.cas-crt.org) before committing. Mark unverified entries with `⚠️ UNVERIFIED`.

### Updating Regulations
When a governing body updates its regulations, update:
1. The relevant reference file (content)
2. The `Version date` field in `references/registry.md`

---

## Versioning

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial release — 6 request types, 5 reference files |
| 2.0 | April 2026 | Added registry, precedents library, ADD/REFRESH functions, two-tier response format |

---

## Disclaimer

This skill provides informational guidance only. It does not constitute formal legal advice. For official proceedings, sanctions, contract execution, or formal submissions to governing bodies, always engage a licensed sports law attorney.

---

*Built with Claude · Skill framework by Anthropic*
