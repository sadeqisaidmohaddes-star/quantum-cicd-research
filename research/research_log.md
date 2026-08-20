# Research Log

Log of meaningful searches performed and what they returned. Compiled from four parallel research threads (each independently verified primary sources via WebFetch — search snippets alone were never treated as proof).

## Thread 1 — MQT QCEC & MQT Debugger (C01, C02)
Primary sources opened directly (no broad search log kept; targeted lookups of known official repos):
- github.com/munich-quantum-toolkit/qcec — README, features, citation block, star count, license
- raw.githubusercontent.com/munich-quantum-toolkit/qcec/main/.github/workflows/ci.yml — actual CI matrix content
- github.com/munich-quantum-toolkit/qcec/tree/main/.github/workflows — workflow file listing
- mqt.readthedocs.io/en/latest/handbook/04_verification.html — official framing of QCEC's use case
- github.com/munich-quantum-toolkit/debugger — README, features, DAP server description, star/fork count
- arxiv.org/abs/2412.12269 — verified title, authors, date, full abstract of MQT Debugger paper
- pypi.org/project/mqt.qcec/ — failed to load, not used as evidence

## Thread 2 — 31% statistic & two arXiv papers (C04, C05, C06)
1. `quantum software developers survey "testing tools" percent practitioners` → surfaced arXiv:2506.17306 with the 31% figure in snippet
2. `"quantum software" empirical study developers practices testing arXiv survey` → surfaced 2607.02029, 2601.08367, 2506.17306, 2311.16913, 2503.05240, 2410.00650
3. WebFetch arxiv.org/abs/2506.17306 → confirmed title/authors/dates/abstract statistic
4. WebFetch arxiv.org/pdf/2506.17306v2 (raw PDF) → failed, compressed PDF stream unreadable by WebFetch
5. WebFetch arxiv.org/html/2506.17306v2 → 404, no HTML version published
6. WebFetch ojcchar.github.io mirror PDF → also unreadable via WebFetch
7. **Read tool directly on downloaded PDF** (bypassing WebFetch's PDF limitation) → successfully extracted full 52-page text, confirmed exact quote ("Only eight of 26 respondents (31%)...") and methodology
8. WebFetch arxiv.org/abs/2410.00650 → confirmed title/authors/date/abstract, no CI/CD or cross-SDK content
9. WebFetch arxiv.org/abs/2607.02029 → confirmed Qolumbina details, no CI/CD content
10. `quantum software "CI/CD" regression testing cross-version SDK arXiv` → surfaced QUTest (2605.19736), NovaQ, QITE, "Software Testing in the Quantum World," a post-quantum-crypto CI/CD paper, a quantum-annealing-for-test-prioritization paper
11. `arXiv quantum circuit mutants empirical analysis recommendations 2311.16913` → confirmed authors/venue
12. WebFetch arxiv.org/html/2605.19736 (QUTest full HTML) → confirmed cross-version testing mechanism, CI output format, pytest non-integration, single-SDK limitation, explicit future-work statement re: Cirq/PennyLane

Unopened candidates flagged for future verification: 2601.08367, 2503.05240, 2506.02090, 2409.08844, 2509.04763 (NovaQ), 2601.13996, 2503.17322 (QITE), 2602.05759 (PQC migration CI/CD).

## Thread 3 — Q-Trace/debugging systems, bug corpora, autonomous tooling (C03, C07, C12)
Queries included (6+ distinct, varied phrasing): "Q-Trace quantum debugging tool", "quantum software bug dataset defect taxonomy empirical study GitHub", "Bugs4Q quantum software defect dataset Qiskit", "QBugs quantum bug dataset benchmark", "autonomous agent quantum software testing CI/CD state-aware regression", plus follow-on primary-source fetches of: arxiv.org/html/2512.13422 (QMon), arxiv.org/pdf/2508.14533 (TraceQ), Microsoft QDK docs (Trace Simulator), arxiv.org/abs/2507.16255 (CUDA-Q statistical assertions), arxiv.org/abs/2506.18458 (Bloq/AutoBloq), arxiv.org/pdf/2206.01111 (MorphQ), arxiv.org/abs/2108.09744 (Bugs4Q), arxiv.org/abs/2606.27124 (Bugs4Q cross-version replication), arxiv.org/abs/2103.16968 (QBugs), arxiv.org/abs/2512.24656 (32K mined bug reports), arxiv.org/abs/2606.07314 (QBugLM).

## Thread 4 — GitHub/PyPI search for pytest plugins & CI/CD products (C08, C09, C10, C11)

| Query/tool | Result summary |
|---|---|
| `gh search repos "quantum pytest"` | 0 results |
| `gh search repos "pytest-quantum"` | 5 hits: qbench/pytest-quantum, Agbamo/pytest-quantumunit, jamesharris1307/…, JMORAF87/qc-assert, metin-5115/qtest |
| `gh search repos "quantum regression testing"` | 0 results |
| `gh search repos "quantum equivalence checking"` | 2 hits, both unrelated SAT-solver student repos |
| `gh api repos/qbench/pytest-quantum` + readme + workflows | Confirmed real PyPI package v1.0.0; CI matrix is Python/OS only |
| `gh api repos/metin-5115/qtest` + readme + workflows | Confirmed real PyPI package v0.1.0; CI matrix is Python/OS only |
| `gh api repos/JMORAF87/qc-assert` + readme + workflow | Minimal single-job CI, not on PyPI |
| `curl pypi.org/pypi/pytest-quantum/json` | Confirms 6 releases 0.1.0→1.0.0 |
| `curl pypi.org/pypi/qtest-quantum/json` | Confirms 1 release 0.1.0 |
| PyPI simple-index grep `*quantum*test*` / `pytest-*quantum*` | Surfaced `quantum-test`, `quantum-tests` (empty/squatted, v0.0.0) |
| `gh search code "matrix qiskit-version"` | 0 results |
| `gh search code "qiskit==0" path:.github/workflows` | 16 hits; revealed Qiskit's official min/dev/latest version-testing CI template reused across ~8 Qiskit-ecosystem repos |
| `gh api repos/Qiskit/qiskit-addon-cutting/contents/.github/workflows/README.md` | Full documentation of test_latest/development/minimum_versions.yml confirmed |
| `gh api .../test_development_versions.yml` (raw) | Confirmed use of `extremal-python-dependencies` for dev Qiskit builds |
| `gh api repos/Qiskit/qiskit/contents/.github/workflows` | Listed Qiskit core's own workflows, found `qpy.yml` |
| `gh api .../qpy.yml` (raw) | Confirmed real QPY cross-version backward-compat test harness |
| `gh search repos "quantum SDK version compatibility"` / `"cross-version quantum"` | 0 results each |
| `gh search repos "quantum" "github action"` | ~18 hits, nearly all post-quantum-cryptography tools, filtered out as noise |
| `gh search repos "quantum transpiler regression"` | 1 hit: furqan-nr/quantum-transpiler-regression-testing |
| `gh search repos "openqasm regression"` | 0 results |
| `gh api repos/furqan-nr/quantum-transpiler-regression-testing` + readme | Confirmed real; 0 stars, created 2026-06-28 |
| `WebFetch https://doi.org/10.5281/zenodo.21020113` | Independently confirmed real Zenodo software record, authors, institution, date |
| `gh search repos topic:quantum-computing "ci"` | Returned established SDKs/libraries (e.g. Cirq), none matching a CI-testing-product description |

---

*All four research threads complete as of 2026-08-20. See claims.md for the consolidated claims table and gap_analysis.md for synthesis.*
