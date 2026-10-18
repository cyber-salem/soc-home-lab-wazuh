# SOC Home Lab — Wazuh SIEM & Detection Engineering

> A hands-on defensive security lab focused on Windows event analysis, security alert triage, file integrity monitoring (FIM), and custom detection engineering.

**Status:** Core lab implementation and dashboard completed. Portfolio documentation and evidence review in progress.

## Overview

This project documents a home SOC lab built to practice the workflow of a junior security operations center (SOC) analyst: collecting telemetry, validating detections, investigating alerts, and documenting findings.

All test activities described here took place in a controlled virtual lab. A detection does **not**, by itself, prove a malicious intrusion.

## Lab architecture

| Component | Technology / purpose |
| --- | --- |
| Hypervisor | Oracle VirtualBox |
| SIEM | Wazuh 4.14.8 (manager, indexer, dashboard) |
| Endpoint | Windows 10 VM with Wazuh agent 4.14.8 |
| Host | Windows 11 |
| Lab networking | VirtualBox NAT and host-only networking |
| Log sources | Windows Security events, PowerShell Operational events, Wazuh FIM |
| Visualization | Custom Wazuh/OpenSearch dashboard |

The Wazuh server and Windows agent communicate over an isolated host-only lab network. Architecture diagrams and redacted screenshots will be added after review.

## Investigations and exercises

| Case | Topic | What was verified |
| --- | --- | --- |
| 001 | PowerShell transcription hardening | A failed configuration assessment was investigated; transcription was enabled and the assessment subsequently passed. |
| 002 | Windows failed sign-in | Event ID 4625 was inspected, including logon type, failure details, and related authentication evidence. |
| 003 | PowerShell registry activity | Event ID 4104 was collected and correlated with Wazuh rule 91843 using the Windows EventRecordID and script block details. |
| 004 | File integrity monitoring | An authorized change to a test file produced a rule 550 alert; SHA-256 values before and after the change were compared. |

Case notes, limitations, and sanitized supporting evidence are being prepared.

## Custom detection engineering

A custom Wazuh rule was created to detect changes to a specific test file monitored by FIM.

- **Custom rule ID:** `100100`
- **Severity level:** `9` (lab-defined priority)
- **Parent detection:** Wazuh rule `550` — file integrity checksum changed
- **Target:** `C:\SOC-Lab-FIM\important.txt`
- **Positive test:** Editing the target file generated a custom alert.
- **Negative test:** Editing a different monitored file generated a general FIM alert, without generating a new rule 100100 alert in the observed test window.

The custom rule and reproduction steps will be published in `detection-rules/` after a final review.

## SOC monitoring dashboard

A saved dashboard titled **SALEM | SOC COMMAND CENTER** brings together five visualizations:

1. Total Security Alerts
2. Alert Severity Distribution
3. PowerShell Activity Timeline
4. File Integrity Monitoring
5. Custom Detection Alerts

The dashboard was saved and its visualizations were confirmed to refresh successfully.

**Interpretation note:** Counts depend on the selected time range and filters. Wazuh rule levels reflect alert severity settings, not definitive evidence of malicious activity.

## Investigation approach

The lab follows a repeatable workflow:

**Alert → Validate event → Collect context → Assess impact → Determine disposition → Document evidence**

The project emphasizes distinguishing directly observed facts from hypotheses, and testing both expected detections and non-matching behavior.

## Troubleshooting and lessons learned

During setup, the lab required practical troubleshooting of:

- Wazuh manager startup timeout
- VM resource constraints and slow guest performance
- Windows agent installation and network connectivity
- PowerShell logging and session behavior
- Detection-rule validation and alert correlation

A detailed, evidence-based troubleshooting log will be added as part of the final portfolio.

## Planned repository structure

```text
soc-home-lab-wazuh/
├── README.md
├── architecture/
├── investigations/
├── detection-rules/
├── screenshots/
└── troubleshooting/
```

These folders will be populated incrementally after verifying the source files and reviewing screenshots for sensitive information.

## Scope and transparency

This is a **personal learning lab**, not a production SOC deployment or a claim of professional incident-response experience.

I built and operated the virtual lab, carried out configuration changes and controlled tests, investigated alerts, interpreted evidence, and checked the results in Windows logs and Wazuh. The custom detection and monitoring dashboard were validated through hands-on testing.

AI-assisted guidance supported parts of the learning process, including technical explanations, troubleshooting suggestions, command and configuration examples, and documentation drafting. It was **a supporting tool, not evidence of a detection or a substitute for hands-on validation and analytical judgment**.

No live company data or third-party systems were used.

---

**Maintainer:** [cyber-salem](https://github.com/cyber-salem)
