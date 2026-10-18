# Troubleshooting log — lessons from the lab

This section records problems that actually appeared during deployment. Observed symptoms and outcomes are separated from hypotheses.

## 01 — Wazuh manager reported failed despite live subprocesses

**Symptoms:** `systemctl is-active wazuh-manager` returned `failed` while individual Wazuh components, including `wazuh-remoted` and `wazuh-analysisd`, appeared to run.

**Finding:** `systemctl show` indicated `Result=timeout` with a `TimeoutStartUSec` of 45 seconds.

**Change:** A systemd drop-in increased the startup timeout to **180 seconds**:

```ini
# /etc/systemd/system/wazuh-manager.service.d/timeout.conf
[Service]
TimeoutStartSec=180s
```

The change was applied with `systemctl daemon-reload`. After a controlled restart, `systemctl status wazuh-manager` displayed **active (running)**.

**Limitation:** This treats the startup timeout in the observed lab configuration; it does not diagnose every possible cause of slowness.

## 02 — Windows 10 VM slow or stuck during boot

A Windows 10 virtual machine appeared stuck on its boot logo and later behaved slowly. Allocating **2 vCPUs and 2500 MB RAM** allowed it to boot in the observed test.

Subsequently, Wazuh Linux guest logs also displayed a `watchdog: BUG: soft lockup` message. This was not proof of file corruption; manager status and analysis configuration were rechecked before proceeding.

**Lesson:** Check CPU, memory, competing VMs and service logs; do not immediately assume an application configuration error.

## 03 — Agent installation: download errors versus Windows service

**Symptoms:** A PowerShell `Invoke-WebRequest` download of the agent MSI failed with a transport/connection exception. Initially, `Get-Service wazuhsvc` found no service.

**Recovery:** Downloaded the official MSI using the host and transferred it to the VM via a VirtualBox shared folder. Installed with elevated Windows PowerShell, supplying the Wazuh manager address and agent name.

**Verification:** `wazuhsvc` reported Running, network port checks succeeded and the endpoint appeared as Active in Wazuh.

**Lesson:** Separate transport/download, MSI installation and agent connectivity into independent tests.

## 04 — PowerShell event collection and self-generated evidence

**Symptoms:** Searches for a test Registry command found 4104 events belonging to the **search commands**, not the original activity.

**Recovery:** Opened a new PowerShell session and generated a unique lab marker in a controlled Registry test. Queried Event ID 4104 locally, then correlated **EventRecordID 878** and ScriptBlock ID with a Wazuh rule 91843 document.

**Lesson:** Investigation actions themselves can generate logs; confirm that evidence belongs to the triggering activity.

## 05 — File integrity monitoring and custom rule

**Symptoms:** Needed to establish the file baseline before generating a controlled change and confirming the custom detection.

**Resolution:** Confirmed `syscheck` scan ended and realtime monitoring started. Tested standard rule 550, then validated custom rule 100100 using `wazuh-analysisd -t`, manager restart and positive/negative tests.

**Lesson:** Validate both expected matching and non-matching behavior.

---

**Safety:** The commands are historical lab notes, not a generic production change procedure. Use backups and approved maintenance windows for changes to real security systems.
