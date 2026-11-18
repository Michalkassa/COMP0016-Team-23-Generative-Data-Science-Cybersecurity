# COMP0016 Project Specification

## Document Details

| Field | Value |
|-------|-------|
| Version number and date of this document | Version 0.2 18th of November 2026|
| Team No. | 23 |
| Working Project Title | Generative Data Science for Cybersecurity |
| Project GitHub Repo URL | https://github.com/Michalkassa/COMP0016-Team-23-Generative-Data-Science-Cybersecurity |
| Academic Supervisor Name | Graham Roberts |
| TA Name | Wonduk Seo |

## Team

| Name | Email | Role |
|------|-------|------|
| Victor Mauger | victor.mauger.25@ucl.ac.uk | |
| Zixi Wang| zczqz34@ucl.ac.uk | |
| Michal Kassa| michal.kassa.25@ucl.ac.uk| |
| Akshat Rai| akshat.rai.25@ucl.ac.uk| |
| Yulin Ding| yulin.ding.25@ucl.ac.uk| |
## Partner Organisation

| Name | Industry |
|-------|-------|
| Avenade | Cybersecurity Consulting |


### Overview of Partner Organisation

Avanade is a global professional services company providing IT consulting and services focused on the Microsoft platform with artificial intelligence, business analytics, cloud, application services, digital transformation, modern workplace, security services, technology and managed services offerings

### Partner Contacts

| Contact Name | Job Title | Email | Phone Number |
|--------------|-----------|-------|--------------|
| Eli Kling | Enterpise AI Capability Lead | eli.kling@avanade.com |  +44 (0) 777 540 67 56 |

### Communication and Meetings

> How often the team meets the partner, through which channel (e.g., Teams, email, Slack), and who the main contact is on each side.

Meeting Once per week using Teams by booking "book-with-me" time slots with the partner. Time slots are decided in the group using whatsapp and during lab sessions on tuesday. The team is main contact on most meetings, using the book-with-me system and Emails to the client. 

## Project Description

> Summarise the project background and the problem(s) to be solved. Please list the key outcomes and deliverables that might be expected (e.g., a proof-of-concept design and implementation of software).

### Background

A data scientist's job has always been the same: collect, clean, analyse and model data. New tools are adopted along the way (for example XGBoost), but generative AI tools are now arriving very quickly. The claims around them are loud and the evidence for how well they work in specific data science applications is thin. For Avanade and its data scientists, the question is: **what actually works, where, and how?**

### Problem

The project measures how effective generative AI is in two strands, using anomaly detection on real cybersecurity (web-server) logs as the test case:

1. **AI as the model (Strand 1).** Do Tabular Foundation Models (TFMs) detect malicious log activity better than an established method (XGBoost)?
2. **AI as the assistant (Strand 2).** Can a team of AI agents (a "Meta-Statistician") help a cybersecurity modeller through the modelling lifecycle, under human oversight, without adding errors?

The findings feed a report and an executive pitch that recommends whether Avanade should build an accelerator offering around these tools.

### Key Outcomes and Deliverables

| ID | Deliverable | Format |
|----|-------------|--------|
| D1 | Tabular Foundation Model Benchmark Code | GitHub repository |
| D2 | Meta-Statistician agent team | Working prototype (hosted on Azure as a stretch goal) |
| D3 | Generative Data Science Report | Written report |
| D4 | Executive pitch for a proposed accelerator | Short slide deck and talk |

- **D1:** a reproducible benchmark of XGBoost against three TFMs (TabPFN, TabICL and a third model, TabDPT or Mitra; see [Any Other Information](#any-other-information)) on anonymised, labelled web-server attack logs.
- **D2:** a coordinated set of AI roles (Coordinator, Data Analyst, Experimenter, Reviewer, Interpreter), reusable skills and analytical tools, used through a chat interface. Deploying it on Azure is a stretch goal (S8).
- **D3:** a literature and evidence review, the benchmark and agent results, and recommendations for Avanade.
- **D4:** a short business-facing pitch with a value proposition, evidence, costs and risks, and a recommendation to proceed, revise or stop.

## Timeline and Milestones

> Key dates, interim deliverables and partner demo points.

A runnable build is demoed to the client every two weeks (git tag `build-YYYY-MM-DD`). A progress video goes to the supervisor every month.

| When | Milestone | Graded |
|------|-----------|--------|
| 27 Oct 2026 | Client introduction, initial ideas and requirements | |
| Before 9 Nov 2026 | Requirements emailed to the client and approved (approval email logged) | |
| 9 Nov 2026 16:00 | Video presenting the agreed requirements | |
| Nov 2026 | Requirements and design submitted (this document) | 5% |
| Nov–Dec 2026 | Data preparation, XGBoost baseline, first TFM, agent team v1 → **Prototype 1** | |
| Jan 2027 (term 2, week 1) | Prototype 1 demoed to the client | |
| 22 Jan 2027 | Elevator pitch | 5% |
| Jan–Feb 2027 | Full benchmark (D1), agent evaluation (D2), Azure deployment if time permits (S8) → **Prototype 2**; IP and GDPR review | |
| Feb–Mar 2027 | Report (D3) and executive pitch (D4) drafted and reviewed with the client | |
| 12 Mar 2027 | Development stops; testing, deployment and hand-over materials | |
| 16 Mar 2027 | Showcase | |
| 20 Mar 2027 | Website report finished; client hand-over | |
| 24 Mar 2027 16:00 | Website report and system artefacts submitted | 40% + 50% |

## Detailed Requirements

> List the requirements (must have, should have) that you will be working on and that should be met to make the project a success.

### D1: Tabular Foundation Model Benchmark

| ID | Requirement | Priority |
|----|-------------|----------|
| R1.1 | Fix one dataset and one detection task, and check data quality and leakage with a simple Causal Directed Graph (DAG) | Must |
| R1.2 | Parse the raw web-server logs and build clearly named features per visitor (`ip_id`) and time window | Must |
| R1.3 | Split the data into training, validation and test sets (time-based where possible), fixed before any model sees the test set | Must |
| R1.4 | Set the decision threshold on validation data at an agreed false-alert budget | Must |
| R1.5 | Train and configure XGBoost and the three TFMs under the same features, splits and a fixed compute budget | Must |
| R1.6 | Report detection accuracy, sensitivity and recall at the fixed false-alert budget for every model | Must |
| R1.7 | Report confidence intervals, calibration and feature importance for every model | Must |
| R1.8 | Make the benchmark reproducible from the repository (pinned dependencies, fixed seeds, one documented run command) | Should |
| R1.9 | Record compute cost (run time and hardware) per model | Should |

### D2: Meta-Statistician Agent Team

| ID | Requirement | Priority |
|----|-------------|----------|
| R2.1 | Implement five roles: Coordinator, Data Analyst, Experimenter, Reviewer and Interpreter | Must |
| R2.2 | Agents run real analysis tools (not just text generation) and share one experiment record | Must |
| R2.3 | Check that modelling choices are statistically justified, using Causal Directed Graphs and False Discovery Rate control | Must |
| R2.4 | Keep a human in the loop: the modeller approves changes, and approvals are logged | Must |
| R2.5 | Provide a chat interface through which the modeller works with the team | Must |
| R2.6 | Test the team on a small set of ground-truth tasks | Must |
| R2.7 | Assess effectiveness qualitatively with a fixed, structured protocol, and report concrete episodes | Must |
| R2.8 | Report performance insights: task completion time, response time and token usage | Must |

### D3: Generative Data Science Report

| ID | Requirement | Priority |
|----|-------------|----------|
| R3.1 | Literature and evidence review of generative data science approaches compared with established methods | Must |
| R3.2 | Review of current cybersecurity analytics approaches | Must |
| R3.3 | Description of the datasets used, including label limitations | Must |
| R3.4 | Benchmark results for the TFMs (from D1) | Must |
| R3.5 | Results from tests with the Meta-Statistician (from D2) | Must |
| R3.6 | Discussion of where the new technology adds value in cybersecurity anomaly detection and where classical approaches remain the better choice | Must |
| R3.7 | Limitations of the results and recommendations for Avanade | Must |

### D4: Executive Pitch for a Proposed Accelerator

| ID | Requirement | Priority |
|----|-------------|----------|
| R4.1 | A shorter review of the findings aimed at business stakeholders | Must |
| R4.2 | A short pitch proposing an accelerator package with a defined value proposition | Must |
| R4.3 | Evidence of benefits and limitations for modellers and analysts | Must |
| R4.4 | Proposed reusable components and service offering | Must |
| R4.5 | Costs, risks and a recommendation to proceed, revise or stop | Must |

## Stretch Requirements

> Additional requirements if time permits.

| ID | Stretch requirement |
|----|---------------------|
| S1 | Add further baselines to the benchmark: logistic regression, random forest, and unsupervised detectors (Isolation Forest, Local Outlier Factor, robust z-score / EWMA on request rate) |
| S2 | Compare point-anomaly detection on single requests with collective anomaly detection on sliding windows per visitor |
| S3 | Manually review a held-out set of traffic that the models flag but fail2ban did not, to look for attacks the rule-based labels miss |
| S4 | Use the SSH brute-force labels as a separate mini-dataset |
| S5 | Compare the agent-assisted workflow with a plain-script workflow on the same task, scored with an agreed rubric |
| S6 | Run the agent team on Microsoft Fabric as well as Azure |
| S7 | Repeat the benchmark on a second cybersecurity dataset to test whether the results generalise |
| S8 | Deploy the agent team (D2) as a hosted service on Azure |

## Target Users and Stakeholders

> Who will actually use the system (the partner's staff, customers, the public). Requirements, testing and ethics decisions all depend on this.

| Stakeholder | Interest |
|-------------|----------|
| **Avanade data scientists and cybersecurity modellers** | Primary users. They run the benchmark (D1) and use the agent team (D2) in their modelling work |
| **Avanade security analysts** | Consumers of detection results; care about recall at a tolerable false-alert rate |
| **Avanade business and practice leads** | Audience for the executive pitch (D4); decide whether to fund an accelerator |
| **Eli Kling (Enterprise AI Capability Lead, Avanade)** | Client and main partner contact; approves requirements and judges acceptance |
| **Avanade clients (indirect)** | Would receive any future accelerator offering; not users of this project's system |
| **UCL supervisor and TA** | Assess the project |

The system is an internal proof of concept for technical staff. It is not intended for the public.

## Out of Scope

> What the project will *not* deliver, to stop scope creep.

- A production-ready intrusion detection system, or real-time detection on live traffic.
- Integration with Avanade's or any customer's security tooling (SIEM, SOC platforms).
- Training or fine-tuning new foundation models. Pretrained TFMs are used as provided.
- Collecting new data or labelling it by hand at scale. The project uses the supplied, already labelled logs.
- Re-identifying anyone, or reversing the dataset's anonymisation.
- A polished end-user product: the chat interface is a working prototype, not a supported application.
- Building the accelerator itself. D4 proposes it; it is not implemented.

## Existing Systems and Integration

> Any existing codebase, APIs, databases or platforms the project must work with, and whether or when the team will get access to them.

- **Client brief and research wiki:** [elikling/ucl-cybersecurity-ml](https://github.com/elikling/ucl-cybersecurity-ml), provided by Avanade. The team has access.
- **Dataset:** the anonymised Wendover web-server logs (see [Data](#data)), already supplied.
- **Azure (Azure OpenAI and hosting):** LLM provider for D2, and hosting platform if the stretch deployment (S8) goes ahead. Environment variables are set up (`.env.example`); subscription access and funding are still to be confirmed with Avanade.
- **Tabular Foundation Models:** TabPFN, TabICL and TabDPT / Mitra, used through their published Python packages and weights.
- **Our repository:** Python 3.11+ (`pyproject.toml`), with GitHub Actions CI running `ruff` on every push and pull request.

There is no existing Avanade codebase that the project must integrate with.

## Constraints and Risks

> Identify any constraints on what can be done (e.g., time, technology, data access) and how risk can be mitigated (managed).

### Constraints

- **Time:** development stops on 12 Mar 2027. Five team members split between two strands alongside other modules.
- **Data:** one month of logs from a single small website. Labels come from fail2ban rules, not an independent ground truth. The data may not be shared outside the project.
- **Compute:** TFMs have limits on training-set size and run much faster on a GPU. All models get the same fixed compute budget.
- **Cost:** LLM calls and Azure hosting cost money; who pays has not yet been agreed.
- **Licensing:** TFM weights and libraries have their own licences, which must be checked before use and before any commercial reuse.

### Risks

| Risk | Likelihood / impact | Mitigation |
|------|---------------------|------------|
| Models only re-learn fail2ban's rules, so results look better than they are | High / High | Leakage check with a DAG (R1.1); per-visitor and time-window features; discuss in D3; manual review of disagreements (S3) |
| Severe class imbalance (about 1 in 10 visitors is an attacker, far fewer requests) distorts metrics | High / Medium | Report recall at a fixed false-alert budget, PR-based metrics and confidence intervals rather than accuracy alone |
| Dataset too large for TFM context limits | Medium / Medium | Aggregate to per-visitor / time-window rows; subsample the training set within the agreed budget |
| No Azure access or funding in time | Medium / High | Confirm with Avanade early; build D2 to run locally first so Azure is a deployment step, not a dependency |
| LLM agents produce wrong or unjustified analysis | High / High | Human approval of every change (R2.4); Reviewer role with statistical checks (R2.3); ground-truth tasks (R2.6) |
| A TFM licence forbids the intended use | Low / Medium | Check licences before use; swap to an alternative TFM |
| Accidental publication of the dataset or secrets | Low / High | Keep the repository private; never commit `.env`; review pull requests |
| Workload is uneven between the two strands | Medium / Medium | Biweekly work packages agreed with the TA; weekly contribution log |

## Acceptance Criteria

> How the partner will judge whether each requirement has been met. How will this be confirmed?

| Deliverable | Accepted when | Confirmed by |
|-------------|---------------|--------------|
| D1 | A clean checkout runs the benchmark end to end with one documented command, and produces, for XGBoost and all three TFMs, accuracy, sensitivity and recall at the fixed false-alert budget, with confidence intervals, calibration and feature importance (R1.1–R1.7) | Demo to the client at a biweekly build; the client or TA reruns it from the repository |
| D2 | All five roles work through the chat interface, run real tools, share one experiment record and require human approval; the team has been tested on the ground-truth tasks, with episodes and performance figures reported (R2.1–R2.8). Azure hosting is a stretch goal (S8) | Live demo to the client, on Azure if deployed |
| D3 | The report covers R3.1–R3.7, cites its sources, states uncertainty and limitations, and labels anything illustrative | Client reviews a draft and the final version |
| D4 | The slide deck and talk cover R4.1–R4.5 and end with a clear proceed / revise / stop recommendation | Presented to the client |

Requirements were approved by the client by email before 9 Nov 2026. Acceptance of each deliverable is confirmed by email from the client and recorded in [LOG.md](LOG.md#decisions).

## Software Testing and AI Evaluation

> What are the strategies for testing the software (unit, functional, integration, regression)? How will the output from AI be evaluated for correctness and accuracy?

### Software testing

- **Unit tests (pytest):** log parsing, feature engineering, label joining (request timestamp within `[ban_time, unban_time]` per `ip_id`), data splits and metric calculations, using small hand-checked fixtures.
- **Data checks:** dataset checksums against `SHA256SUMS`; schema, row count and missing-value checks after each pipeline step; tests that no test-set rows or future timestamps leak into training.
- **Functional tests:** each agent tool (profiling, leakage check, experiment run) called on a known input and its output checked.
- **Integration tests:** the full benchmark run on a small sample; an agent episode run end to end with a mocked LLM so it is fast and deterministic.
- **Regression tests:** benchmark metrics recorded per build; a change that moves the results beyond seed-to-seed variance must be explained.
- **CI:** GitHub Actions runs `ruff` now and will run `pytest` on every push and pull request. Every biweekly build must pass CI.

### AI evaluation

- **Tabular Foundation Models:** evaluated exactly like XGBoost. Same features, splits and compute budget; threshold and metrics frozen before the test set is used; bootstrap confidence intervals; calibration curves; feature importance; recall at the fixed false-alert budget.
- **Meta-Statistician agents:**
  - Run on a small set of ground-truth tasks with known correct answers (for example, a planted leakage feature, or a choice that needs FDR correction), and checked for whether the team gets them right.
  - A fixed, structured qualitative protocol, applied the same way to every episode, with concrete episodes (successes and failures) reported.
  - Performance metrics: task completion time, response time and token usage.
  - Every agent change is approved by a person and logged, so wrong suggestions are caught and counted.

## Technical and/or Mentor Support Availability

> Will technical support or a mentor be provided by the project partner? In particular, for more specialised domain or development knowledge.

Eli Kling (Enterprise AI Capability Lead, Avanade) is the main contact for domain and technical guidance, through regular Teams meetings and email. Avanade provides the project brief and a research wiki ([elikling/ucl-cybersecurity-ml](https://github.com/elikling/ucl-cybersecurity-ml)). Academic support comes from the supervisor (Graham Roberts) and the TA (Wonduk Seo), who meet the team weekly.

To confirm with Avanade: whether further Avanade specialists (cybersecurity, Azure) can be contacted when needed.

## Design and Technical Challenges

> Including web, mobile, wearable, architecture, data analysis, AI/ML, LLMs, graphics, VR/AR, security, algorithms, and anything else.

- **Data analysis and feature engineering:** turning raw Apache logs into per-visitor, per-time-window features (request rate, unique paths, 404 rate, status-code entropy, user-agent rarity, timing between requests) without leaking label information.
- **Label quality:** fail2ban labels mark rule thresholds, not true attacks. Some categories (SSH brute force, recidive) do not map to HTTP requests at all.
- **Class imbalance:** attacks are rare, especially per request, so accuracy alone is misleading.
- **Fair benchmarking:** TFMs have context-size limits and different hardware needs. All models must get comparable features, splits and compute.
- **Statistical rigour:** using Causal Directed Graphs to reason about leakage, and False Discovery Rate control when many comparisons are made.
- **Multi-agent LLM architecture:** coordinating five roles, giving them reliable tools, keeping one shared experiment record, and stopping agents from inventing results.
- **Human oversight:** designing the approval step so it is quick for the modeller but nothing changes unapproved.
- **Cloud deployment:** hosting the agent team on Azure securely, with keys kept out of the repository and costs kept low.
- **Evaluating agents:** there is no single accuracy number for an agent team, so the qualitative protocol must be fixed in advance and applied consistently.

## Knowledge/Skills Required

> Any particular knowledge or skills that are needed, or need to be learnt?

- Python data science: pandas, NumPy, scikit-learn, XGBoost.
- Tabular Foundation Models (TabPFN, TabICL, TabDPT / Mitra): how they work, their limits and their licences.
- Evaluation methodology: imbalanced classification metrics, threshold setting at a false-alert budget, bootstrap confidence intervals, calibration, feature importance.
- Causal inference basics (Directed Acyclic Graphs) and multiple-testing control (False Discovery Rate).
- Cybersecurity basics: web-server logs, common attack patterns (path scans, brute force), how fail2ban works.
- LLM agent design: prompting, tool use, multi-agent coordination, guardrails.
- Azure: Azure OpenAI and hosting a web service.
- Software engineering: git and pull requests, testing with pytest, CI.
- Writing for business stakeholders (D4).

## Devices and Software

> Software, hardware or cloud services that are required for the project. If specific hardware is needed will it be provided by the project partner? If access to a paid-for cloud service is needed (e.g., Azure, AWS, OpenAI, Anthropic, etc.), will it be funded by the project partner?

- **Hardware:** team members' own laptops. No special hardware is needed.
- **Software:** Python 3.11+, pandas, NumPy, scikit-learn, XGBoost, TabPFN, TabICL, TabDPT / Mitra, pytest, ruff, Jupyter, uv; GitHub and GitHub Actions.
- **Cloud:** Azure OpenAI for the LLM agents, and Azure for hosting D2 if the stretch deployment (S8) goes ahead. Both are paid services. **Funding and subscription access are to be confirmed with Avanade.**
- **Collaboration:** Microsoft Teams (client meetings), email, WhatsApp (team).

## Compute and GPU Resources

> Specific resources needed to support AI use or development. Will they be available?

- **TFMs:** small datasets run on a CPU, but a GPU makes TabPFN and similar models much faster. Aggregating to per-visitor / time-window rows keeps the data small enough for a laptop or a free-tier GPU (for example Google Colab). A fixed compute budget per model is agreed before the benchmark is run.
- **XGBoost and classical baselines:** run on a CPU.
- **LLM agents:** run through a hosted API (Azure OpenAI), so no local GPU is needed. Token usage is recorded (R2.8) to track cost.
- **Availability:** whether Avanade or UCL can provide GPU time or Azure credits is to be confirmed. The fallback is laptops and free-tier GPUs.

## Data

> Any data required for the project. Is it freely available, and not subject to any restrictions such as copyright? Will the data be available on time, and does it have any special storage requirements (e.g., due to size or restricted accessibility)?

**Dataset:** anonymised web-server logs from a small, volunteer-run UK leisure / ecommerce website, 6 Sep to 7 Oct 2026 (31 days). Full details are in the [dataset card](D1-Models-Benchmark/data/DATACARD-wendover.md).

| File | Contents | Rows |
|------|----------|------|
| `access_log.csv` | One row per HTTP request | 129,145 |
| `error_log.csv` | Apache error log entries | 6,452 |
| `attack_labels.csv` | fail2ban ban episodes (ground-truth labels) | 1,155 |

- **Labels:** derived from fail2ban jails (path scans, WordPress login brute force, SSH brute force and others). 743 attacker IPs out of 7,607 unique IPs. The labels reflect fail2ban's rule thresholds, so they miss low-and-slow attacks.
- **Availability:** already supplied, with `SHA256SUMS` to check integrity.
- **Restrictions:** the data belongs to the originating website operator. It is used only for this project and **may not be shared, published or redistributed**.
- **Storage:** small (about 32 MB). Must be kept only in a private repository or private storage; processed data is never committed.

## Ethical Approval and GDPR Compliance

> Does the project involve collecting or using data that can identify individuals, working with people to collect data or conduct experiments, or does it require secure storage or limited access to data, raise moral issues about the work to be undertaken or the use of the results of the work?
>
> If needed, has ethical approval been applied for or granted?

- **Personal data:** IP addresses can be personal data under UK GDPR. In this dataset every IP was replaced with an HMAC-SHA256 token using a salt that was then discarded, so the mapping cannot be reversed. The site identity, secret tokens in URLs and email addresses were also redacted. Logs do not contain POST bodies, so there are no passwords or usernames. The data is pseudonymised, and the team will make no attempt to re-identify anyone.
- **Restricted access:** the data must stay in private storage with access limited to the project, and is used only for this project.
- **Human participants:** the agent evaluation (D2) is carried out by the team on ground-truth tasks. No outside participants are recruited, so ethical approval is not expected to be needed. If the scope changes to include studies with Avanade staff or other people, ethical approval will be applied for through UCL first.
- **LLM use:** only the anonymised dataset and derived results are sent to the LLM provider (Azure OpenAI), never secrets or raw identifiers.
- **Use of results:** detection results describe attack behaviour, not individuals. Limitations are reported honestly so the results are not over-trusted.
- **Status:** ethical approval not applied for (not currently required). GDPR position to be reviewed again in Jan–Feb 2027.

## IP and Licensing

> Who owns the code the team writes, and what licence it will be released under (open source, proprietary, partner-owned)?

| Item | Owner | Terms |
|------|-------|-------|
| Project brief, planning documents, research wiki and repository | Avanade | Avanade IP. Not shared outside the project |
| Everything the team produces (D1 to D4) | Avanade | Avanade IP. Avanade decides licence, access and publication |
| Web-server log data (access, error and attack-label files) | The originating website operator | Used only for this project. May not be shared, published or redistributed |
| Third-party models, libraries and cited research | Their developers, maintainers and publishers | Used under their own licences; sources cited; commercial terms checked before any reuse |

Until Avanade chooses a licence, the code is "all rights reserved" ([LICENCE.md](LICENCE.md)). TFM weights (for example TabPFN) are checked for licence terms before use.

## Code Hosting and Hand-over

> What happens to the GitHub repo, who has access, and what gets handed over at the end (code, documentation, deployment).

- **Hosting:** a GitHub repository, which must be private because it holds the dataset and Avanade IP. Access: the five team members, the supervisor, the TA and the Avanade contact.
- **During the project:** work goes through pull requests with CI checks. Each biweekly build is a git tag (`build-YYYY-MM-DD`).
- **Hand-over (20 Mar 2027):**
  - The repository (D1 benchmark code and D2 agent code) with setup and run instructions.
  - The Azure deployment of D2 (if deployed), with deployment instructions and a list of the resources it uses, so Avanade can run or shut it down.
  - The report (D3) and the executive pitch slides (D4).
  - Documentation: the dataset card, this specification and the project log.
- **After the project:** since the work is Avanade IP, ownership of the repository and any Azure resources is transferred to Avanade, or Avanade is given a full copy, as Avanade prefers. Secrets and API keys are never committed and are revoked or handed over separately.

## Any Other Information

- **Third TFM:** the Deliverables deck names the third Tabular Foundation Model as Mitra in one place and TabDPT in another. Which one is used is to be confirmed with the client.
- **Grade rules the team follows:** everyone codes, writes website sections and talks to the client using their own git account; every agreement is made in writing and logged; 3+ options are compared for every major decision; results are reported honestly with uncertainty, and anything illustrative is labelled; every build stays runnable; sources and AI use are cited.
- **Project log:** meetings, work packages, decisions, risks, contributions and AI use are tracked in [LOG.md](LOG.md).

## Change Log

| Version | Date | Author | Summary of Changes |
|---------|------|--------|--------------------|
| 0.1 | 17 Nov 2026 | Michal Kassa | Initial version |
| 0.2 | 18 Nov 2026 | Michal Kassa | Filled in remaining sections from the Deliverables deck and repository; Azure deployment moved to stretch requirements |
