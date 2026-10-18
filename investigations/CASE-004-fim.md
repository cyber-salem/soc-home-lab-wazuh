# Case 004 — File Integrity Monitoring (FIM)

**Category:** File integrity alert triage  
**Lab path:** `C:\SOC-Lab-FIM\important.txt`  
**Disposition:** Authorized test-file modification detected successfully

## Objective

Verify that Wazuh detects a change to a monitored Windows file, compares integrity data, and emits useful fields for triage.

## Configuration

A local test directory was added inside the Windows agent's existing `<syscheck>` section:

```xml
<directories check_all="yes" realtime="yes">C:\SOC-Lab-FIM</directories>
```

The agent restarted successfully. Local agent logs showed the initial scan finishing and realtime monitoring starting.

## Controlled changes

The file was created with initial content and changed deliberately:

```powershell
Set-Content 'C:\SOC-Lab-FIM\important.txt' 'Version 1 - Original File'
Get-FileHash 'C:\SOC-Lab-FIM\important.txt' -Algorithm SHA256

Set-Content 'C:\SOC-Lab-FIM\important.txt' 'Version 2 - Modified File - SOC Investigation'
Get-FileHash 'C:\SOC-Lab-FIM\important.txt' -Algorithm SHA256
```

## Verified evidence

| Field | Value |
| --- | --- |
| Wazuh Rule ID | `550` |
| Rule level | `7` |
| `syscheck.event` | `modified` |
| `syscheck.mode` | `realtime` |
| `syscheck.path` | `c:\soc-lab-fim\important.txt` |
| Alert description | Integrity checksum changed |

The local SHA-256 fingerprint **changed**, and the post-change fingerprint calculated on Windows matched `syscheck.sha256_after` in Wazuh.

In the captured alert, the monitored test file's modified time and SHA-256 fields provided additional corroborating context.

## Analyst interpretation

- A hash difference supports **a content difference**, but **does not identify the person or process** responsible.
- A Wazuh rule level expresses the configured alert priority; it does not establish attacker attribution.
- On a real system, an analyst should verify change authorization, owner, timestamps, process/user context and affected asset criticality before disposition.
- The default FIM detection does not by itself provide full process attribution or automatically block modifications.

## Follow-on engineering

A separate custom rule `100100` was written and tested to highlight changes to this specific file. See [Detection Engineering](../detection-rules/README.md).

## Evidence status

Original and modified SHA-256 screenshots and detailed Wazuh rule 550 fields are available in the organized evidence archive, pending review before public sharing.
