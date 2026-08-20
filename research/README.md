# Research: Prior Art for Quantum CI/CD Regression Testing

This directory documents a rigorous prior-art and claim-verification research phase for the question:

> Is there a genuine open research/software gap around CI/CD regression testing for quantum software — specifically, an open-source pytest/GitHub Actions style infrastructure that runs quantum projects across SDK versions and detects regressions/equivalence failures?

**Architecture/design status: BLOCKED UNTIL HUMAN REVIEW.** No implementation, plugin, or GitHub Actions workflow has been built. This directory is research only.

## How to read this directory

1. **`gap_analysis.md`** — start here. The final synthesis: what exists, what's novel, what isn't, and the narrowest defensible research gap.
2. **`claims.md`** — the consolidated claims table (C01–C13) with status, evidence, primary source, and confidence for every claim in the original research brief.
3. **`prior_art.md`** — detailed per-system narrative findings, including the full prior-art comparison matrix (all systems × all dimensions).
4. **`papers.md`** — every academic paper verified, including the confirmed 31% statistic source and the reconstructed "two arXiv papers" candidates (most notably QUTest).
5. **`repositories.md`** — every GitHub repository/PyPI package inspected for pytest plugins and CI/CD products.
6. **`ci_cd_landscape.md`** — synthesis of the CI/CD-specific findings (Qiskit's own version-matrix template, QPY compat harness, QUTest, the transpiler-regression pilot).
7. **`quantum_testing_landscape.md`** — debugging/tracing systems and the state-aware/autonomous-tooling question.
8. **`bug_corpora.md`** — the bug/fault corpus investigation (Bugs4Q and related work).
9. **`evidence.json`** — machine-readable structured records for every major claim.
10. **`research_log.md`** — every search query run across all four research threads and what it returned.
11. **`sources.md`** — full list of every URL opened, including inaccessible/unverified sources explicitly flagged.
12. **`raw_notes.md`** — methodology caveats and miscellaneous observations not elevated to full claim status.

## Headline findings

- **MQT QCEC and MQT Debugger are real and mature**, but solve narrower problems (equivalence checking; single-run assertion debugging) than the proposed CI/CD infrastructure — confirmed by direct inspection of their repos, CI configs, and docs.
- **The 31% practitioner statistic is real and precisely traceable**: "Only eight of 26 respondents (31%) reported using quantum-specific testing tools" — Zappin et al., arXiv:2506.17306, Finding 2, p.18.
- **The most important finding of this research phase**: **QUTest** (arXiv:2605.19736, May 2026) already implements cross-Qiskit-version regression testing with GitHub Actions-compatible output. This materially narrows any novelty claim.
- **A bug corpus (Bugs4Q) already exists and has already been used for a cross-Qiskit-version regression study** (21 versions, 77,700 executions, arXiv:2606.27124) — the "no corpus exists" claim is false.
- **A single-SDK transpiler-regression pilot** ("cart," June 2026) found 38% of real transpiler bug-fixes are invisible to equivalence oracles — direct evidence equivalence checking alone is insufficient.
- **No cross-SDK (Qiskit vs Cirq vs PennyLane) regression/equivalence tool was found anywhere.** This is the strongest remaining candidate for genuine novelty, combined with automated (not hand-written) regression detection, pytest-native packaging, and reusable GitHub Actions distribution.
- **The state-aware/autonomous-agent angle is genuinely unaddressed** in the literature, but is the least load-bearing and most speculative part of the original idea.

See `gap_analysis.md` Section 13 for the recommended narrowed research gap, and Section 14 for what further evidence is needed before a publication-quality novelty claim.
