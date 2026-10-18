# Evidence review — publication pending

The supplied archive **SOC-Home-Lab-Portfolio-Evidence-Organized.zip** contains **39 curated screenshots** in eight sections, plus a bilingual index, mapping CSV and an excluded-images list. The original organizer reported selecting 39 out of 228 images.

**The source screenshots were preserved without redaction**. None has been committed to the GitHub repository yet. This is intentional: every image must pass content and privacy review before publication.

## Evidence families

| Section in supplied ZIP | Images | Planned use |
| --- | ---: | --- |
| Lab setup/network | 4 | Architecture and connectivity |
| Wazuh server/agent | 5 | Service, endpoint, collected events |
| PowerShell / SCA | 7 | Logging configuration, Event ID 4104 |
| Failed logon | 6 | Event ID 4625, supporting fields |
| FIM | 6 | Controlled change, hashes, rule 550 |
| Custom rule | 4 | Configuration test, rule 100100 |
| Visualization drafts | 5 | Dashboard assembly process only |
| Optional troubleshooting | 2 | Before/after manager startup |

### Important correction to the original archive

The supplied archive labels the five visualization images as **IN PROGRESS**. They remain valid **intermediate editor screenshots**. The dashboard was subsequently completed, saved, and tested separately, under the title **SALEM | SOC COMMAND CENTER**. Do **not** repurpose those five drafts as proof of the final saved dashboard; obtain the final screenshot from the later test.

## High-value evidence for the portfolio front page

- Agent connected / active
- Event 4104 correlated to Wazuh rule 91843
- Rule 550 FIM change with SHA-256 fields
- Custom rule 100100 alert plus its fields
- Final saved dashboard, with five panels and no accidental level filter

These will be selected and embedded only after reviewing the original images at full resolution.

## Review checklist

Before committing any screenshot, check for:

- Credentials, private keys, API tokens, authentication headers, shared-folder secrets or browser authentication content
- Personal usernames, emails, hostnames, window titles and browser tab titles
- Lab IP addresses, MAC addresses and software version details (decide intentionally whether they should appear)
- Unexpected terminal history, command outputs, file paths and system identifiers
- Misleading screenshots, such as a failed configuration presented as final or editor drafts labeled complete

**A private GitHub repository is not a substitute for data minimization.** Keep the source ZIP in local storage until approved assets are ready.

## Evidence interpretation limits

- Event 4625 **alone** does not demonstrate brute-force activity.
- Rule 550 demonstrates a monitored file integrity change, **not** attacker attribution.
- Rule 100100 is the **one custom rule** demonstrated, not a wider detection ruleset.
- Dashboard numbers are time/filter dependent, not fixed performance metrics.
