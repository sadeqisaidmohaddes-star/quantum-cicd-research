# Quantum CI/CD Landscape (Claims C08–C11, cross-refs C05/C06)

Summary view — see `repositories.md` for full inspection detail and `papers.md` for the QUTest paper.

## What exists today, layered

1. **SDK-internal version-matrix CI (CONFIRMED, C09):** Qiskit's official ecosystem CI template (`test_latest_versions.yml`, `test_development_versions.yml`, `test_minimum_versions.yml`, reused across ~8 Qiskit-ecosystem repos) already runs a project's existing test suite against latest/dev/minimum Qiskit versions in GitHub Actions. It is real, in active use, and reusable across Qiskit-based projects. **What it does NOT do:** diff behavior between versions or detect equivalence-level regressions — it only checks pass/fail of whatever tests already exist.

2. **Narrow serialization-format regression testing (CONFIRMED, C09):** Qiskit core's own `qpy.yml` / `qpy_compat` harness performs genuine cross-version regression testing, but only for QPY circuit serialization compatibility, and it's internal to the Qiskit repo (not externally reusable tooling).

3. **A published cross-Qiskit-version regression-testing tool with CI-compatible output (PARTIALLY CONTRADICTS the gap, C05/C06 — see `papers.md`):** **QUTest** (arXiv:2605.19736, May 2026) runs the same OpenQASM 3 test across multiple isolated Qiskit versions and emits JUnit/xUnit XML for Jenkins/GitHub Actions/GitLab CI. Not pytest-native; Qiskit-only; assertions are hand-written (no automated equivalence/regression detection algorithm).

4. **A research pilot on transpiler regression detection (PARTIALLY CONFIRMED, C10):** `quantum-transpiler-regression-testing` ("cart", Zenodo DOI 10.5281/zenodo.21020113, June 2026) found that ~38% of real Qiskit transpiler bug-fixes are regressions invisible to black-box equivalence oracles — direct evidence that equivalence checking (the QCEC layer) alone is insufficient. Single-SDK, CLI-based, not packaged as a pytest plugin or GitHub Action, brand new (0 stars, single small-institution team).

5. **Immature pytest plugins (PARTIALLY CONFIRMED, C08):** `pytest-quantum`, `qtest-quantum`, `qc-assert` — real, installable, but each does framework-to-framework (not version-to-version) equivalence checking or single-run assertions only; none execute across multiple installed SDK versions and diff results automatically. All are very young, single-maintainer, 0–2 stars.

6. **No cross-SDK (Qiskit vs Cirq vs PennyLane) regression/equivalence tool found anywhere (C10/C11).** Every cross-version or regression-testing artifact found is single-SDK (Qiskit-only).

## What this means for the proposed idea

The **narrow, defensible remaining gap** is the intersection of:
- pytest-native (not a bespoke CLI or non-Python test runner)
- cross-**SDK** (not just cross-version-within-Qiskit)
- automated regression/equivalence detection (not hand-written assertions)
- packaged as reusable, drop-in GitHub Actions tooling for arbitrary user projects (not internal-only CI for one SDK's own repo)

No single existing system combines all four. QUTest solves cross-version + CI-output but not pytest-native or cross-SDK. Qiskit's own template solves reusable GitHub Actions version-matrix CI but not regression *detection* (just pass/fail of existing tests) and is single-SDK. `pytest-quantum` solves pytest-native + cross-**framework** equivalence but not cross-**version** automated regression detection. See `gap_analysis.md` for the full synthesis and narrowed thesis framing.
