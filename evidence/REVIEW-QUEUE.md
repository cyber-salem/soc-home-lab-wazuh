# Screenshot review queue

**Source:** `SOC-Home-Lab-Portfolio-Evidence-Organized.zip`  
**Curated total:** 39 screenshots  
**Upload status:** 15 selected, cropped derivatives have been committed to this **private** repository at [`assets/screenshots/`](../assets/screenshots/). Original full-resolution source images are preserved in the separate ZIP.

## Selected and committed to private GitHub

| Image | Status |
| --- | --- |
| Final saved dashboard | [Uploaded](../assets/screenshots/dashboard-command-center.png) |
| Active Windows agent | [Uploaded](../assets/screenshots/wazuh-agent-active.png) |
| Event 4104 local and Wazuh fields | [Gallery](GALLERY.md#4-powershell-event-4104--cross-source-validation) |
| Event 4625 local and Wazuh fields | [Gallery](GALLERY.md#3-windows-event-4625--failed-local-sign-in) |
| FIM before/after SHA-256 and rule 550 | [Gallery](GALLERY.md#5-file-integrity-monitoring--hash-verification) |
| Custom detection 100100 matching alert and hashes | [Gallery](GALLERY.md#6-custom-wazuh-detection-rule-100100) |
| SCA transcription passed | [Uploaded](../assets/screenshots/sca-transcription-passed.png) |
| Connectivity and custom-rule validation | [Gallery](GALLERY.md) |

## Highest-priority source originals (preserved in ZIP)

| Priority | Image in organized ZIP | Intended use |
| --- | --- | --- |
| P1 | `02-Wazuh-Server-and-Agent/03-win10-soc-lab-agent-active.png` | Agent connection proof |
| P1 | `03-PowerShell-Logging-and-SCA/07-wazuh-windows-event-4104-details.png` | Local/Wazuh event correlation |
| P1 | `05-File-Integrity-Monitoring/06-fim-alert-document-hash-details.png` | Hash and file-change evidence |
| P1 | `06-Custom-Detection-Rule/03-custom-fim-rule-alert-id-100100.png` | Custom rule alert |
| P1 | `06-Custom-Detection-Rule/04-custom-rule-100100-alert-evidence.png` | Custom rule detailed fields |
| P1 | **Final saved dashboard screenshot (separate from archive)** | Main project hero / final outcome |
| P2 | `05-File-Integrity-Monitoring/03-fim-test-file-sha256-baseline.png` | Hash before edit |
| P2 | `05-File-Integrity-Monitoring/04-fim-test-file-sha256-after-change.png` | Hash after edit |
| P2 | `03-PowerShell-Logging-and-SCA/02-wazuh-sca-powershell-transcription-passed.png` | Post-remediation SCA result |
| P2 | `06-Custom-Detection-Rule/02-wazuh-rule-validation-and-manager-active.png` | Rule validation |
| P2 | `04-Failed-Logon-Investigation-4625/05-wazuh-received-event-4625-alert.png` | Authentication alert |

## Remaining screenshots — technical appendix candidates

- `01-Lab-Setup-and-Network/` — 4 screenshots
- `02-Wazuh-Server-and-Agent/` — 5 total, excluding promoted P1
- `03-PowerShell-Logging-and-SCA/` — 7 total, excluding promoted screenshots
- `04-Failed-Logon-Investigation-4625/` — 6 total, excluding promoted screenshots
- `05-File-Integrity-Monitoring/` — 6 total, excluding promoted screenshots
- `06-Custom-Detection-Rule/` — 4 total, excluding promoted screenshots
- `07-Dashboard-Visualizations-IN-PROGRESS/` — 5 **editor-stage drafts**, useful as a development journey but not final dashboard proof
- `08-Troubleshooting-Optional/` — 2 optional before/after screenshots

## Remaining public-release review

1. Inspect each candidate **at original resolution**, including taskbar, browser tabs, paths, terminal history and IDs.
2. Prefer cropping to the relevant event fields; preserve unmodified originals privately.
3. Redact credentials / tokens entirely. Decide whether usernames, private IPs and MAC addresses should be displayed.
4. Check that every screenshot demonstrates the claim made in the caption.
5. Confirm the updated dashboard evidence is from its **saved view**, not a draft.
6. Upload the **approved derivative** only, add caption and link from case study, then request a second pass before setting repository public.

**Review policy:** Source originals are curated, and 15 derivative images are approved for the **private portfolio draft only**. Public publication remains pending a final identity/metadata review and explicit owner approval.
