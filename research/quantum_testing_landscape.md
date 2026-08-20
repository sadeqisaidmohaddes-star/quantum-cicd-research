# Quantum Software Testing/Debugging Landscape (Claims C03, C12; cross-refs C01/C02/C07/C11)

## Debugging / tracing / assertion-based tools (C03)

See `prior_art.md` for the full table. Summary: "Q-Trace" as a named tool is **FALSE/NOT FOUND** — no such quantum-specific tool exists under that name; it is most plausibly a confusion with **TraceQ** (surface-code trace analysis) or **MQT Debugger**. Real systems verified (QMon, TraceQ, Microsoft QDK Trace Simulator, CUDA-Q Statistical Assertions, Proq, Bloq/AutoBloq, MorphQ) all operate at the **single-circuit, single-run fault-localization or monitoring level**. None perform cross-SDK-version regression comparison; none integrate with pytest or GitHub Actions.

## State-aware / autonomous quantum testing tooling (C12)

**Status: NOT FOUND AFTER SEARCH** — treated as absence-of-evidence, not proof of non-existence.

- Generic (non-quantum) autonomous AI testing agents exist abundantly in classical software QA (Lyzr, Autify, TestCollab, etc.) — no quantum-specific angle found in any of them.
- The closest quantum-specific agentic system is **QBugLM** (arXiv:2606.07314) — genuinely agentic/multi-agent and quantum-specific, but explicitly framework-agnostic OpenQASM bug-injection benchmarking, with **no CI/CD integration, no cross-SDK-version regression detection, and no demonstrated state-awareness**.
- Direct searches combining "autonomous agent," "state-aware," "quantum software testing," and "CI/CD regression" returned no quantum-specific hits beyond generic classical-QA products.

**Conclusion:** the individual pieces of this compound claim exist separately (quantum-specific agentic bug tooling; generic autonomous CI/CD testing agents for classical software), but no verified source combines quantum-specificity + state-awareness + autonomy + CI/CD + cross-version regression detection into one system. This is the most genuinely open sub-claim of the entire research phase — but it is also the narrowest and least load-bearing part of the original idea, and should not be oversold as "the gap" on its own; see `gap_analysis.md`.

## Cross-references
- MQT QCEC / MQT Debugger: see `prior_art.md` (C01/C02) — solve equivalence-checking and single-run assertion debugging respectively, not CI/CD orchestration.
- QUTest: see `papers.md` (C05/C06) — already solves cross-Qiskit-version regression testing with CI-compatible output, the single most important prior-art find of this research phase.
- Bugs4Q / Bugs4Q-Robust: see `bug_corpora.md` (C07) — existing bug corpus already used in a cross-Qiskit-version reproducibility study.
