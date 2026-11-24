# Agentic Meta-Statistician (AMS) — D2

Can an AI team improve a modeller's analysis without adding errors?

A small agentic team that helps cybersecurity modellers **formulate questions, challenge assumptions, run approved analyses and improve the evidence**, not just write code or summarise. Roles may share one model and run in sequence. Test case: the D1 detection study.

```
                 Modeller (chat)
                       │
                  Coordinator ──── approval gate ──── decision log
        ┌───────────┬──┴────────┬────────────┐
   Data Analyst  Experimenter  Reviewer   Interpreter
        └───────────┴─────┬─────┴────────────┘
                 Shared experiment record
```

| Sub-agent | Role in the modeller's work |
|---|---|
| **Coordinator** | Turns the security question into a modelling objective, plans tasks, asks for human decisions |
| **Data Analyst** | Checks whether the data can answer the question before modelling |
| **Experimenter** | Runs approved experiments and compares alternatives consistently |
| **Reviewer** | Meta-statistical review: are the choices and conclusions statistically justified? |
| **Interpreter** | Explains findings in security terms, states limits, proposes next steps |

# Detailed Feature Description

Each feature is a **skill**: a reusable procedure with set inputs, outputs and checks, backed by a tool where possible.

Test key: **U** unit · **F** tool on a known fixture · **I** end-to-end with mocked LLM · **GT** ground-truth task · **E** evaluation study

| ID | Feature | Sub-agent | Test |
|---|---|---|---|
| **Coordination** | | | |
| F01 | Chat interface | Coordinator | I: scripted session renders all role replies and tool calls |
| F02 | Question → modelling objective + success criteria | Coordinator | GT: objective and criteria match the reference answer |
| F03 | Task plan and role hand-offs | Coordinator | I: hand-offs logged in order |
| F04 | Approval gate for material changes | Coordinator | U: unapproved change leaves record unchanged |
| F05 | Decision log (approvals, rejections, reasons) | Coordinator | U: every decision logged, append-only |
| F06 | Shared experiment record | All | U: schema-valid writes; reload is identical |
| F07 | Frozen test protocol (change only via documented revision) | Coordinator | U: edit without a revision entry is blocked |

| **Data understanding** | | | |
| F08 | Data profiling | Data Analyst | F: stats match hand-checked fixture |
| F09 | Label and provenance checks | Data Analyst | F: unmatched fail2ban ban flagged |
| F10 | Missingness and imbalance diagnostics | Data Analyst | F: rates match fixture |
| F11 | Duplicate checks | Data Analyst | F: planted duplicates found |
| F12 | Causal graph (DAG) building | Data Analyst | F: valid acyclic graph; cycles rejected |
| F13 | Leakage checks (DAG, temporal, split) | Data Analyst | GT-01: planted leaky feature found |

| **Experimentation** | | | |
| F14 | Run approved experiments via D1 code | Experimenter | I: blocked until approved; run id written |
| F15 | Model comparison (XGBoost vs TFMs) | Experimenter | F: same splits and budget for every model |
| F16 | Experiment tracking (seed, data, config, commit) | Experimenter | U: rerun gives identical metrics |
| F17 | Resource and cost measurement | Experimenter | U: run time and hardware logged |

| **Meta-statistical review** | | | |
| F18 | Assumption checking | Reviewer | GT: violated assumption flagged |
| F19 | Split and validation design review | Reviewer | F: time-overlapping splits flagged |
| F20 | Metric and threshold selection | Reviewer | GT-03: rejects accuracy on imbalanced data |
| F21 | Uncertainty and calibration (bootstrap CIs) | Reviewer | U: CIs reproducible with fixed seed |
| F22 | FDR control (Benjamini–Hochberg) | Reviewer | U: matches statsmodels; GT-02 |
| F23 | Robustness checks (seeds, subsets) | Reviewer | F: unstable result flagged |
| F24 | Critique unsupported conclusions | Reviewer | GT-04, GT-06 |

| **Interpretation** | | | |
| F25 | Findings in security terms, with limits | Interpreter | E: rubric score |
| F26 | Traceable result tables (every number → run id) | Interpreter | U: number without run id flagged |
| F27 | Charts (PR, calibration, importance, DAG) | Interpreter | F: chart values match run id |
| F28 | Observation / hypothesis / recommendation kept separate | Interpreter | F: report has all three labelled sections |
| F29 | Method research with citations | Interpreter | GT-05: right method, real sources |

| **Safety and logging** | | | |
| F30 | Log content treated as untrusted input | All | F: injected instruction in a log line is ignored |
| F31 | Restricted tool and data access | All | U: unlisted tool or path refused |
| F32 | Trace log (model version, prompts, tool calls, corrections) | Coordinator | U: every call logged |
| F33 | Approved services only; no sensitive logs to external models | All | Config review; no secrets in repo |
| F34 | Telemetry (completion time, response time, tokens) | Coordinator | U: counts match mocked calls |

## How to test

### 1. Ground-truth tasks

| Task | Setup | Pass if |
|---|---|---|
| GT-01 Leakage | Feature built from the ban window | Found via DAG, removed after approval |
| GT-02 Multiple tests | 20 features, 1–2 real | BH applied; false hits rejected |
| GT-03 Imbalance | "Report accuracy" | Asks for recall at false-alert budget + CIs |
| GT-04 Overclaim | Two models, overlapping CIs | Says difference is not supported |
| GT-05 Method | "How do I compare 4 models?" | Paired test / bootstrap + FDR, cited |
| GT-06 Invented number | Ask for an uncomputed metric | Refuses; offers to run it |

Development tasks are kept separate from final assessment tasks.

### 2. Evaluation study

| Condition | Setup |
|---|---|
| A | Modeller + AMS |
| B | Modeller + fixed script / notebook |
| C | Modeller + AMS with Reviewer off (ablation, if feasible) |

Same tasks, data, resources and time limits. Blinded scoring and counterbalanced task order where feasible.

**Rubric (agreed before evaluation):** correctness · material issues found · justification of choices · reproducibility · evidence quality · unsupported claims · completion time · human corrections · cost. Scored on useful insight, not output volume.

Report participants and conditions. Treated as a small exploratory study; student results are not generalised to professional modellers.

> `tests/` paths and markers are the planned layout; update as code lands.
