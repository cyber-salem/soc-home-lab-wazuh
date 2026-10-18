# Case 002 — Windows Failed Logon (Event ID 4625)

**Category:** Authentication event triage  
**Environment:** Windows 10 local Security log + Wazuh  
**Disposition:** Controlled lab authentication failure; no demonstrated compromise

## Trigger and observations

A failed sign-in event was investigated in **Windows Event Viewer → Windows Logs → Security**, then located in Wazuh Threat Hunting.

| Field | Observed or interpreted value |
| --- | --- |
| Windows Event ID | `4625` — failed account logon |
| Logon Type | `2` — interactive logon |
| Source Network Address | `127.0.0.1` — loopback/local |
| Account Name | Displayed as `-` in the examined event |
| Status | `0xC000006D` |
| SubStatus | `0xC0000380` |
| Lab context | A deliberately incorrect local sign-in PIN was entered |

The observed source address and Logon Type **do not establish that a remote attacker was involved**. Likewise, a blank account name cannot safely be interpreted as proof of which account was targeted.

The event was correlated with a Wazuh rule reporting a failed logon. The Windows and Wazuh evidence was reviewed together; the analyst should distinguish event-record identifiers from timestamps shown in local time versus UTC.

## Triage process

1. Inspect the complete Windows 4625 event, not only its headline.
2. Identify logon type, error details, account fields, source information and time.
3. Check nearby successful logon events, when available, to establish a timeline.
4. Ask whether there was a known user action, authorized testing or a pattern of repeated failures.
5. Avoid calling it brute force without a repeated pattern and supporting context.

## Assessment

The user confirmed an intentional, incorrect local PIN attempt in the test VM. That information supports a **benign lab explanation**, but the event alone would be insufficient to reach the same conclusion on an unknown corporate endpoint.

## Training distinction

The separate scenario involving **35 remote logon failures in two minutes** was a *hypothetical analyst exercise*, **not** a demonstrated live detection from this case. It is intentionally excluded from the project's factual results.

## Evidence status

The evidence archive includes Event Viewer details, source-loopback fields, and Wazuh alert views. All screenshots require privacy review before publication.
