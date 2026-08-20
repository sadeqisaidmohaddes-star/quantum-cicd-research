# Gap Analysis

This document is written last, after all prior-art research (`prior_art.md`, `papers.md`, `repositories.md`, `ci_cd_landscape.md`, `bug_corpora.md`, `quantum_testing_landscape.md`, `claims.md`, `evidence.json`) was complete. It does not protect the original hypothesis — where evidence contradicts it, that is stated plainly below.

---

## 1. What already exists?

A genuine, active prior-art landscape exists across five layers:
- **Equivalence checking** of individual circuit pairs (MQT QCEC) — mature, citable, widely usable.
- **Single-run assertion-based debugging** (MQT Debugger, CUDA-Q assertions, Proq, Bloq/AutoBloq) — several independent implementations.
- **SDK-internal version-tier CI** (Qiskit's official `test_latest/development/minimum_versions.yml` template) — real, reusable, actively used across ~8 Qiskit-ecosystem repos.
- **Cross-Qiskit-version regression testing with CI-compatible output** (QUTest, arXiv:2605.19736, May 2026) — published and working, though not pytest-native and Qiskit-only.
- **Bug corpora and cross-version reproducibility studies** (Bugs4Q + its 21-Qiskit-version replication study, arXiv:2606.27124) — real, and already used for exactly this kind of cross-version regression analysis, as a research study.
- **Immature pytest plugins with cross-framework (not cross-version) equivalence assertions** (pytest-quantum, qtest-quantum) — real but young, unadopted (0–2 stars).
- **A single-SDK transpiler-regression pilot** (`quantum-transpiler-regression-testing` / "cart," June 2026) finding that ~38% of real transpiler bug-fixes are invisible to equivalence oracles.

## 2. What does MQT QCEC already solve?
The algorithmic core of pairwise circuit equivalence checking (decision-diagram, alternating DD, simulation-based falsification, ZX-calculus engines), primarily for verifying a compiled circuit against its source. It does not solve orchestration, CI/CD packaging, cross-version execution, or cross-SDK testing. It is a candidate *component* a broader system could call, not a competing end-to-end product.

## 3. What does MQT Debugger already solve?
Assertion-driven fault localization within one execution of one quantum program, via classical simulation, with IDE (DAP) integration. It does not solve cross-run, cross-version, or CI-level regression detection.

## 4. What do quantum testing frameworks already solve?
Framework-to-framework (Qiskit↔Cirq↔pytket) equivalence assertions inside pytest (`pytest-quantum`), and single-run circuit-property assertions (`qtest-quantum`). Both are pytest-native — that piece of the proposed idea already has (immature) precedent. Neither executes the same test against multiple *versions* of one SDK.

## 5. What does existing quantum CI/CD solve?
Qiskit's official CI template solves "run my existing tests against latest/dev/minimum Qiskit" as a reusable, drop-in GitHub Actions pattern — but it only reports pass/fail of tests the developer already wrote; it does not diff behavior between versions or detect equivalence-level regressions automatically. Qiskit's own QPY compatibility harness does genuine cross-version regression testing, but only for one narrow artifact (serialization format) and is not externally reusable.

## 6. Does an open-source pytest + GitHub Actions regression-testing infrastructure already exist?
**Partially, but not as a unified, adopted product.** No single system is simultaneously: pytest-native, cross-version, cross-SDK, and automated in its regression/equivalence detection. The closest single system (QUTest) covers cross-version + CI output but explicitly rejects pytest and is Qiskit-only. The closest pytest-native systems (pytest-quantum, qtest-quantum) cover the Python-ecosystem-idiomatic layer but not cross-version regression detection, and have essentially no adoption (0–2 stars, <9 months old).

## 7. Does cross-SDK or cross-version quantum regression testing already exist?
**Cross-version: yes, in at least two independent 2026 efforts** (QUTest for Qiskit-version regression with CI output; the Bugs4Q replication study measuring reproducibility collapse across 21 Qiskit versions; the "cart" pilot analyzing transpiler regressions). **Cross-SDK regression/equivalence testing: no working tool of any kind was found** — this is the most defensible piece of "not yet solved" in the entire investigation.

## 8. Is there an existing standardized fault/bug corpus?
No single universally-standard corpus (nothing analogous to Defects4J for Java), but real, citable, actively-used corpora exist (Bugs4Q is explicitly described elsewhere as "widely used"; a 32K-report mined dataset exists though not yet packaged). The original framing ("no corpus exists") is **false**. The narrowest true version: no corpus is packaged as a ready-to-use pytest/CI fixture.

## 9. Does the 31% statistic actually exist?
**Yes — confirmed, with exact provenance.** "Only eight of 26 respondents (31%) reported using quantum-specific testing tools," Zappin et al., arXiv:2506.17306, Finding 2, Section 5.2, p.18 (to appear ACM TOSEM). It should be cited precisely, with its N=26 caveat, as evidence of *unmet practitioner need* — not as proof that no relevant tooling exists (it doesn't measure tool existence, only adoption/awareness among a small sample).

## 10. Do the alleged papers actually support the research gap?
No specific pre-given arXiv IDs were available to check directly — the original "two papers" claim itself could not be confirmed as originally stated and should be treated as **unverified**. Independent search surfaced a paper (QUTest) that **partially contradicts** rather than supports the gap as originally framed, since it already implements a meaningful chunk of the proposed system. The 31% survey paper supports the *need* narrative but is not itself technical prior art for or against a specific tool.

## 11. What part of the proposed idea is genuinely novel, if any?
The narrowest defensible novel combination, not found anywhere in this research:
- **pytest-native** test discovery and fixtures (some precedent exists, e.g. pytest-quantum)
- **cross-SDK** (Qiskit vs Cirq vs PennyLane, not just cross-version-within-Qiskit) — **no precedent found anywhere**
- **automated regression/equivalence detection** (not hand-written assertions) as the comparison mechanism — QUTest and the pytest plugins all rely on manually-written assertions; nothing automatically diffs behavior and flags a regression the way, e.g., MQT QCEC's engines algorithmically prove/disprove equivalence
- **packaged as reusable, drop-in GitHub Actions tooling for arbitrary third-party quantum projects** (not internal-only CI for one SDK's own repository, and not a bespoke research pilot with 0 stars)

No system in this research combines all four. The strongest partial overlaps are QUTest (3 of 4, missing pytest+cross-SDK) and pytest-quantum (2 of 4, missing cross-version+automated-detection).

## 12. What parts are NOT novel and should be removed from the thesis/product claim?
- "No one does equivalence checking for quantum circuits" — false, MQT QCEC solves this well.
- "No one does quantum program debugging" — false, MQT Debugger and several assertion-based tools solve single-run debugging.
- "No bug corpus exists for quantum software" — false, Bugs4Q and others exist and are actively used, including for cross-version studies.
- "No one does cross-Qiskit-version regression testing" — false as of May/June 2026 (QUTest, cart pilot, Bugs4Q replication study).
- "No one has built quantum-aware CI/CD in GitHub Actions" — false, Qiskit's own ecosystem template is real and reusable, even if it doesn't do behavioral diffing.
- Any claim built on "two arXiv papers proving the gap" with unverified/unsupplied IDs — must be replaced with the papers actually verified here, correctly characterized (several of which cut against, not for, the novelty claim).

## 13. What is the narrowest defensible research gap?
**A pytest-native, cross-SDK (not merely cross-version) automated regression/equivalence-detection framework for quantum software, packaged as reusable GitHub Actions tooling for third-party projects — using existing components (e.g., MQT QCEC as an equivalence-checking engine, Bugs4Q-style corpora as a validation fixture) rather than reinventing them.** This is materially narrower than the original framing ("an open-source pytest/GitHub Actions style infrastructure that runs quantum projects across SDK versions and detects regressions/equivalence failures") — the original framing is largely already addressed piecewise (Qiskit's CI template handles version-matrix execution; QUTest handles cross-version behavioral drift with CI output; pytest-quantum handles pytest-native cross-framework equivalence). What is not addressed anywhere is the **cross-SDK, automated-detection, pytest-native, reusable-packaging** combination specifically.

The state-aware/autonomous-agent angle (C12) remains a genuinely open sub-question, but it is the least load-bearing part of the idea (no adjacent prior art at all, positive or negative) and should be treated as a possible *extension* of the core gap above, not the primary thesis.

## 14. What evidence would still be required before making a publication-quality novelty claim?
- **Direct confirmation or retraction of the originally-cited "two arXiv papers"** — the original IDs, if they exist, were never supplied to this research pass; find and check them explicitly rather than relying solely on the reconstructed candidates here.
- **A systematic, non-English-limited literature search** (this pass used English-language arXiv/GitHub/PyPI search only) — quantum software engineering has active Chinese- and German-language research communities (e.g., TUM/Munich groups) that may have unindexed or differently-titled prior art.
- **Direct outreach or citation-graph tracing from QUTest and the "cart" pilot** — both are very recent (within 3 months of this check) and may have follow-up versions, related work sections, or author statements that further narrow or widen the gap.
- ~~A DOI-resolver-verified check of the QCEC and Bugs4Q journal citations~~ — **done in verification pass 2 (2026-08-20)**: both citations were cross-confirmed via independent bibliographic listings (Semantic Scholar, researchr, ACM DL) after direct DOI resolution was blocked by ScienceDirect's JS wall. This also **corrected** the Bugs4Q bug count from an unverified "~50–67" to the DOI-confirmed 36 (2021 preprint) / 42 (JSS 2023 published version) — see `raw_notes.md`. Full-text abstract confirmation via the publisher page itself remains outstanding if stricter bibliographic rigor is later required.
- **An adoption/usage audit** (download counts, dependent repos, citation counts) for QUTest, cart, pytest-quantum, and qtest-quantum, to substantiate claims about their (im)maturity beyond GitHub star counts.
- **A working prototype comparison**: before claiming the narrowed gap is real and buildable, a small proof-of-concept should attempt to run the same test suite against two SDK versions of two different quantum SDKs (e.g., Qiskit and Cirq) and confirm no existing tool does this end-to-end — this research pass found strong textual/documentary evidence of absence, not an exhaustive empirical proof.

---

## Recommendation

The evidence does **not** support the original framing of the research gap as stated. Multiple substantial pieces of the proposed system already exist, some published within the last three months of this research date. The 31% statistic is real but was being used, in the original framing, to imply an evidentiary gap in *tooling* when it actually measures a gap in practitioner *adoption/awareness* — a different claim. The "two arXiv papers" as originally referenced could not be verified at all and should not be cited further without locating the actual intended IDs.

The idea is not dead, but it must be reframed narrowly around the cross-SDK + automated-detection + pytest-native + reusable-packaging combination identified in Section 13, explicitly positioned as building on (not competing with) MQT QCEC, Bugs4Q, and QUTest rather than claiming to be first to the general problem space.
