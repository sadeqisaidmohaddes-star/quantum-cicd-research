# Bug/Fault Corpora for Quantum Software (Claim C07)

**Status: EXISTS_NOT_STANDARDIZED.** The claim "there is no dedicated standard bug corpus for quantum SDK versions / quantum software regression testing" is **FALSE as literally stated** — real, citable, actively-studied corpora exist. The narrowest defensible version of the claim is: "no corpus is packaged as a ready-to-use pytest/CI fixture for cross-SDK-version regression testing."

Search covered 6+ distinct queries plus follow-on primary-source fetches (see `research_log.md`), specifically to avoid the "not found quickly ⇒ doesn't exist" trap.

## Verified corpora

### 1. Bugs4Q — the most established corpus found
- **Primary source:** arXiv:2108.09744 (Zhao et al., presented ASE 2021 New Ideas track); journal version in *Journal of Systems and Software*, vol. 205 (2023), DOI 10.1016/j.jss.2023.111805.
- **Content:** the arXiv preprint (2108.09744, 2021) describes 36 manually-validated real Qiskit bugs (spanning Terra/Aer/Ignis/Aqua modules), each with buggy code, fixed code, and reproducing tests. **Correction from verification pass 2 (2026-08-20):** the published JSS 2023 version (independently confirmed via ACM DL listing, not just the repo's citation block) describes the benchmark as **42 real, manually-validated Qiskit bugs mined from GitHub, StackOverflow, and Stack Exchange** — the count grew between the 2021 preprint and the 2023 journal version. The earlier "~50–67 entries under Bugs4Q-NA" figure could not be re-confirmed in this pass and should be treated as UNVERIFIED until opened directly; cite 36 (preprint) or 42 (JSS 2023, the more authoritative published count) instead.
- **Repository:** github.com/Z-928/Bugs4Q (public); an alternate repo name `Bugs4Q-Framework` also appears in secondary listings — not independently distinguished from the primary repo in this pass.
- **Standing:** a 2026 replication study (see #2 below) describes it as "a widely used dataset of real-world bugs in quantum programs."

### 2. Cross-version regression study built directly on Bugs4Q — highly material
- **Primary source:** arXiv:2606.27124 (Ohto, Ishimoto, Matsumoto, Kusumoto), accepted ICSME 2026 Replication Track.
- **What it did:** Ran the Bugs4Q corpus across **21 Qiskit versions, 77,700 total executions**. Found bug reproducibility collapsed from **62.2% to 16.2%** across versions — direct empirical evidence that quantum SDK version drift breaks existing bug reproductions/tests.
- **Artifact released:** a patched fork, "Bugs4Q-Robust," addressing version-sensitivity issues in the original corpus.
- **Relevance:** this is existing academic evidence that (a) cross-Qiskit-version regression behavior is real and measurable, and (b) at least one research group has already built and published a cross-version execution harness over a bug corpus — closely adjacent to, though not identical to, the proposed CI/CD infrastructure (this was a research study, not a reusable pytest/GitHub Actions product).

### 3. QBugs
- **Primary source:** arXiv:2103.16968.
- **Content:** algorithmic (not ecosystem-level) bugs, with reproducibility infrastructure explicitly built to enable "fair and unbiased comparisons" of quantum debugging techniques — i.e., an earlier attempt at exactly the kind of standardization the original claim assumed doesn't exist.

### 4. Large mined bug-report dataset
- **Primary source:** arXiv:2512.24656 (Yousuf & Sofi, Jan 2026).
- **Content:** 32,296 verified bug reports mined from 123 repositories (2012–2024) spanning Qiskit, Cirq, PennyLane, PyQuil, QuTiP, and D-Wave Ocean.
- **Status:** at time of check, described as "will be made available upon publication" — i.e., mined/classified data, not yet a released, curated benchmark artifact. A companion 4,984-issue / 36-repo Qiskit-ecosystem benchmark was mentioned in search results but not independently opened — flagged UNVERIFIED, do not cite without direct confirmation.

### 5. QBugLM
- **Primary source:** arXiv:2606.07314 (June 2026).
- **Content:** an agentic bug-injection benchmark for OpenQASM 3.0, framework-agnostic (not tied to a single SDK's real bug history).

### 6. Qolumbina (cross-referenced from papers.md)
- **Primary source:** arXiv:2607.02029.
- **Content:** 40 curated open-source quantum programs as a QST evaluation benchmark. Not a bug corpus per se (no labeled faults) — a program benchmark suite.

## Conclusion

No single corpus functions as *the* de facto standard the way, e.g., Defects4J does for Java. But the field is not a blank slate: Bugs4Q is real, public, and "widely used" per independent replication work; and arXiv:2606.27124 already demonstrates the exact failure mode (cross-Qiskit-version reproducibility collapse) that motivates the proposed research, using that corpus as its substrate. Any thesis/product framing claiming "no corpus exists" must be corrected. The defensible framing is: **existing corpora are not packaged as ready-to-use, CI-native (pytest/GitHub Actions) regression fixtures — that packaging/tooling layer is the open gap, not the underlying bug data.**
