# Scope, limitations, and next experiments

An honest portfolio should clearly distinguish a working laboratory demonstration from production-ready coverage.

## Verified strengths

- Connected Windows Wazuh agent and operational server services.
- Investigated Windows event IDs 4625 and 4104 with contextual fields.
- Confirmed a PowerShell event's EventRecordID and ScriptBlock ID in Wazuh.
- Detected controlled file modification and confirmed a changed SHA-256 fingerprint.
- Configured and tested a file-specific custom detection with both matching and non-matching file actions.
- Saved and refreshed a five-panel SOC monitoring dashboard.

## Important limitations

| Area | Limitation | Impact |
| --- | --- | --- |
| Scope | One monitored Windows 10 VM | Not representative of a multi-host enterprise SOC |
| Operating system | Windows 10 is an older test platform | Results should not be presented as validation of current hardened production endpoints |
| SCA benchmarking | A Windows Enterprise CIS benchmark appeared in the alert descriptions, while the observed guest was Windows 10 Home | Some control checks or priorities may not map directly to the guest edition |
| Alert level | Wazuh level numbers are configured rule priorities | A level 9 alert is not automatically a more urgent real incident than a lower-level, high-context alert |
| Alert count | Dashboard uses `wazuh-alerts-*` | Does not represent every raw Windows event or unique security incident |
| FIM | Integrity change evidence lacks verified actor/process attribution | Must correlate with audit logs or other telemetry for a full investigation |
| Rule 100100 | Matches a specific test path and the default rule 550 | Does not automatically monitor *every* sensitive file or detect every type of tampering |
| Negative test | One non-target file changed and no new custom alert appeared in the observed window | Does not establish a quantified false-positive rate |
| Brute-force training | A multi-attempt RDP scenario was discussed hypothetically | Not claimed as a lab-detected intrusion |
| Continuous monitoring | Lab VMs can be shut down between sessions | This is not a 24/7 SOC system |

## Next experiments (not yet implemented)

- Collect richer process creation telemetry (for example, properly configured Security 4688 or Sysmon) and correlate process trees.
- Add a table of raw alert details and telemetry freshness to the dashboard.
- Test a carefully scoped folder-wide FIM spotlight rule with rate/priority considerations.
- Record more controlled logon attempts and evaluate a detection rule that correlates multiple failures.
- Create repeatable test cases and preserve their expected positive and negative outcomes.
- Integrate a **future** AI-assisted analyst helper only after reliable manual triage and validation.

These are ideas for a next phase, **not claims about completed project features**.
