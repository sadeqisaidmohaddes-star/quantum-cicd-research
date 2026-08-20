# Prior Art — Detailed Findings

Status legend: CONFIRMED | PARTIALLY CONFIRMED | UNVERIFIED | FALSE / CONTRADICTED | NOT FOUND AFTER SEARCH

Jump to: [Prior-Art Comparison Matrix](#prior-art-comparison-matrix) (full table, all systems, all dimensions) — detailed per-system narrative follows below it.

---

## Prior-Art Comparison Matrix

Cells use YES / NO / PARTIAL / UNKNOWN only — never assumed. "—" = not applicable (e.g. a paper/dataset has no Debugging dimension).

| Project/System | Type | Open Source? | Academic? | Quantum SDKs | Testing | Regression Testing | Equivalence Checking | Debugging | Tracing | pytest | GitHub Actions | CI/CD | Cross-Version | Cross-SDK | Bug/Fault Corpus | Automated Fault Detection | State-Aware | Autonomous/Agentic | Primary Source | Overlap w/ Proposed Work |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **MQT QCEC** | Library | YES | YES | Qiskit, OpenQASM | NO | NO | YES | NO | NO | NO | PARTIAL (own repo only, OS/compiler matrix) | PARTIAL (own repo only) | NO | NO | NO | PARTIAL (equivalence counterexamples) | NO | NO | github.com/munich-quantum-toolkit/qcec | Solves equivalence-checking layer only |
| **MQT Debugger** | Library/tool | YES | YES | OpenQASM | NO | NO | NO | YES | PARTIAL (state inspection) | NO | PARTIAL (own repo only) | PARTIAL (own repo only) | NO | NO | NO | PARTIAL (assertion-driven localization) | NO | NO | github.com/munich-quantum-toolkit/debugger; arXiv:2412.12269 | Solves single-run assertion debugging only |
| **QMon** | Monitoring tool | UNKNOWN | YES | UNKNOWN | PARTIAL (monitoring) | NO | NO | NO | PARTIAL | YES | NO | UNKNOWN | UNKNOWN | NO | NO | NO | NO | NO | NO | arxiv.org/html/2512.13422 | Low — runtime monitoring only |
| **TraceQ** | Analysis tool | UNKNOWN | YES | N/A (surface-code) | NO | NO | NO | NO | YES | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | NO | NO | NO | arxiv.org/pdf/2508.14533 | None — hardware/QEC focused |
| **Microsoft QDK Trace Simulator** | Product | PARTIAL (QDK is OSS) | NO | Q# / QDK | PARTIAL | NO | NO | YES | YES | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | NO | NO | NO | Microsoft QDK docs | Low — resource estimation/debugging, single-run |
| **CUDA-Q Statistical Assertions** | Debugging technique | UNKNOWN | YES | CUDA-Q | NO | NO | NO | YES | NO | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | PARTIAL | NO | NO | arxiv.org/abs/2507.16255 | Low — single-run statistical debugging |
| **Proq** | Fault localization | UNKNOWN | YES | UNKNOWN | NO | NO | NO | YES | NO | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | YES (single-run) | NO | NO | cited in arXiv:2506.18458 | None — single-circuit fault localization |
| **Bloq / AutoBloq** | Fault localization | UNKNOWN | YES | UNKNOWN | NO | NO | NO | YES | NO | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | YES (single-run, outperforms Proq) | NO | NO | arXiv:2506.18458 | None — single-circuit fault localization |
| **MorphQ** | Metamorphic testing | YES | YES | Qiskit (tests the SDK itself) | YES | PARTIAL | NO | NO | NO | NO | UNKNOWN | UNKNOWN | UNKNOWN | NO | NO | NO | YES | NO | NO | arXiv:2206.01111 | Partial — tests Qiskit itself, not user projects; not deeply verified |
| **Bugs4Q / Bugs4Q-Robust** | Bug corpus | YES | YES | Qiskit | — | — | — | — | — | — | NO | NO | — | — | — | YES (36-67 real bugs) | NO | NO | NO | arXiv:2108.09744; github.com/Z-928/Bugs4Q | Reusable corpus, not a CI tool itself |
| **Cross-version Bugs4Q replication study** | Research study | Fork released | YES | Qiskit (21 versions) | YES | YES | NO | NO | NO | NO | UNKNOWN | UNKNOWN | YES (21 Qiskit versions, 77,700 execs) | NO | Uses Bugs4Q | YES (reproducibility measurement) | NO | NO | arXiv:2606.27124 | High — closest academic precedent for cross-version regression study |
| **QBugs** | Bug corpus + infra | YES | YES | UNKNOWN (algorithmic) | — | — | — | — | — | — | UNKNOWN | UNKNOWN | — | — | YES | NO | NO | NO | arXiv:2103.16968 | Standardization attempt for debugging-technique comparison |
| **QBugLM** | Agentic benchmark | UNKNOWN | YES | OpenQASM 3 (framework-agnostic) | YES | NO | NO | NO | NO | NO | UNKNOWN | UNKNOWN | NO | NO | YES (bug-injection benchmark) | YES | NO | YES | arXiv:2606.07314 | Closest agentic system found; no CI/CD, no cross-version |
| **Qolumbina** | Benchmark suite | YES | YES | Multiple (curated programs) | PARTIAL | NO | NO | NO | NO | NO | UNKNOWN | UNKNOWN | NO | NO | PARTIAL (program benchmark, not labeled faults) | NO | NO | NO | arXiv:2607.02029 | Benchmark corpus only, not a testing tool |
| **QUTest** | Testing framework | YES (implied by paper; repo not independently confirmed) | YES | Qiskit only | YES | YES | NO (manual assertions) | NO | NO | NO | NO — explicitly avoids pytest | YES (JUnit/xUnit output for GH Actions) | YES | YES (via runtime_version pragma across Qiskit versions) | NO (Qiskit only; Cirq/PennyLane future work) | NO | PARTIAL (manual assertions, no auto-diff) | NO | NO | arXiv:2605.19736 | **HIGH — most directly overlapping system found** |
| **pytest-quantum** | pytest plugin | YES (PyPI) | NO | Qiskit, Cirq, pytket | YES | PARTIAL | PARTIAL (cross-framework only) | YES (cross-framework only) | NO | NO | YES | YES (own CI) | YES (own CI) | NO | YES (framework-to-framework only) | NO | PARTIAL | NO | NO | github.com/qbench/pytest-quantum | Partial — pytest-native + cross-framework equivalence, but no cross-version |
| **qtest-quantum** | pytest plugin | YES (PyPI) | NO | Qiskit (implied) | YES | PARTIAL | PARTIAL (single-SDK fidelity) | PARTIAL | NO | NO | YES | YES (own CI) | YES (own CI) | NO | NO | NO | PARTIAL | NO | NO | github.com/metin-5115/qtest | Partial — pytest-native, single-SDK only, immature (0 stars) |
| **qc-assert** | pytest plugin | YES (not on PyPI) | NO | UNKNOWN | PARTIAL | Stated intent only | NO | NO | NO | NO | YES | YES (basic) | NO | NO | NO | NO | NO | NO | NO | github.com/JMORAF87/qc-assert | Minimal — intent stated, not implemented |
| **Qiskit ecosystem CI template** (test_latest/dev/minimum_versions.yml) | CI template | YES | NO (official SDK tooling) | Qiskit | YES (runs existing tests) | PARTIAL (pass/fail only, no diffing) | NO | NO | NO | NO | UNKNOWN | YES | YES | YES (latest/dev/min tiers) | NO | NO | NO | NO | NO | github.com/Qiskit/qiskit-addon-cutting | Reusable version-tier CI, but no behavioral diffing or regression detection |
| **Qiskit QPY compat harness** | Internal CI | YES (in Qiskit repo) | NO | Qiskit | YES (serialization only) | YES (serialization only) | NO | NO | NO | NO | UNKNOWN | YES | YES | YES (serialization format only) | NO | NO | YES (serialization only) | NO | NO | github.com/Qiskit/qiskit/.github/workflows/qpy.yml | Narrow — serialization compatibility only, not externally reusable |
| **quantum-transpiler-regression-testing ("cart")** | Research tool/pilot | YES | YES (paper submitted, not confirmed accepted) | Qiskit transpiler only | YES | YES | PARTIAL (finds gaps in equivalence oracles) | NO | NO | NO | NO | UNKNOWN | UNKNOWN | NO | NO | NO | YES | NO | NO | github.com/furqan-nr/quantum-transpiler-regression-testing; Zenodo 10.5281/zenodo.21020113 | High — closest regression-testing *pilot*; single-SDK, CLI, brand new, 0 stars |
| **Zappin et al. practitioner survey** (not a tool) | Empirical study | — | YES | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — | arXiv:2506.17306 | Evidence of unmet need (31% stat, calls for CI/CD tooling); not a system |

**Reading the matrix:** No row is YES across pytest + Cross-Version + Cross-SDK + Automated Fault Detection simultaneously. QUTest comes closest (YES on CI/CD, Cross-Version, Regression Testing) but is explicitly NO on pytest and Cross-SDK. `pytest-quantum` is YES on pytest but only PARTIAL/framework-level, NO on Cross-Version. This is the empirical basis for the narrowed gap in `gap_analysis.md`.

---

## MQT QCEC (Claim C01) — Status: CONFIRMED (existence/capabilities); overlap claim FALSE

**What it is:** MQT QCEC ("Quantum Circuit Equivalence Checking") is an open-source C++20/Python library from the Munich Quantum Toolkit (MQT), developed by the Chair for Design Automation, Technical University of Munich, part of the Munich Quantum Software Stack (Munich Quantum Valley initiative).

**What it does:** Determines whether two quantum circuits are functionally equivalent. Implements multiple equivalence-checking engines — decision-diagram (DD) construction, alternating DD, simulation-based falsification, and ZX-calculus rewriting — combined into an automated flow that either proves equivalence or produces a counterexample. Supports partial equivalence checking (ancillary/garbage qubits, measured output distributions) and parameterized/symbolic circuits. Primary documented use case: verifying that a compiled/transpiled circuit remains equivalent to its original source circuit.

**SDK/format support:** Qiskit `QuantumCircuit` objects and OpenQASM files. No evidence of native Cirq or PennyLane integration.

**CI/CD and regression-testing capability:** Its own `.github/workflows/ci.yml` (fetched directly, raw content inspected) runs a matrix of OS × architecture × compiler (ubuntu/macos/windows × x86/arm × gcc/clang/msvc, release/debug) to validate QCEC's *own build*. There is **no Python-SDK-version matrix and no cross-SDK-version regression harness**. The official MQT verification handbook (`04_verification.html`) frames QCEC purely as an equivalence-checking methodology/library — it does not mention CI/CD integration, regression testing, or cross-SDK/version testing as a use case.

**Maturity:** 117 GitHub stars, 1,516+ commits on main, MIT license, active CD/release-drafter automation implying regular PyPI releases (`pip install mqt.qcec`). Actively maintained, cross-platform tested.

**Academic citation (verified):** Burgholzer, L. & Wille, R., "QCEC: A JKQ tool for quantum circuit equivalence checking," *Software Impacts*, 2021, DOI: 10.1016/j.simpa.2020.100051 (cited in the repo's own citation block; additional cited papers cover compilation verification, parameterized circuits, and ZX-calculus methods, not individually re-verified beyond the reference list).

**Overlap verdict:** QCEC solves the **algorithmic equivalence-checking layer** — one-shot pairwise verification that two given circuits are functionally equivalent. It does **not** solve: (1) reusable CI/CD harness or pytest plugin for discovering/running a project's quantum tests; (2) matrix execution across multiple *versions* of a quantum SDK to catch upgrade-induced behavioral regressions; (3) cross-SDK (Qiskit vs Cirq vs PennyLane) equivalence testing; (4) a GitHub Actions-native regression-testing product for arbitrary user projects; (5) machine-readable regression reports for CI. A system that uses QCEC as one equivalence-checking *component* inside a cross-SDK-version CI harness would not duplicate QCEC — the gap is specifically the orchestration/CI/cross-version layer.

**Sources opened directly:**
- https://github.com/munich-quantum-toolkit/qcec (README, features, citation block, star count, license)
- https://raw.githubusercontent.com/munich-quantum-toolkit/qcec/main/.github/workflows/ci.yml (actual CI matrix content)
- https://github.com/munich-quantum-toolkit/qcec/tree/main/.github/workflows (workflow file listing)
- https://mqt.readthedocs.io/en/latest/handbook/04_verification.html (official framing of QCEC's use case)

---

## MQT Debugger (Claim C02) — Status: CONFIRMED (existence/capabilities); overlap claim FALSE

**What it is:** "MQT Debugger — A semi-automated tool for debugging quantum programs," also part of the Munich Quantum Toolkit, built on MQT Core.

**What it does:** Assertion- and simulation-based debugging (not classical interactive breakpoint stepping, though it does expose state inspection such as `state.get_state_vector_full()` and a Debugger Adapter Protocol (DAP) server for IDE integration). Developers place assertions in their quantum program; assertions are evaluated via classical simulation; on assertion failure, the framework runs diagnostic methods to localize probable error causes. This matches the associated arXiv paper's description exactly (below).

**SDK/format support:** OpenQASM input via Python bindings (`mqt.debugger` on PyPI). No native Qiskit/Cirq/PennyLane SDK integration found.

**CI/CD and regression-testing capability:** Has GitHub Actions CI/CD workflows and codecov coverage tracking, but this is standard software engineering CI for **the debugger's own codebase** (build/test/lint), not a feature for testing other people's quantum programs across SDK versions. No cross-version testing, no pytest-plugin-style capability for user projects.

**Maturity:** Much smaller/younger than QCEC — 21 stars, 4 forks, 496 commits, MIT license. Real and actively developed, but a small project.

**Academic citation (verified by opening the arXiv abstract page directly):**
- Title: "A Framework for Debugging Quantum Programs"
- Authors: Damian Rovara, Lukas Burgholzer, Robert Wille
- arXiv ID: 2412.12269, submitted 2024-12-16
- Abstract confirms: describes scarcity of debugging tools for quantum programs; proposes an open-source assertion-based debugging framework (linked to the `mqt-debugger` repo) where users place assertions evaluated via classical simulation and the framework diagnoses failure causes.
- Explicitly **not** a CI/CD system and **not** about regression testing across SDK versions.

**Overlap verdict:** MQT Debugger solves single-run, assertion-based fault localization within one quantum program execution, with IDE integration. It does not address CI/CD orchestration, cross-SDK-version regression detection, or automated test discovery across a project.

**Sources opened directly:**
- https://github.com/munich-quantum-toolkit/debugger (README, features, DAP server description, star/fork count)
- https://arxiv.org/abs/2412.12269 (verified title, authors, date, full abstract)

---

## Q-Trace / Other Quantum Debugging Systems (Claim C03)

**"Q-Trace" as a named quantum debugging tool — Status: FALSE / NOT FOUND.** Web searches for "Q-Trace" return unrelated products (a manufacturing-traceability SaaS, an ARM Cortex-M embedded trace tool). No quantum-specific tool by that exact name exists. It appears the name was confused with, or is a garbled reference to, real systems below (most plausibly **TraceQ**, a trace-based analysis tool for surface-code layouts).

Real, primary-sourced systems found:

| System | What it does | Open Source | Academic | Primary Source | Overlap w/ proposed CI/CD regression idea |
|---|---|---|---|---|---|
| **QMon** | Monitors quantum circuit execution via mid-circuit measurement/reset | Unknown | Yes | arxiv.org/html/2512.13422 | Low — runtime monitoring, not CI/version regression |
| **TraceQ** | Trace-based analysis of logical-qubit spatial-temporal activity on 2D surface-code layouts | Unknown | Yes | arxiv.org/pdf/2508.14533 | None — hardware/error-correction focused |
| **Microsoft QDK Trace Simulator** | Debugs classical control code + estimates resources for quantum programs | Part of QDK (OSS) | No (product) | Microsoft docs | Low — simulation/resource estimation, not regression detection |
| **Statistical Assertions (CUDA-Q)** | GPU-accelerated statistical assertion-based debugging | Unknown | Yes | arxiv.org/abs/2507.16255 | Low — single-run debugging, not cross-version |
| **Proq** | Fault localization via projection-based assertions (Birkhoff–von Neumann quantum logic); works on measurement-restricted hardware | Unknown | Yes | cited in Bloq paper (arXiv 2506.18458); "A Tool For Debugging Quantum Circuits" (ResearchGate) | None — single-circuit fault localization |
| **Bloq / AutoBloq** | Bloch-vector-assertion fault localization; reported to outperform Proq (F1 0.74 vs 0.38 on Grover), 5x faster | Not stated | Yes — arXiv 2506.18458 (Oldfield, Laaber, Ali) | arxiv.org/abs/2506.18458 | None — fault localization within one circuit run, no CI/pytest/version-matrix integration mentioned |
| **MorphQ** | Metamorphic testing *of the Qiskit platform itself* (tests the SDK, not user code) | Yes | Yes — arXiv 2206.01111 | arxiv.org/pdf/2206.01111 | Partial — Qiskit-testing-Qiskit; see also C11; not deeply verified, flagged for follow-up |

**Bottom line:** every verified debugging/assertion tool operates at the single-circuit, single-run fault-localization level (inject → detect → localize on one snapshot of one SDK version). None perform cross-version or cross-SDK regression comparison, and none integrate with pytest or GitHub Actions.

**Lead surfaced (not independently verified in this pass — see papers.md):** "Challenges and Practices in Quantum Software Testing and Debugging: Insights from Practitioners" (TOSEM 2025, arXiv 2506.17306) surfaced as a strong candidate primary source for the C04 31%-statistic claim; passed to that research thread for verification.

---

## Existing Bug/Fault Corpora for Quantum Software (Claim C07)

**Status: EXISTS_NOT_STANDARDIZED (multiple real corpora exist; claim that "no corpus exists" is FALSE/CONTRADICTED as literally stated).** See `bug_corpora.md` for full detail. Search covered 6+ distinct queries plus follow-on primary-source fetches.

Summary of verified corpora:
1. **Bugs4Q** (arXiv 2108.09744; journal version *JSS* vol. 205, 2023, DOI 10.1016/j.jss.2023.111805) — 36 manually-validated real Qiskit bugs (Terra/Aer/Ignis/Aqua) with buggy+fixed code and reproducing tests, later extended to ~50–67 entries ("Bugs4Q-NA"). Public repo: github.com/Z-928/Bugs4Q. Described in a 2026 replication study as "a widely used dataset of real-world bugs in quantum programs."
2. **A 2026 ICSME Replication-Track paper (arXiv 2606.27124)** ran Bugs4Q across **21 Qiskit versions / 77,700 executions**, found bug reproducibility collapsed from 62.2% to 16.2% across versions, and released a patched fork ("Bugs4Q-Robust"). This is direct, existing evidence of cross-Qiskit-version regression study using a bug corpus — a close cousin of the proposed idea's evaluation methodology.
3. **QBugs** (arXiv 2103.16968) — algorithmic (not ecosystem) bugs with reproducibility infrastructure, explicitly built to enable "fair and unbiased comparisons" of quantum debugging techniques.
4. **Mined dataset, arXiv 2512.24656** (Yousuf & Sofi, Jan 2026) — 32,296 verified bug reports from 123 repos (2012–2024) across Qiskit, Cirq, PennyLane, PyQuil, QuTiP, D-Wave Ocean. Not yet released as a standardized artifact at time of check ("will be made available upon publication").
5. **QBugLM** (arXiv 2606.07314, June 2026) — agentic bug-injection benchmark for OpenQASM 3.0, framework-agnostic.

**Conclusion:** no single corpus is the de facto standard, and none is packaged as a ready-to-use pytest/CI fixture — but real, citable, actively-studied bug corpora exist, at least one is explicitly "widely used," and one (arXiv 2606.27124) already performs cross-Qiskit-version regression analysis using a bug corpus. The claim "there is no dedicated bug corpus for quantum SDK regression testing" is FALSE as stated; the narrowest defensible version is "no corpus is packaged as a ready-to-use pytest/CI fixture for cross-SDK-version regression testing."

---

## State-Aware / Autonomous Quantum Testing Tooling (Claim C12)

**Status: NOT FOUND AFTER SEARCH** (absence-of-evidence, not proof of non-existence — flagged explicitly rather than treated as a confirmed gap).

- Generic (non-quantum) "autonomous AI testing agent" products exist abundantly in classical software QA (e.g. Lyzr, Autify, TestCollab) — no quantum angle.
- Closest quantum-specific agentic system: **QBugLM** (arXiv 2606.07314) — genuinely agentic/multi-agent and quantum-specific, but explicitly framework-agnostic OpenQASM benchmarking, with no CI/CD integration, no cross-SDK-version regression detection, and no demonstrated state-awareness.
- A direct search for "autonomous agent quantum software testing CI/CD state-aware regression" returned no quantum-specific results beyond generic classical-QA agent products.

**Conclusion:** the compound claim's individual pieces exist separately (agentic quantum bug tooling; generic autonomous CI/CD testing agents for classical software) but no source combines quantum-specificity + state-awareness + autonomy + CI/CD + cross-version regression detection as a single system. This is a defensible gap by absence of evidence after a reasonably broad search, not a proven non-existence claim.
