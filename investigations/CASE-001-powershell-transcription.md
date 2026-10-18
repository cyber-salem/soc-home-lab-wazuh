# Case 001 — PowerShell Transcription: SCA Finding and Remediation

**Category:** Host configuration / logging coverage  
**Environment:** Windows 10 VM + Wazuh Security Configuration Assessment (SCA)  
**Disposition:** Authorized configuration change; control re-evaluated as passed

## Evidence preview

[![Wazuh SCA shows PowerShell Transcription as Passed](../assets/screenshots/sca-transcription-passed.png)](../assets/screenshots/sca-transcription-passed.png)

*Post-remediation check result. See the discussion below for the original failure.*

## Initial finding

The Wazuh SCA check for PowerShell Transcription reported **Failed**. Inspection of the Windows policy locations did not show a configured `Transcription` policy key:

```powershell
'HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription',
'HKCU:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription' |
ForEach-Object { Test-Path $_ }
```

The missing setting matters because transcript files can help reconstruct interactive PowerShell activity during a later investigation. A failed SCA control is **not** evidence of an active attack.

## Authorized remediation

The setting was created on the Windows lab endpoint using elevated PowerShell:

```powershell
New-Item -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription' -Force
New-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription' `
  -Name EnableTranscripting -PropertyType DWord -Value 1 -Force
```

The final value was confirmed with `Get-ItemProperty`. A PowerShell transcript text file was later observed in the lab user's Documents folder.

## Validation evidence

- SCA check **15970** subsequently showed **Passed**.
- The `EnableTranscripting` registry value was `1`.
- The observation is limited to the tested host and time of assessment.

## Analyst takeaways

1. A vulnerability, a configuration failure and an incident are distinct categories.
2. Record both the **before** and **after** state when closing a security finding.
3. A single passed setting does not certify overall host hardening.
4. Transcription and Script Block Logging (event 4104) are **different telemetry sources**.

## Screenshot status

The cropped post-remediation SCA screenshot is included in the repository. The original failure view remains in the source archive for technical appendix review. See the [gallery](../evidence/GALLERY.md).
