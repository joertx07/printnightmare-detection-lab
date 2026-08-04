# PrintNightmare Threat Detection & Incident Response Lab (CVE-2021-34527)

## 📌 Executive Overview
This project documents an end-to-end security monitoring, detection engineering, and incident response implementation targeting **PrintNightmare (CVE-2021-34527)**. PrintNightmare is a critical vulnerability in the Windows Print Spooler service (`spoolsv.exe`) that permits unauthenticated remote code execution (RCE) and local privilege escalation (LPE) to `SYSTEM` privileges.

The goal of this lab was to simulate exploitation telemetry, capture kernel and system audit logs via **Sysmon** and **Windows Security Event Logs**, ingest events into **Splunk Enterprise SIEM**, engineer targeted Search Processing Language (SPL) detection rules, and generate a formal Incident Response (IR) report.

---

## 🏗️ Lab Architecture & Environment

* **Attacker:** Atomic Red Team Test T1547.012 with a custom DLL
* **Victim Workstation:** Windows 10 Pro (Domain-Joined to `mydomain.com`)
* **Domain Controller:** Windows Server 2019 (Active Directory DC)
* **SIEM / Logging Pipeline:** Splunk Enterprise & Splunk Universal Forwarder
* **Endpoint Telemetry:** Sysmon & Advanced Windows Audit Policy

---

## 📁 Repository Structure

```text
printnightmare-detection-lab/
├── README.md
├── sysmon-config.xml
├── splunk-queries/
│   ├── 01_suspicious_spoolsv_child_process.spl
│   ├── 02_unsigned_dll_loaded_by_spoolsv.spl
│   ├── 03_dll_written_to_spool_driver_path.spl
│   ├── 04_spoolsv_outbound_smb_connection.spl
│   ├── 05_new_user_account_created.spl
│   ├── 06_user_added_to_local_administrators.spl
│   └── 07_correlated_attack_timeline.spl
├── dashboards/
│   ├── printnightmare_dashboard.xml
│   └── dashboard_overview.png
├── screenshots/
│   ├── 01_sysmon_event_viewer.png
│   ├── 02_splunk_data_ingestion.png
│   ├── 03_detection_alerts_triggered.png
│   └── 04_atomic_red_team_execution.png
├── incident-report/
│   └── IR_Report_PrintNightmare.pdf
