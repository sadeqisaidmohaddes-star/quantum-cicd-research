# Raw Notes / Methodology Caveats

## Research process
This research phase was conducted via four independent, parallel research passes (one per claim cluster), each required to open primary sources directly via WebFetch/gh CLI rather than trust search-result snippets. Findings were then cross-referenced and synthesized into the deliverable files. No claim in `claims.md` or `evidence.json` is based on a snippet alone.

## Miscellaneous observations not elevated to full claim status

- **"Q-Trace" likely originates from confusion with TraceQ or MQT Debugger.** Neither name resembles "Q-Trace" closely enough to be a confident match; flagged as FALSE/NOT FOUND rather than guessing which was intended.
- **The two "alleged arXiv papers"** referenced in the original project framing were never given specific IDs to check against in this research task. This is itself worth flagging to the project owner: if specific IDs exist somewhere (e.g. in an earlier conversation, notes, or slide deck), they should be supplied and checked directly rather than relying on the reconstructed candidates here (QUTest, the 31% survey paper, and others).
- **QUTest (arXiv:2605.19736) and the "cart" transpiler-regression pilot (Zenodo 10.5281/zenodo.21020113) are both extremely recent** (May and June 2026 respectively, relative to the August 2026 research date) and low-adoption (cart has 0 GitHub stars). Their existence proves the *idea space* is not virgin territory and is actively being worked on by multiple independent groups right now — but neither is an established, widely-adopted solution. This cuts both ways: it undercuts a strong "no one has thought of this" novelty claim, but also means the space is not yet consolidated, leaving room for a more complete/robust implementation.
- **MorphQ** (arXiv:2206.01111) does metamorphic testing *of Qiskit itself* — this is a different problem (testing the SDK) from testing *user projects* against multiple SDK versions (the proposed idea). Flagged as only partially relevant and not deeply verified; a follow-up pass should confirm this distinction holds before citing MorphQ in either direction.
- **PyPI has squatted/placeholder packages** (`quantum-test`, `quantum-tests`) with no real content — a reminder that package-index presence alone is not evidence of a real, functioning tool.
- **Post-quantum cryptography (PQC) tooling is a major source of false-positive noise** in "quantum" + "GitHub Actions"/"CI" searches — PQC migration scanners (pqc-scan, KyberCheck, pqc-guard-action, etc.) are an entirely unrelated field that happens to share the "quantum" keyword. Filtered out during research; any future search in this space should apply the same filter.
- **WebFetch could not parse arXiv PDF binary streams directly** for at least one paper (2506.17306) — worked around by using the Read tool on a locally downloaded copy. Future research passes hitting the same limitation should use the same workaround rather than giving up on a source.

## Verification pass 2 (2026-08-20)

Before extending this research into a public website, two open items flagged in gap_analysis.md Section 14
("evidence still required before a publication-quality novelty claim") were closed out:

1. **QCEC citation (Burgholzer & Wille, Software Impacts 2021, DOI 10.1016/j.simpa.2020.100051)** — previously
   verified only via the repo's own citation block. Attempted direct DOI resolution; ScienceDirect blocked
   full-text scraping via WebFetch (JS-rendered redirect wall), but the title/authors/venue/year were
   independently cross-confirmed via three separate bibliographic listings (Semantic Scholar, researchr, and
   the ACM/Elsevier index) found through a fresh web search — upgraded from "repo-only" to "independently
   cross-confirmed."
2. **Bugs4Q citation (JSS vol. 205, 2023, DOI 10.1016/j.jss.2023.111805)** — same DOI-resolution attempt,
   same ScienceDirect block, same workaround. This one surfaced a genuine **correction**: the ACM DL listing
   for the published JSS 2023 version states the benchmark contains **42** real, manually-validated Qiskit
   bugs mined from GitHub, StackOverflow, and Stack Exchange — not the "~50–67 (Bugs4Q-NA)" figure carried
   over from pass 1, which could not be re-confirmed and is now marked UNVERIFIED. The 2021 arXiv preprint's
   36-bug figure is still correct for that specific version. All research files (`bug_corpora.md`,
   `claims.md`, `prior_art.md`, `evidence.json`) were updated to cite 36 (preprint) or 42 (JSS 2023,
   preferred) instead of the unconfirmed range.

This correction does not change any claim's overall status (C07 remains FALSE — a real corpus exists) but it
does change a specific number that had propagated across four files without independent verification. Per
the project's research-integrity rule, it is documented here rather than silently fixed.

## Confidence caveats worth restating up front for whoever reads gap_analysis.md next
- The N=26 sample behind the 31% statistic is small; the authors themselves flag generalizability limits. Use it as "one survey found," not as an established field-wide constant.
- Several "absence" findings (C11, C12, and parts of C10) are NOT_FOUND after a reasonably broad search, not proven non-existence. A differently-worded search, or access to non-English-language or non-indexed venues, could still surface something missed.
