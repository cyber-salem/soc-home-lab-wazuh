# Custom FIM detection rule — 100100

**Status: Implemented and tested in the lab.**

## Verified screenshots

| Custom rule alert | Wazuh document fields |
| --- | --- |
| [![Wazuh rule 100100 detected](../assets/screenshots/custom-rule-100100-hit.png)](../assets/screenshots/custom-rule-100100-hit.png) | [![Rule 100100 level nine, file modification and SHA256 hashes](../assets/screenshots/custom-rule-100100-fields.png)](../assets/screenshots/custom-rule-100100-fields.png) |

[Rule syntax check and active manager](../assets/screenshots/custom-rule-validation.png) · [Evidence gallery](../evidence/GALLERY.md)

## Detection logic

The rule in [`soc_lab_fim.xml`](soc_lab_fim.xml) builds on the standard Wazuh integrity-change alert (`if_sid=550`) and matches **only**:

```text
C:\SOC-Lab-FIM\important.txt
```

The configured alert level is **9**. This is a deliberate *lab priority*, not proof that a file change is malicious.

The case-insensitive PCRE2 expression is anchored with `^` and `$` to avoid matching unrelated files. Wazuh rules may use the internal event field `file` to check the FIM path, while the indexed alert shows the path as `syscheck.path`.

## Configuration and deployment

The rule was added to the Wazuh manager's custom rule directory:

```bash
/var/ossec/etc/rules/soc_lab_fim.xml
```

The Windows agent's existing `syscheck` block contained:

```xml
<directories check_all="yes" realtime="yes">C:\SOC-Lab-FIM</directories>
```

The directory and original file already existed when FIM was initialized.

### Safe verification

```bash
sudo /var/ossec/bin/wazuh-analysisd -t
echo $?
sudo systemctl is-active wazuh-manager
```

An exit status of **0** from `wazuh-analysisd -t` confirmed the configuration test passed at that time. The manager was subsequently restarted to load the rule and returned `active`.

**Do not restart production managers just to reproduce this lab.** Schedule or stage such changes according to operational change-control policy.

## Test matrix

| Test | Input | Expected behavior | Observed in lab |
| --- | --- | --- | --- |
| Positive | Modify `important.txt` | Custom rule 100100 alert | **Pass** — level 9 alert displayed |
| Negative | Modify `other-test.txt` in same monitored directory | Standard FIM detection but no new 100100 alert | **Pass in observed window** — rule 550 appeared, 100100 count remained unchanged |

### Positive test (Windows test VM)

```powershell
Set-Content -Path 'C:\SOC-Lab-FIM\important.txt' -Value 'Version 3 - Custom Detection Rule Test'
```

Then in Wazuh Threat Hunting:

```text
rule.id: 100100
```

### Negative test (Windows test VM)

```powershell
Set-Content 'C:\SOC-Lab-FIM\other-test.txt' 'Negative Test - Version 1'
Set-Content 'C:\SOC-Lab-FIM\other-test.txt' 'Negative Test - Version 2'
```

Compare Wazuh searches for `rule.id: 550` and `rule.id: 100100`. Match on timestamps and `syscheck.path`, rather than assuming a count alone proves the cause.

## Limitations and future enhancements

- This rule detects only the **specified file**, not every file in the directory.
- It depends on FIM coverage and successful event collection.
- It has no documented automatic prevention, attribution, or ticketing actions.
- A separate folder-wide spotlight rule can be developed later.
- A security team's production alert level should follow asset criticality, change frequency, and response procedures.
- Additional test cases (rename, delete, overlapping rules, baseline drift) remain future work.

See [Case 004](../investigations/CASE-004-fim.md) for the investigation behind the file integrity finding.
