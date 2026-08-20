# Quantum CI/CD Regression Testing — Prior Art Research

A rigorous, primary-source-verified investigation into whether a genuine open research/software gap exists around CI/CD regression testing for quantum software — specifically, an open-source pytest/GitHub Actions style infrastructure that runs quantum projects across SDK versions and detects regressions/equivalence failures.

**This is a research project, not a software product.** No architecture, plugin, or GitHub Actions workflow has been implemented here. Every finding is traced to a primary source (official repository, arXiv paper, DOI record) that was actually opened and inspected — never accepted from a search-result snippet alone.

**Start here → [`research/README.md`](research/README.md)**, then **[`research/gap_analysis.md`](research/gap_analysis.md)** for the final synthesis.

## Contents

| File | What it covers |
|---|---|
| [`research/README.md`](research/README.md) | Index and headline findings |
| [`research/claims.md`](research/claims.md) | Consolidated claims table (C01–C13): status, evidence, source, confidence |
| [`research/prior_art.md`](research/prior_art.md) | Full prior-art comparison matrix + detailed per-system narrative |
| [`research/papers.md`](research/papers.md) | Every academic paper verified, incl. the 31% statistic's exact source |
| [`research/repositories.md`](research/repositories.md) | GitHub/PyPI repositories inspected for pytest plugins and CI/CD tooling |
| [`research/ci_cd_landscape.md`](research/ci_cd_landscape.md) | Synthesis of CI/CD-specific findings |
| [`research/quantum_testing_landscape.md`](research/quantum_testing_landscape.md) | Debugging/tracing systems and the autonomous-tooling question |
| [`research/bug_corpora.md`](research/bug_corpora.md) | Bug/fault corpus investigation |
| [`research/gap_analysis.md`](research/gap_analysis.md) | Final synthesis — what's novel, what isn't, the narrowed gap |
| [`research/evidence.json`](research/evidence.json) | Machine-readable structured records for every claim |
| [`research/research_log.md`](research/research_log.md) | Every search query run and what it returned |
| [`research/sources.md`](research/sources.md) | Full list of every URL opened, incl. inaccessible/unverified sources |
| [`research/raw_notes.md`](research/raw_notes.md) | Methodology caveats and miscellaneous observations |

## Headline finding

A published tool (**QUTest**, arXiv:2605.19736, May 2026) already implements cross-Qiskit-version regression testing with GitHub Actions-compatible output — this materially narrows the original novelty claim. The narrowest defensible remaining gap is a **pytest-native, cross-SDK** (not just cross-version), **automated** regression/equivalence-detection framework packaged as reusable GitHub Actions tooling. See `research/gap_analysis.md` Section 13.

## Status

Architecture/design work is **blocked pending human review** of this research. See `research/gap_analysis.md` Section 14 for what further evidence would be needed before a publication-quality novelty claim.

## Rendered version

This research is also presented as a human-readable web section at [quantum.sadeqi.me/research](https://quantum.sadeqi.me/research) on the Quantum Powerhouse site, which links back to this repository as the source of truth for the raw artifacts.
