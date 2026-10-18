# Development Roadmap — In Progress

**Project:** [Wazuh SOC Home Lab](README.md)  
**Track:** SOC Analyst L1 → Detection Engineering → AI-Assisted SOC  
**Roadmap last updated:** 2026-10-18

> **Core Phase 01 is complete. Further development is ongoing.** The five milestones below are planned improvements—not completed features. Each will be marked done **only after** hands-on testing, evidence collection, and a written investigation or technical report.

## Progress at a glance

| Priority | Next milestone | Current status | Evidence required to mark complete |
| --- | --- | --- | --- |
| 01 | **Case 005 — Suspicious Process Tree Investigation** | **Next up · Planned** | Parent/child process telemetry, timeline, analyst verdict |
| 02 | **Case 006 — Repeated Failed Logon Detection** | **Planned** | Correlation rule, controlled test, false-positive review |
| 03 | **Case 007 — DNS & Network Anomaly Investigation** | **Planned** | DNS/process correlation, context enrichment, case report |
| 04 | **Detection Engineering v2 — Detection-as-Code & Testing** | **Planned** | Versioned rules, reproducible positive/negative tests, coverage notes |
| 05 | **AI-Assisted SOC Triage Prototype** | **Planned · Advanced goal** | Read-only alert enrichment, evidence-grounded summaries, human review |

---

## 01. Case 005 — Suspicious Process Tree Investigation

**Objective:** Understand what executed, which process launched it, and whether the observed parent-child relationship is expected in context.

**Technical plan:** Enable and validate Sysmon process-creation telemetry (Event ID 1), or Windows Security 4688 with appropriate settings; generate a safe laboratory test and correlate process IDs, parent image, command line, user, time, and host in Wazuh.

**Definition of done**
- [ ] Confirm process creation telemetry arrives from the Windows VM.
- [ ] Reproduce a safe parent-child process test; capture original logs and matching Wazuh data.
- [ ] Produce an annotated process tree and timeline.
- [ ] Write **Case 005** with competing explanations, disposition, and limitations.

**Skills demonstrated:** Process investigation, Windows telemetry, evidence correlation, analyst reasoning.

## 02. Case 006 — Repeated Failed Logon Detection

**Objective:** Move from investigating a single Windows 4625 event to detecting a *pattern* of repeated failed authentication attempts in the controlled lab.

**Technical plan:** Generate an approved series of local test failures, inspect 4625 event fields and time windows, design a Wazuh frequency/correlation rule, and test the outcome against benign isolated failures. Avoid targeting external accounts or services.

**Definition of done**
- [ ] Establish a normal single-failure baseline.
- [ ] Produce repeated failed sign-ins using lab-only accounts.
- [ ] Implement and test a rule that detects a repeated-failure pattern.
- [ ] Record detection window, threshold, false-positive considerations, and escalation criteria in **Case 006**.

**Skills demonstrated:** Authentication triage, SIEM correlation, detection tuning.

## 03. Case 007 — DNS & Network Anomaly Investigation

**Objective:** Investigate suspicious-looking outbound DNS behavior using host and network evidence rather than judging a domain name alone.

**Technical plan:** Collect suitable DNS telemetry (for example, Sysmon Event ID 22 if supported by the configuration, or another documented log source), generate clearly benign controlled queries, correlate timestamps, source process, queried domains, and observed network behavior.

**Definition of done**
- [ ] Verify DNS events are captured and indexed correctly.
- [ ] Create a harmless, repeatable test with documented expected behavior.
- [ ] Enrich and classify observed domains using context, not appearance alone.
- [ ] Write **Case 007** with evidence, alternative explanations, and what remains unknown.

**Skills demonstrated:** DNS investigation, endpoint/network correlation, reducing false positives.

## 04. Detection Engineering v2 — Detection-as-Code & Repeatable Tests

**Objective:** Make custom Wazuh detections easier to maintain, reproduce, and validate—not merely increase the number of alert rules.

**Technical plan:** Extend the existing custom-rule work, keep configurations in Git, document dependencies and minimum logging requirements, add safe positive/negative test cases, and map relevant detections to MITRE ATT&CK only when supported by observed behavior.

**Definition of done**
- [ ] Add at least **two additional lab-validated** custom detections with clear scope.
- [ ] Document expected fields, sample benign test actions, and prerequisites.
- [ ] Record positive and negative outcomes for each new detection.
- [ ] Publish a simple regression checklist or test harness and known limitations.

**Skills demonstrated:** Detection logic, rule maintenance, quality assurance, ATT&CK-informed analysis.

## 05. AI-Assisted SOC Triage Prototype — Advanced Goal

**Objective:** Explore AI for accelerating repetitive SOC work **without delegating the security verdict to AI**.

**Technical plan:** Build an experimental **read-only** assistant that accepts sanitized Wazuh alert samples or securely retrieved test data, extracts verifiable fields, proposes investigation questions, and drafts an analyst-facing summary with explicit evidence references. Keep credentials out of repositories and logs.

**Definition of done**
- [ ] Define a structured alert input and a consistent output format.
- [ ] Demonstrate an evidence-grounded summary for at least **three** controlled lab alerts.
- [ ] Show where the assistant distinguishes facts, hypotheses, and missing evidence.
- [ ] Compare summaries against a manual analyst checklist, including incorrect or incomplete suggestions.
- [ ] Document privacy safeguards and require **human approval** for any action; no autonomous blocking or remediation.

**Skills demonstrated:** SOC workflow design, safe AI integration, structured analysis, analyst oversight.

---

## Change log — visible progress, not artificial activity

| Date | Verified update |
| --- | --- |
| **2026-10-18** | Published this roadmap following Phase 01 core implementation: four documented exercises, one tested custom rule, and a saved five-panel monitoring dashboard. |

**Update policy:** Add a dated row only when meaningful work is performed and verified. A daily commit is *not* required; quality of evidence matters more than commit frequency.

## Project boundaries

- All investigation tests must run on systems and accounts owned or explicitly authorized for the lab.
- Plans are aspirational and are **not** listed as current job skills until actually practiced.
- Screenshots, rules and findings will be linked when available.
- The primary goal remains practical **SOC L1 / Blue Team** capability, with AI as a support tool.

[← Back to project overview](README.md) · [Existing case studies](investigations/) · [Current evidence gallery](evidence/GALLERY.md)
