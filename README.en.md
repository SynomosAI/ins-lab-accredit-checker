# ins-lab-accredit-checker

[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](LICENSE)
[![Content: ARR](https://img.shields.io/badge/Content%20License-ARR%20%7C%20citable-blue.svg)](LICENSE-CONTENT)

> **Status: RESERVED (placeholder · open for claim)** — this repository already ships the four-file industry-access skeleton per the platform protocol, and waits for an operator with domain credentials to claim it and fill in real rules.

This is the SynomosAI **domain profile** for inspection/testing bodies — CMA qualification (检验检测机构资质认定) and CNAS laboratory accreditation, with their scope of competence. It decomposes "may this body issue this report" into verifiable attributes, so that AI only provides prerequisite guidance — never a test conclusion.

## What this domain governs

CMA qualification and scope-of-competence verification for inspection/testing bodies.

CMA (资质认定) and CNAS (实验室认可) are two independent systems, each with a defined competence scope. Issuing reports beyond scope, or back-dating / co-signing, are the main industry risks. AI can lay out the qualifications vs. covered scope; the test conclusion is issued and owned by the laboratory itself.

## Domain identity

| Field | Value |
|---|---|
| Domain ID | `ins` (globally unique, never reused) |
| Domain name | Inspection & testing · CMA/CNAS qualification and scope |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved at | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `ins.cma_status` | enum | Validity of the CMA qualification certificate per regulator records · valid/expired/none/suspended/not_required |
| `ins.cnas_status` | enum | CNAS accreditation status (independent of CMA) · accredited/expired/none/suspended/not_applicable |
| `ins.scope_coverage` | enum | Are the requested parameters/methods within the approved scope (current standard version) · covered/partially/not_covered/unclear |
| `ins.report_validity` | enum | Current report validity (withdrawn/corrected) · valid/pending/void/unknown |
| `ins.signatory_authority` | enum | Authorized signatory qualification and authorized domains · authorized/restricted/none/unknown |

## Red lines (machine-readable, non-negotiable)

1. Never output "test passed / meets the standard" — test conclusions are issued and owned by the body.
2. Never state that a project outside the accredited scope may be reported.
3. Never suggest out-of-scope reporting, co-signing, back-signing, or retro-fitting raw records.

Each red line has a matching blocking rule in `gate-map.json`; the platform validator fails if coverage is missing.

## Quick Start / 快速开始

This repo is a declarative skeleton — no runtime, no install.

```bash
git clone https://github.com/SynomosAI/ins-lab-accredit-checker.git
cd ins-lab-accredit-checker
python -m json.tool domain.manifest.json    # validate the manifest
cat checker.io.json                         # read the MCP tool contract
```

The checker MCP tool returns only four states — `shown / missing / expired / unverifiable` — and is forbidden from outputting "pass/fail / meets-standard" conclusions (see `_forbidden_outputs` in `checker.io.json`).

## Repository layout

```text
domain.manifest.json   # declaration: attributes / issuer requirements / red lines / validity
gate-map.json          # friction levels per action class (gate/1.0)
privacy.json           # privacy notice (privacy/1.0) — an admission condition
checker.io.json        # MCP checker I/O contract (show & verify, never judge)
LICENSE                # code & config: MIT
LICENSE-CONTENT        # prose content: All Rights Reserved (citable with attribution)
```

## References

- Metrology Law of the PRC (计量法)
- Measures for the Administration of Qualification of Inspection and Testing Bodies (检验检测机构资质认定管理办法)
- Regulations on Certification and Accreditation of the PRC (认证认可条例)
- CNAS-CL01 Criteria for the Competence of Testing and Calibration Laboratories (检测和校准实验室能力认可准则)
- Measures for the Supervision and Administration of Inspection and Testing Bodies (检验检测机构监督管理办法)

The above references only explain the origin of the domain's attributes; they are not legal advice.

## Claiming this domain

The domain is open to qualified institutions. To claim:

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red lines per current rules.
3. Run the platform validator self-test (all five criteria must pass).
4. Open a PR with credential proof and rule citations.

## License

Code and configuration are MIT-licensed. Prose content is copyrighted by SynomosAI.

© 2026 SynomosAI. All rights reserved.

Full terms: [LICENSE](LICENSE) (MIT) · [LICENSE-CONTENT](LICENSE-CONTENT) (ARR). Report security issues privately via [SECURITY.md](SECURITY.md).
