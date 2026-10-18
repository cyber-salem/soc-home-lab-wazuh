# SOC Lab — start, verify, and shut down safely

This is a small reference for repeating the lab without changing its configuration every time. Commands and VM names are specific to this **personal VirtualBox lab**.

## Start of session

1. Start the **Wazuh server** VM. Allow time for its services to initialize; the lab previously required a 180-second systemd startup timeout.
2. On the Wazuh server terminal / SSH session, verify the services:

```bash
sudo systemctl is-active wazuh-manager wazuh-indexer wazuh-dashboard filebeat
sudo /var/ossec/bin/wazuh-control status
```

3. Start the Windows 10 VM after the server is ready. Confirm `wazuhsvc` is running:

```powershell
Get-Service wazuhsvc
Test-NetConnection 192.168.56.101 -Port 1514
Test-NetConnection 192.168.56.101 -Port 1515
```

4. Open Wazuh → **Endpoints** and verify that `WIN10-SOC-LAB` is Active.
5. Open **SALEM | SOC COMMAND CENTER**, confirm the selected time range, remove any accidental global filters, and refresh.

**Do not paste passwords or dashboard credentials into terminal screenshots or the repository.**

## Investigate a fresh alert

- Record the **agent**, **timestamp** and **rule ID**.
- Open the detailed document rather than trusting the summary.
- For authentication events, inspect `data.win.system.eventID`, logon type, status and source.
- For PowerShell, inspect Event 4104 script text and event record identification.
- For FIM, inspect `syscheck.path`, change type, hash and mode.
- Decide whether the event is confirmed benign, suspicious, or still needs investigation, with reasons.

## End of session

1. Save relevant screenshots or notes in the local evidence area, not in an unreviewed public location.
2. Close programs on the Windows guest and use the Windows **Shut down** menu. Wait until the VirtualBox VM reports powered off.
3. Shut down the Wazuh Linux VM gracefully:

```bash
sudo shutdown -h now
```

4. Wait for its VM state to become powered off. Avoid forcefully closing a VM that is still writing indexes unless recovery requires it.
5. Next session, start the server before the Windows agent VM.

## Resource notes

Both guests run on a laptop with limited simultaneous VM resources. Monitor performance; slow service startups or Linux watchdog warnings merit investigation and should not be treated as evidence of corruption or compromise.
