# Papers — Verified Primary Sources

All entries below were verified by opening the actual arXiv abstract page and/or full text (PDF/HTML), not by trusting search snippets.

---

## The 31% practitioner statistic — source paper (Claim C04)

**Title:** "Challenges and Practices in Quantum Software Testing and Debugging: Insights from Practitioners"
**Authors:** Jake Zappin, Trevor Stalnaker, Oscar Chaparro, Denys Poshyvanyk (William & Mary)
**arXiv ID:** 2506.17306 (v1: 2025-06-18; v2: 2026-01-16)
**Venue:** To appear in ACM Transactions on Software Engineering and Methodology (TOSEM), 2025/2026
**URL:** https://arxiv.org/abs/2506.17306

**Exact statistic (verbatim, extracted from the full PDF text, not a snippet):**
> "Only eight of 26 respondents (31%) reported using quantum-specific testing tools."

Stated as **Finding 2**, Section 5.2, p. 18; restated in the abstract, introduction, Section 8.2, and Section 8.4.

**Methodology:** Survey of quantum software developers, invited from 1,397 industry/government contacts + 75 academic contacts. 38 completed responses; 12 excluded for lacking hands-on quantum development experience, leaving **N = 26** analyzed respondents. Plus 4 follow-up semi-structured interviews. Fielded via Qualtrics, 2024-05-20 to 2024-08-05. IRB-approved.

**Detail behind the number:** Question T10 ("Tools used for testing," multiple choice). 16/26 respondents reported using **no** testing tools at all. Of the remaining 10, 8 (= 31% of the full N=26) used quantum-specific frameworks/libraries; e.g., Qiskit Test Utilities was used by only 4/26 respondents.

**Caveat (from the authors themselves, Section 9.2):** N=26 is small; the authors explicitly flag limited generalizability, though they argue triangulation with prior literature supports the pattern.

**Verdict:** Claim C04 is **CONFIRMED**. The 31% figure is real, correctly transcribed, and traceable to an exact page/section/finding of a real, citable, soon-to-be-published TOSEM paper. It should be cited precisely as "one 2024 survey of 26 quantum software developers found 31% (8/26) reported using quantum-specific testing tools" — not generalized as a field-wide constant.

**Relevance to the CI/CD gap:** The paper is a practitioner survey, not a tool paper. Section 8.3.4 explicitly **calls for** (but does not build) "CI/CD pipelines tailored to hybrid systems," listing it as a promising future direction. This paper **supports** (identifies an unmet practitioner need for) the proposed research gap rather than contradicting it — but it is evidence of *need*, not evidence of *novelty* (i.e., it doesn't prove no such tool exists elsewhere).

---

## Reconstructed candidates for "the two alleged arXiv papers" (Claims C05/C06)

No specific arXiv IDs were supplied for the "two papers" referenced in the original project framing, so these could not be confirmed/denied against a given ID — they were reconstructed via broad independent search. Any prior claim of specific IDs should be treated as **UNVERIFIED** unless those IDs surface elsewhere. The following are the real, independently-verified candidates most relevant to the claimed gap, ranked by materiality:

### 1. QUTest — the most material find of the entire research phase

**Title:** "QUTest: A Native Testing Framework for Quantum Programs"
**Author:** José Campos (University of Porto / Lisboa)
**arXiv ID:** 2605.19736, submitted 2026-05-19
**URL:** https://arxiv.org/abs/2605.19736 (full text verified via HTML)

**What it does:**
- Lets the **same OpenQASM 3 test run against multiple Qiskit versions** in isolated environments via a `runtime_version` pragma, explicitly designed "to expose behavioral drift" — i.e., this is a published, working implementation of **cross-Qiskit-version regression testing**.
- Emits JUnit/xUnit XML output, explicitly stated to be "suitable for CI systems such as Jenkins, **GitHub Actions**, and GitLab CI."
- Does **NOT** integrate with pytest — it is a standalone OpenQASM-native CLI tool, explicitly designed to avoid Python test frameworks.
- Supports **only Qiskit** today. Cross-SDK support (Cirq, PennyLane) and execution on real hardware are explicitly listed as future work, not implemented.
- Has no automated regression/equivalence-detection algorithm — developers write assertions manually; it does not use decision-diagram or ZX-calculus equivalence checking (contrast with MQT QCEC).

**Verdict: PARTIALLY CONTRADICTS the originally claimed gap.** A published, CI-integrable, cross-Qiskit-version regression-testing framework already exists (as of May 2026). This materially narrows any defensible novelty claim: "cross-Qiskit-version regression testing with CI-compatible output" is **not novel**. What QUTest does *not* provide — and what remains open — is: (a) pytest-native integration (Python-ecosystem-idiomatic test discovery/fixtures), (b) cross-SDK testing (Qiskit vs Cirq vs PennyLane), (c) automated equivalence/regression *detection* (vs. manually-written assertions), and (d) any bug-corpus-driven or state-aware detection layer.

### 2. arXiv:2506.17306 — see C04 section above (the 31% survey paper). Supports the gap (identifies unmet need) but is not a tool paper.

### 3. "A Survey on Testing and Analysis of Quantum Software"

**Authors:** Matteo Paltenghi & Michael Pradel (University of Stuttgart)
**arXiv ID:** 2410.00650, submitted 2024-10-01
**URL:** https://arxiv.org/abs/2410.00650

Broad survey spanning quantum-computing, software-engineering, programming-languages, and formal-methods literature on testing/analysis techniques and benchmarks. Verified abstract and reviewed content contain **no mention of CI/CD, GitHub Actions, regression testing, or cross-SDK/version testing**. Useful as general background prior art; not directly relevant to the specific CI/CD regression-testing gap.

### 4. "Benchmarking Quantum Software Testing with Scalable Quantum Programs" (Qolumbina)

**Authors:** Li, Shao, Li, Zhao, Cai
**arXiv ID:** 2607.02029, submitted 2026-07-02
**URL:** https://arxiv.org/abs/2607.02029

Presents **Qolumbina**, a benchmark of 40 curated open-source quantum programs for quantum-software-testing (QST) evaluation. No CI/CD, no regression/cross-version testing — a static benchmark corpus, not a CI tool. Relevant to the bug/benchmark-corpus question (C07); see `bug_corpora.md`.

### 5. "Quantum Circuit Mutants: Empirical Analysis and Recommendations"

**Authors:** Mendiluze Usandizaga, Yue, Arcaini, Ali
**arXiv ID:** 2311.16913, submitted 2023-11-28; published in *Empirical Software Engineering*, 2025
**URL:** https://arxiv.org/abs/2311.16913

Large-scale mutation-testing empirical study: 700K+ faulty circuit mutants generated from 382 real circuits. No CI/CD or cross-version/cross-SDK testing content.

### Other candidates surfaced but not opened (flagged for follow-up, not verified)
2601.08367 ("Methodological Analysis of Empirical Studies in QST"), 2503.05240 (Q&A mining), 2506.02090, 2409.08844, 2509.04763 (NovaQ), 2601.13996, 2503.17322 (QITE — described as cross-platform, assembly-level, NOT cross-version), 2602.05759 (post-quantum-crypto migration CI/CD — different domain, not quantum-circuit testing). These were not independently verified and should not be cited until opened directly.

---

## MQT Debugger paper (cross-referenced from prior_art.md, Claim C02)

**Title:** "A Framework for Debugging Quantum Programs"
**Authors:** Damian Rovara, Lukas Burgholzer, Robert Wille
**arXiv ID:** 2412.12269, submitted 2024-12-16
**URL:** https://arxiv.org/abs/2412.12269

Confirmed by opening the abstract page directly. Describes an open-source, assertion-based debugging framework (linked to github.com/munich-quantum-toolkit/debugger) for single-run quantum program debugging via classical simulation. Not a CI/CD system; not about cross-SDK-version regression testing. See `prior_art.md` for full detail.

---

## MQT QCEC paper (cross-referenced from prior_art.md, Claim C01)

**Title:** "QCEC: A JKQ tool for quantum circuit equivalence checking"
**Authors:** Lukas Burgholzer, Robert Wille
**Venue:** *Software Impacts*, 2021, DOI: 10.1016/j.simpa.2020.100051
**Source:** cited directly in the official repository's citation block (github.com/munich-quantum-toolkit/qcec)

Not independently opened via arXiv/DOI resolver in this pass (verified only via the repository's own citation metadata) — flagged as PARTIALLY CONFIRMED pending direct DOI resolution if a publication-quality citation is needed later.
