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

## Confidence caveats worth restating up front for whoever reads gap_analysis.md next
- The N=26 sample behind the 31% statistic is small; the authors themselves flag generalizability limits. Use it as "one survey found," not as an established field-wide constant.
- Several "absence" findings (C11, C12, and parts of C10) are NOT_FOUND after a reasonably broad search, not proven non-existence. A differently-worded search, or access to non-English-language or non-indexed venues, could still surface something missed.
