# Hackers Manual Checklist — Golem Community Builder Programme

> Pragmatic version for a programme in its early stage. Lists only the **fundamentals** so the manual is solid in its initial phase, marking what's already covered and what's worth adding.

## Convention

- ✅ **Covered** — clearly documented in the manual
- 🟡 **Partial** — mentioned but lacking detail or pending definition
- ❌ **Missing** — not present, worth adding
- ⊘ **N/A** — does not apply to the programme format

References in parentheses point to the file where each item is covered.

---

## 1. Programme fundamentals

- [✅] Explicit mission and purpose (README.md → "Introduction", "Why this programme exists")
- [✅] Difference vs classic hackathon stated (README.md → "Introduction")
- [✅] Target audience defined across 3 profiles (README.md → "Who this is for")
- [✅] Minimum visual identity (logo, banner, badges in README.md)
- [✅] Golem Network context for newcomers (README.md → "About Golem Network")

---

## 2. Eligibility

- [✅] Accepted profiles (Web3 with/without Golem, Web2) in README.md
- [✅] No prior Golem experience required (README.md → "Who this is for")
- [✅] Teams allowed with no size cap (FAQ.md)
- [✅] Multiple participation clarified (FAQ.md)
- [🟡] Geographic restrictions not mentioned — add a line if any apply, or state "globally open"

---

## 3. Format and duration

- [✅] Continuous, open programme with no central deadline (README.md → "Introduction")
- [✅] Per-project duration: 2–4 weeks (README.md → "Development")
- [✅] 5-stage process visualized (README.md → "Participation process")
- [🟡] Pitch response time ("promptly" in FAQ, worth adding a rough SLA, e.g., <7 days)

---

## 4. Tracks

- [✅] Five tracks described with clear focus (builders_guide.md)
- [✅] Success criteria per track (builders_guide.md)
- [✅] Open track with prior validation (Track E)
- [✅] Reference example pre-programme (gScribe in README.md)
- [🟡] Examples of completed projects — to be populated as they exist

---

## 5. Tech stack and onboarding

- [✅] SDKs and minimum versions listed (builders_guide.md → "Current stack")
- [✅] Available networks: testnet hoodi and mainnet with differences (builders_guide.md)
- [✅] Faucet and test funds mentioned
- [✅] Official repos and docs linked (README.md → "Official resources")
- [🟡] Programme-owned "hello world" quickstart — currently delegated to official docs; could add a minimal template repo

---

## 6. Team formation

- [✅] Teams with no size cap (FAQ.md)
- [✅] Single official point of contact per team (FAQ.md)
- [✅] Internal bounty split left to the team (FAQ.md)
- [⊘] Formal cofounder matching — overkill at this stage, Discord is enough

---

## 7. Mentorship and support

- [✅] Golem team available during development (README.md, FAQ.md)
- [✅] Single channel: official Discord (README.md → "Contact")
- [🟡] Response time expectation undocumented — suggest a basic cadence or SLA
- [🟡] Rules on what the Golem team does/doesn't do (reviews code, doesn't write it) — useful to avoid friction

---

## 8. IP and licensing

- [✅] Builder retains code ownership (FAQ.md)
- [✅] Open-source license required (submission_guide.md)
- [✅] Golem can promote the project (FAQ.md, README.md → "Co-promotion")
- [✅] Builder may reuse the project (FAQ.md)

---

## 9. Evaluation criteria

- [✅] Success criteria declared per track (builders_guide.md)
- [🟡] No explicit numeric rubric — for a binary approval programme (yes/no/adjust) this may suffice; worth listing 3–5 cross-cutting criteria (technical quality, reproducibility, write-up clarity) the team uses on review
- [✅] Three possible review outcomes: approved, scope adjustment, rejected with justification (README.md)

---

## 10. Deliverables and submission

- [✅] Public GitHub repo required (submission_guide.md)
- [✅] README with minimum sections defined (submission_guide.md)
- [✅] Real execution metrics on Golem (submission_guide.md, README.md)
- [✅] Write-up for Discord (submission_guide.md)
- [✅] Wallet for payment at submission (submission_guide.md)
- [🟡] Pre-built README template — optional but lowers friction

---

## 11. Pitch

- [✅] Structured template available (pitch_template.md)
- [✅] Minimum fields defined (track, description, scope, plan, deliverables)
- [🟡] Official form: marked as "pending" in README.md — resolve before pushing for traction
- [⊘] Video pitch / demo day — programme doesn't use public pitch format, N/A

---

## 12. Prize and payment

- [✅] Clear amount: 500 USD in $GLM per project (README.md, badge)
- [✅] Payment form: $GLM to builder's wallet (README.md → "Delivery and payment")
- [🟡] Post-validation payment timeline — unspecified, worth a line (e.g., "within X days after delivery approval")
- [🟡] Exchange rate: USD↔GLM calculation timing not clarified

---

## 13. Communication and community

- [✅] Discord as single official channel (README.md, FAQ.md)
- [✅] Official resources (docs, repos, token) listed (README.md)
- [🟡] Partner communities: "TBC" — update once confirmed
- [🟡] Communication cadence during project — expected "proactive" but no suggested frequency

---

## 14. Exception handling

- [✅] Dropout policy explained (FAQ.md)
- [✅] Scope changes require re-approval (FAQ.md)
- [✅] Reasonable technical changes mid-development allowed (FAQ.md)

---

## 15. Conduct and plagiarism

- [❌] Code of conduct — short doc missing, a 1-page page linked from README is enough
- [❌] Policy on pre-existing code and forks — clarify whether starting from a fork is allowed or it must be new
- [❌] Policy on generative AI use for code — state whether allowed, requires disclosure, etc.

---

## 16. Post-delivery

- [✅] Co-promotion in official channels and partner communities (README.md, FAQ.md)
- [✅] Builder can reuse the project in their portfolio (FAQ.md)
- [🟡] Re-entry / same builder's second project — implicit policy, worth an explicit line

---

## Quick summary

| Status | Count | Reading |
|--------|-------|---------|
| ✅ Covered | ~40 | The operational core of the programme is solid |
| 🟡 Partial | ~14 | Details worth sharpening before scaling traction |
| ❌ Missing | 3 | Code of conduct + AI policy + pre-existing code policy |
| ⊘ N/A | 2 | Formal cofounder matching and video pitch |

**Minimum to add before pushing the programme harder:**

1. **Code of conduct** (1 page) linked from README and FAQ.
2. **Policy on generative AI** and **pre-existing code / forks** — 2 paragraphs in FAQ.
3. **Official pitch form** — unblock the "pending" in README.
4. **Approximate pitch response SLA** (e.g., <7 business days).
5. **Payment timeline after approval** (e.g., <X days in $GLM).

The rest (numeric rubric, programme quickstart, README template, structured mentorship) are incremental improvements that make sense when the programme grows, not now.

---

**Version:** 2.0 (simplified) · **Last updated:** 2026-05-11
