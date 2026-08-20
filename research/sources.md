# Sources — Full List

All URLs below were opened directly (WebFetch / gh CLI / Zenodo DOI resolution) during this research phase, not treated as proof from search-result snippets alone.

## Official repositories / documentation
- https://github.com/munich-quantum-toolkit/qcec — MQT QCEC (README, features, citation block)
- https://raw.githubusercontent.com/munich-quantum-toolkit/qcec/main/.github/workflows/ci.yml — MQT QCEC CI matrix (raw YAML)
- https://github.com/munich-quantum-toolkit/qcec/tree/main/.github/workflows — MQT QCEC workflow listing
- https://mqt.readthedocs.io/en/latest/handbook/04_verification.html — MQT verification handbook (official framing of QCEC)
- https://github.com/munich-quantum-toolkit/debugger — MQT Debugger (README, DAP server description)
- https://github.com/qbench/pytest-quantum — pytest-quantum plugin
- https://pypi.org/project/pytest-quantum/ — pytest-quantum PyPI release history
- https://github.com/metin-5115/qtest — qtest-quantum plugin
- https://pypi.org/project/qtest-quantum/ — qtest-quantum PyPI release history
- https://github.com/JMORAF87/qc-assert — qc-assert plugin
- https://github.com/Qiskit/qiskit-addon-cutting — official Qiskit ecosystem CI template source
- https://github.com/Qiskit/qiskit/blob/main/.github/workflows/qpy.yml — Qiskit QPY cross-version compat harness
- https://github.com/furqan-nr/quantum-transpiler-regression-testing — "cart" transpiler regression-testing pilot
- https://github.com/Z-928/Bugs4Q — Bugs4Q bug corpus repository

## arXiv papers (abstract and/or full text verified directly)
- https://arxiv.org/abs/2412.12269 — MQT Debugger: "A Framework for Debugging Quantum Programs" (Rovara, Burgholzer, Wille)
- https://arxiv.org/abs/2506.17306 — 31% statistic source: "Challenges and Practices in Quantum Software Testing and Debugging: Insights from Practitioners" (Zappin, Stalnaker, Chaparro, Poshyvanyk)
- https://arxiv.org/abs/2605.19736 — QUTest: "A Native Testing Framework for Quantum Programs" (Campos)
- https://arxiv.org/abs/2410.00650 — "A Survey on Testing and Analysis of Quantum Software" (Paltenghi, Pradel)
- https://arxiv.org/abs/2607.02029 — Qolumbina: "Benchmarking Quantum Software Testing with Scalable Quantum Programs" (Li, Shao, Li, Zhao, Cai)
- https://arxiv.org/abs/2311.16913 — "Quantum Circuit Mutants: Empirical Analysis and Recommendations" (Mendiluze Usandizaga, Yue, Arcaini, Ali)
- https://arxiv.org/html/2512.13422 — QMon
- https://arxiv.org/pdf/2508.14533 — TraceQ
- https://arxiv.org/abs/2507.16255 — CUDA-Q Statistical Assertions
- https://arxiv.org/abs/2506.18458 — Bloq/AutoBloq
- https://arxiv.org/pdf/2206.01111 — MorphQ
- https://arxiv.org/abs/2108.09744 — Bugs4Q
- https://arxiv.org/abs/2606.27124 — Cross-Qiskit-version Bugs4Q replication study (ICSME 2026 Replication Track)
- https://arxiv.org/abs/2103.16968 — QBugs
- https://arxiv.org/abs/2512.24656 — 32,296-bug-report mined dataset (Yousuf & Sofi)
- https://arxiv.org/abs/2606.07314 — QBugLM

## Other primary sources
- https://doi.org/10.5281/zenodo.21020113 — Zenodo software record for "cart" (independently resolved, not just repo self-description)
- Journal: Burgholzer & Wille, "QCEC: A JKQ tool for quantum circuit equivalence checking," *Software Impacts*, 2021, DOI 10.1016/j.simpa.2020.100051 (verified via repo citation block only, not independently opened via DOI resolver — flagged PARTIALLY CONFIRMED in papers.md)
- Journal: Bugs4Q extended version, *Journal of Systems and Software*, vol. 205 (2023), DOI 10.1016/j.jss.2023.111805 (verified via citing papers, not independently opened via DOI resolver)

## Sources attempted but inaccessible (documented, not silently dropped)
- https://pypi.org/project/mqt.qcec/ — failed to load via WebFetch; not used as evidence, maturity assessed from GitHub signals instead
- https://arxiv.org/pdf/2506.17306v2 — WebFetch could not parse compressed PDF stream; worked around via Read tool on downloaded PDF
- https://arxiv.org/html/2506.17306v2 — 404, no HTML version published
- https://ojcchar.github.io/files/42-tosem25-quantum-test-debug.pdf — mirror PDF, also unreadable via WebFetch

## Unverified leads (explicitly flagged — do not cite without independent confirmation)
- arXiv:2601.08367, 2503.05240, 2506.02090, 2409.08844, 2509.04763 (NovaQ), 2601.13996, 2503.17322 (QITE), 2602.05759 (PQC migration CI/CD) — surfaced by search, not opened/verified in this research phase
- A companion "4,984-issue / 36-repo Qiskit-ecosystem benchmark" mentioned alongside arXiv:2512.24656 in search snippets — not independently opened
- `n26124939/Quentangle-SAT` — GitHub repo surfaced under "quantum equivalence checking" search, legitimacy/functionality not verified
