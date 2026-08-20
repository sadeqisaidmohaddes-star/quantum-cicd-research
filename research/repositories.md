# Repositories Inspected — Pytest Plugins, CI Products, Regression Tooling (Claims C08–C11)

All entries below were inspected directly (README, workflow YAML, PyPI release history) via `gh api`/`gh search` and WebFetch — not from search snippets.

---

## C08 — Quantum pytest plugins: PARTIALLY CONFIRMED (real plugins exist; none do cross-SDK-version regression detection)

| Project | Repo | PyPI | Stars | Created/Updated | Discovers tests | Multi-SDK-version execution | Result comparison | Regression detection | GitHub Actions | Machine-readable output |
|---|---|---|---|---|---|---|---|---|---|---|
| `pytest-quantum` | github.com/qbench/pytest-quantum | v1.0.0 (6 releases) | 2 | created 2026-03-21, pushed 2026-05-12 | YES | NO — CI matrix is Python 3.11–3.13 × OS only | PARTIAL — `assert_cross_platform_equivalent`, `assert_qiskit_cirq_equivalent`, `assert_qiskit_pytket_equivalent` compare across **frameworks**, not across **versions of one SDK** | PARTIAL — manual assertions only, no automatic version-diffing | YES (own CI) | UNKNOWN — no evidence of structured JSON/JUnit regression report |
| `qtest` / `qtest-quantum` | github.com/metin-5115/qtest | v0.1.0 only | 0 | created 2026-05-21, pushed 2026-06-18 | YES | NO — CI matrix is Python 3.9–3.12 × OS only | PARTIAL — `assert_circuit_equivalent` (single-SDK process fidelity), no cross-SDK/version diffing | PARTIAL — cost-regression assertions (e.g. `assert_max_two_qubit_count`), single run only | YES | UNKNOWN |
| `qc-assert` | github.com/JMORAF87/qc-assert | not on PyPI | 0 | created/pushed 2025-12-31/2026-01-01 | YES (minimal) | NO — single Python 3.11 job | NO | Stated intent ("catch regressions when SDK upgrades change behavior") but not implemented | YES (basic) | NO |

Also found on PyPI simple-index: `quantum-test`, `quantum-tests` — both empty/squatted placeholder packages (v0.0.0, no summary). Not relevant.

**Assessment:** all three real plugins are very young (created within ~9 months of the Aug 2026 check date), single-maintainer, 0–2 GitHub stars — not established/adopted infrastructure. None execute the same test suite against multiple *installed versions* of a quantum SDK and automatically diff results to flag a regression; they are single-run assertion libraries with framework-to-framework (not version-to-version) equivalence helpers. **This is a real but immature and narrow prior-art cluster, not a solved problem.**

---

## C09 — GitHub Actions + quantum CI products: CONFIRMED (exists as official SDK-ecosystem internal CI templates, not a third-party product)

**Qiskit's official addon-repository CI template**, found in [Qiskit/qiskit-addon-cutting](https://github.com/Qiskit/qiskit-addon-cutting) and reused verbatim across Qiskit/qiskit-ibm-catalog, qiskit-community/qiskit-pasqal-provider, Gopal-Dahale/qiskit-qulacs, xthecapx/qiskit-qward, eggerdj/restless-simulator. Verified via `.github/workflows/README.md` and raw YAML:
- `test_latest_versions.yml` — runs the test suite against the latest released Qiskit, daily + on every push.
- `test_development_versions.yml` — installs **dev/unreleased** Qiskit and qiskit-ibm-runtime from `git+https://github.com/Qiskit/qiskit.git` (using the real PyPI tool `extremal-python-dependencies`), to catch breaking changes *before* a Qiskit release. Runs daily.
- `test_minimum_versions.yml` — pins every dependency to its declared minimum version and re-runs tests, verifying `pyproject.toml` lower bounds.

Explicitly documented as "designed to work out of the box for any research software prototype, especially those based on Qiskit" — a **reusable internal CI pattern for the Qiskit ecosystem**. It asserts pass/fail of the existing test suite at each version tier; it does **not** diff behavior between versions or detect equivalence-level regressions.

**Qiskit core's own QPY backward-compatibility workflow** ([Qiskit/qiskit `.github/workflows/qpy.yml`](https://github.com/Qiskit/qiskit/blob/main/.github/workflows/qpy.yml), calling `test/qpy_compat/run_tests.sh`) — genuine cross-version regression testing: circuits serialized by older Qiskit versions are deserialized and checked against newer versions. Narrowly scoped to the QPY serialization format, lives inside the Qiskit repo itself, not packaged as reusable external tooling.

**Noise filtered out:** most "quantum" + "GitHub Action" search hits (pqc-scan, KyberCheck, pqc-guard-action, quantum-estimate-action, maknoon-action) are **post-quantum cryptography (PQC) migration scanners** — an unrelated field sharing the "quantum" keyword.

---

## C10 — Cross-SDK/cross-version regression testing as reusable open tooling: PARTIALLY CONFIRMED — closest prior art found, but narrow/immature

**Most significant find of the entire research phase alongside QUTest: [furqan-nr/quantum-transpiler-regression-testing](https://github.com/furqan-nr/quantum-transpiler-regression-testing)** ("cart" — cost-aware regression testing).

Verified via README **and** independent Zenodo DOI resolution (not just the repo's self-description):
- Zenodo record confirmed real: **"Leakage-Safe Evaluation of Quantum Transpiler Regression Testing (cart)"**, DOI `10.5281/zenodo.21020113`, authors Furqan Nasir, Arif Shah, Iftikhar Alam (City University of Science and Information Technology, Peshawar, Pakistan), published 2026-06-29, MIT-licensed open-source software artifact.
- README states the accompanying paper is "submitted to Quantum Information Processing, Quantum Software Engineering collection" — submission only, **acceptance not independently verified**.
- Headline finding: across 26 merged Qiskit transpiler bug-fixes, ~38% (10/26) are regressions **invisible to black-box output-equivalence oracles** — i.e., direct evidence that equivalence-checking alone (the QCEC layer) is insufficient for catching real-world SDK regressions, which is directly relevant to motivating a broader regression-testing approach.
- Scope: single-SDK (Qiskit transpiler only), not cross-SDK. Ships as Python CLI + scripts, **not** a pytest plugin or GitHub Action others can drop in.
- Maturity: repo created 2026-06-28 (brand new), 0 stars, single small-institution author group.

**This should be treated as directly relevant, possibly competing/complementary prior art — do not omit from any novelty argument.** No other reusable, installable, cross-SDK or cross-version quantum regression/equivalence tool was found; searches for "quantum SDK version compatibility", "cross-version quantum", "OpenQASM regression" returned zero results beyond the items documented here and in `papers.md` (QUTest).

---

## C11 — Other equivalence/regression tools beyond MQT QCEC: NOT FOUND (beyond items above)

No other academic or industry (IBM/Google/Xanadu/Quantinuum) open-source equivalence checker with CI integration was found via repository search. "Quantum equivalence checking" repo search returned only unrelated SAT-solver student projects (e.g. `n26124939/Quentangle-SAT`, 0 stars — content not verified as legitimate/functional, flagged UNKNOWN not CONFIRMED).

---

## Search log (gh CLI / GitHub code & repo search, WebFetch)

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
| `gh search repos "quantum" "github action"` | ~18 hits, nearly all post-quantum-cryptography tools (different field), filtered out |
| `gh search repos "quantum transpiler regression"` | 1 hit: furqan-nr/quantum-transpiler-regression-testing |
| `gh search repos "openqasm regression"` | 0 results |
| `gh api repos/furqan-nr/quantum-transpiler-regression-testing` + readme | Confirmed real; 0 stars, created 2026-06-28 |
| `WebFetch https://doi.org/10.5281/zenodo.21020113` | Independently confirmed real Zenodo software record, authors, institution, date |
| `gh search repos topic:quantum-computing "ci"` | Returned established SDKs/libraries (e.g. Cirq), none matching a CI-testing-product description |
