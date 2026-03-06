# 🖋 InkScrypt
### The Citizen's Credit Engine

> *"The law is a calculator, not a guessing game."*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Status: Live](https://img.shields.io/badge/Status-Live-green)](https://righttoremaininformed.com/inkscrypt)
[![Built With: Zero AI](https://img.shields.io/badge/Built%20With-Zero%20AI-orange)](https://github.com/Tetrahedroned/inkscrypt)
[![Zero Server](https://img.shields.io/badge/Server-None-success)](https://righttoremaininformed.com/inkscrypt)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-righttoremaininformed.com-blue)](https://righttoremaininformed.com/inkscrypt)

---

## What This Is

InkScrypt is a **deterministic, logic-based credit law engine** that encodes federal consumer protection law — FCRA and FDCPA — as executable JavaScript running entirely in the browser.

It does not summarize. It does not guess. It does not use AI. It **calculates.**

You describe your situation in plain English. InkScrypt maps it to the exact federal statute that protects you, evaluates whether a violation has occurred, calculates the legal deadline using a clock that accounts for weekends and all 11 federal holidays, and generates a professionally formatted PDF letter — complete with a SHA-256 self-verifying document fingerprint.

**Nothing is sent to a server. Nothing is stored. Nothing is tracked.** The entire engine lives in a single HTML file and runs on your device.

No subscriptions. No AI hallucinations. No gatekeeping. Free. Always.

---

## Why This Exists

My name is Chris. I'm a father from Louisiana.

I built this entire site on a Galaxy S21 Ultra in my spare time. Every module, every line of code, InkScrypt, Decoded, all of it.

I built this because I watched people pay $99/month to "credit gurus" for services they already had the legal right to perform themselves — for free — under federal law. I watched someone I love pay a debt collector out of fear. Not because they owed it. Because the system is designed to feel bigger than you.

The Credit Repair Organizations Act says it plainly:

> *"Anything a credit repair company can legally do, you can do yourself."*

InkScrypt is the tool that makes that sentence real.

When this site goes down — because some months the budget runs out — the code stays here. The community keeps it. It cannot be bought out. It cannot be shut down. That's the whole point of open source.

This is named as a salute to **Ink** — the one who keeps me going.

---

## How the Engine Works

InkScrypt is a **single self-contained HTML file**. No backend. No database. No API calls. The entire engine — statute library, clock, violation evaluator, document builder, fingerprint generator, and PDF renderer — is embedded JavaScript that executes locally in your browser.

This is not a limitation. This is a deliberate architectural decision. A tool built to help people assert their legal rights should never transmit their personal information to a third-party server.

### The Execution Path

```
User Input (plain English + form fields)
         ↓
[Scenario Mapper]
  → User selects from 11 situation types
  → Each scenario maps to exact federal statute(s)
  → Determines document type required
         ↓
[Clock Engine]
  → Takes user-provided date of incident/notice
  → Calculates 30-day statutory deadline
  → Skips all weekends
  → Skips all 11 U.S. federal holidays (hardcoded, updated annually)
  → Returns deadline date + days remaining
         ↓
[Violation Evaluator]
  → Was a response received?
  → Did the deadline pass?
  → Cross-references scenario against statute requirements
  → Returns one of three states:
      PENDING   — within the statutory window
      VIOLATION — deadline passed, no adequate response
      COMPLIANT — properly resolved
         ↓
[Document Builder]
  → Constructs formal letter from evaluated result
  → Injects: consumer name/address, respondent name/address,
    exact statute citations, violation description, demand language,
    CFPB/FTC regulatory warning, deadline notice
  → Applies document-type-specific legal language
         ↓
[Fingerprint Engine]
  → Concatenates full document content into a single string
  → Hashes using Web Crypto API (SHA-256, native browser)
  → Derives a unique document ID: INKSCRYPT-YYYY-MM-DD-XXXXXXXX-XXXXXXXX
  → Embeds fingerprint + timestamp into document footer
  → No server required to verify — the document witnesses itself
         ↓
[PDF Renderer]
  → jsPDF (client-side, no upload)
  → Renders formatted letter with:
      — Header with document ID
      — Violation status badge
      — Statute citation block
      — Demand paragraph
      — Regulatory warning
      — Wet Ink signature line
      — SHA-256 fingerprint footer
  → Downloads directly to device
```

### The Deterministic Guarantee

The same inputs will always produce the same output. There is no model, no probability, no inference. The logic is a series of conditional evaluations against encoded statute text. If the statute says 30 days, the clock counts 30 days. If the statute says the collector must cease contact after a written request, the letter says exactly that — citing the exact subsection.

This is what separates InkScrypt from AI-generated letters. An AI might produce something that *sounds* correct. InkScrypt produces something that *is* correct, because the output is a direct function of the statute, not a prediction.

### The Zero-Server Architecture

```
Traditional credit repair app:
User → Form → Server → Database → Response → PDF

InkScrypt:
User → Browser → PDF
```

Personal information never leaves the device. There is no account to create. There is no data to breach. There is no company with a database of people asserting their federal rights.

---

## Federal Statutes Encoded

11 statutes. Every one verified against the current U.S. Code.

| Key | Citation | Description |
|-----|----------|-------------|
| `FCRA_605` | 15 U.S.C. § 1681c | 7-year reporting limits — the expiration clock |
| `FCRA_609` | 15 U.S.C. § 1681g | Right to full file disclosure |
| `FCRA_611` | 15 U.S.C. § 1681i | 30-day reinvestigation deadline |
| `FCRA_612` | 15 U.S.C. § 1681j | Free annual credit report |
| `FCRA_623` | 15 U.S.C. § 1681s-2 | Furnisher obligations — direct disputes |
| `FDCPA_805` | 15 U.S.C. § 1692c | Prohibited contact (workplace, hours, attorney) |
| `FDCPA_807` | 15 U.S.C. § 1692e | False or misleading representations |
| `FDCPA_808` | 15 U.S.C. § 1692f | Unfair collection practices |
| `FDCPA_809` | 15 U.S.C. § 1692g | Debt validation rights — 30-day window |
| `FDCPA_813` | 15 U.S.C. § 1692k | Civil liability — statutory damages up to $1,000 |
| `CROA` | 15 U.S.C. § 1679 | Credit Repair Organizations Act — advance fee prohibition |

---

## Document Types Generated

10 document types. Each is built from statute-specific logic, not a template.

| Document | Statute | Trigger |
|----------|---------|---------|
| **FCRA Bureau Dispute** | § 1681i | Inaccurate or unverifiable tradeline |
| **Method of Verification Demand** | § 1681i(a)(6)(B)(iii) | Bureau returned "verified" without explanation |
| **Furnisher Direct Dispute** | § 1681s-2 | Dispute sent directly to the company reporting the error |
| **FCRA Violation Notice** | § 1681i | Reinvestigation deadline passed without adequate response |
| **Reporting Period Expiration** | § 1681c | Negative item reportable window has expired |
| **Debt Validation Demand** | § 1692g | First contact from collector — validation requested |
| **Cease and Desist** | § 1692c | Collector violating contact restrictions |
| **FDCPA Violation Notice** | § 1692e / § 1692f | False threats, deceptive representations, unfair practices |
| **CROA Violation Notice** | § 1679b | Credit repair company charged advance fees |
| **Combined FCRA/FDCPA Notice** | Multiple | Collector both reporting and contacting improperly |

Every document includes:
- Exact federal statute citations with subsection specificity
- Highlighted demand block
- CFPB/FTC regulatory warning to the recipient
- Legal deadline notice
- SHA-256 self-verifying document fingerprint
- Wet Ink signature line

---

## The Wet Ink Signature

Every InkScrypt document ends with a signature line unlike anything a credit repair guru has ever produced.

The signature line itself is a protection clause — rendered in micro-print using the same technique banks apply to personal checks. The consumer signs directly on their rights.

```
FORMAL NOTICE UNDER FEDERAL LAW • RECEIPT TRIGGERS STATUTORY OBLIGATIONS •
RETAINED AS EVIDENCE • ALTERATION VOIDS THIS NOTICE •
```

This is not decorative. It establishes formal notice, declares the document as evidence, and signals to the recipient that this was prepared with precision. No template sold online has this. This is InkScrypt's mark.

---

## The Document Fingerprint

Every generated document carries a SHA-256 self-verifying fingerprint.

```
INKSCRYPT-2026-03-04-F3AD4E50-394CC1BB
SHA-256  |  2026-03-04 14:32:07 UTC
```

**How it works:**

1. The full document content — every word, every citation, every name — is concatenated into a single string
2. That string is hashed using the browser's native Web Crypto API (SHA-256)
3. The resulting hash is formatted into the document ID shown above
4. The ID is embedded in the document footer before the final PDF render

**Why this matters:**

If even one character of the document is altered after generation, the hash breaks. The document cannot be silently modified. In a legal context — where the authenticity of a notice letter may be challenged — this is not a small thing.

No server required to verify. The document witnesses itself. A public verification endpoint exists at `righttoremaininformed.com/inkscrypt#verify`.

---

## Companion: Decoded — What I Wish I'd Known

InkScrypt generates the instrument. **Decoded** is the guide that explains why every word in that instrument matters.

Decoded (`righttoremaininformed.com/decoded`) is a 6,500-word field manual built from the same research that built InkScrypt. It covers:

- How e-OSCAR automation actually processes your dispute — and why most disputes fail before a human ever reads them
- The collector training script, decoded section by section — what they're saying, why they're saying it, what your counter is
- What "verified" actually means when a bureau uses that word
- Metro 2 — the standard, the myth, and how to actually use it
- The enforcement graveyard: $2.7B Lexington Law settlement, Growth Cave, The Credit Game, FES — the pattern behind every case
- Word-for-word scam phrases flagged by the FTC
- Bureau executive escalation contacts — verified by the mortgage broker community
- State-level protections: Colorado, New York, California, and the 2026 federal medical debt rule
- The real FTC statistics on what disputes actually accomplish

The full sourced research document is included in this repository as `CREDIT_REPORT_FIELD_MANUAL.md` — 153 primary citations.

---

## Project Structure

```
inkscrypt/
├── inkscrypt.html              # The entire engine — fully self-contained
├── CREDIT_REPORT_FIELD_MANUAL.md  # The Decoded research document — 153 sources
└── README.md                   # You are here
```

That's it. One HTML file. No dependencies to install. No server to configure. Open it in a browser and it works.

---

## Roadmap

### Completed
- [x] Statute Library — 11 federal statutes encoded
- [x] Clock Engine — federal holiday aware, weekend-skipping deadline calculator
- [x] Violation Evaluator — deterministic PENDING / VIOLATION / COMPLIANT logic
- [x] 10 document types — statute-specific letter generation
- [x] Wet Ink signature — micro-print protection clause
- [x] SHA-256 document fingerprint — self-verifying, no server required
- [x] Zero-server architecture — everything runs in browser, nothing transmitted
- [x] Public verification endpoint — confirm document authenticity
- [x] Decoded companion — 6,500-word field manual, 153 sources
- [x] Full mobile responsiveness


---

## Contributing

InkScrypt is open source because the law belongs to everyone.

**If you are a consumer attorney or paralegal and you find a statute error — open an issue immediately.** Accuracy is everything here. A wrong citation in a legal notice could harm someone. That is the one thing this project cannot afford.

**If you are a developer** — pull requests are welcome. The statute logic inside `inkscrypt.html` is the most important place to contribute. Clear, verifiable, well-commented additions only.

**If you are someone who used InkScrypt and it helped you** — share it. That is the entire distribution model.

### Before contributing:

- Every statute citation must be verified against the current U.S. Code at `uscode.house.gov`
- No AI-generated legal content — human-verified only
- Document any statute changes with a source link in the PR description
- Test the full generation flow before submitting

---

## Legal Disclaimer

InkScrypt is a free educational tool based on publicly available federal statutes.

It is **not legal advice.** The creator is not an attorney.

Nothing in InkScrypt instructs users to dispute accurate information, file false reports, or engage in any conduct that violates federal or state law.

For legal advice specific to your situation, consult a licensed FCRA or FDCPA attorney in your jurisdiction. Many take these cases on contingency — no cost to you unless they win.

---

## The Hosting Guarantee

The live version at `righttoremaininformed.com` is hosted out of my own pocket.

If the site is down — the budget for the month ran out.

If the site is offline — this repository is the backup. Clone it. Open `inkscrypt.html` in any browser. It works. No setup. No server. No account.

The power stays with you. That is the whole point of open source.

---

## License

MIT License — free to use, modify, and distribute.

The statutes encoded in this software are federal law and are in the public domain.  
The software implementation is © 2026 Chris — righttoremaininformed.com.

---

*Named as a salute to Ink — the one who keeps me going.*

---

**[righttoremaininformed.com](https://righttoremaininformed.com)** &nbsp;·&nbsp; [Live Demo](https://righttoremaininformed.com/inkscrypt) &nbsp;·&nbsp; [Decoded — What I Wish I'd Known](https://righttoremaininformed.com/decoded) &nbsp;·&nbsp; [Report an Issue](https://github.com/Tetrahedroned/inkscrypt/issues)
