# Splunk Windows Security Monitoring

## Project Overview

This project demonstrates how Windows Security Event Logs can be collected, monitored, and investigated using Splunk Enterprise. The objective is to simulate the day-to-day activities of a SOC Analyst by monitoring authentication events, identifying suspicious activities, and visualizing security events through dashboards.

---

## Objectives

- Collect Windows Security Event Logs
- Monitor successful and failed logins
- Detect privileged account activity
- Detect new user account creation
- Create dashboards for security monitoring
- Perform basic security investigations using SPL

---

## Lab Environment

| Component | Details |
|----------|---------|
| Operating System | Windows 11 |
| SIEM | Splunk Enterprise |
| Log Source | Windows Security Event Logs |
| Log Collection | Splunk Universal Forwarder |
| Index | main |

---

## Architecture

![Architecture](architecture/architecture.png)

---

## Windows Event IDs Monitored

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4672 | Special Privileges Assigned |
| 4720 | User Account Created |

---

## Project Workflow

1. Generate Windows Security Events.
2. Splunk Universal Forwarder collects Security Event Logs.
3. Logs are forwarded to Splunk Enterprise.
4. Events are indexed in the **main** index.
5. SPL queries are used for investigation.
6. Dashboards visualize login activity and user behavior.

---

## SPL Queries

### Successful Logins

```spl
index=main EventCode=4624
```

### Failed Logins

```spl
index=main EventCode=4625
```

### Privileged Logons

```spl
index=main EventCode=4672
```

### New User Accounts

```spl
index=main EventCode=4720
```

### Top Users

```spl
index=main
| top Account_Name
```

### Login Timeline

```spl
index=main (EventCode=4624 OR EventCode=4625)
| timechart count by EventCode
```

Additional SPL queries are available in:

```
spl_queries/windows_security_queries.txt
```

---

## Dashboard

The dashboard contains the following panels:

- Successful Logins
- Failed Logins
- Privileged Logons
- New User Accounts
- Top Users
- Login Activity Timeline

---

## Investigation Scenario

### Scenario

A user reports repeated login failures.

### Investigation Steps

1. Search Event ID **4625**.
2. Identify affected user account.
3. Check login frequency.
4. Review source IP address (if available).
5. Compare with successful login events (4624).
6. Determine whether the activity appears suspicious.

---

## Repository Structure

```
splunk-windows-security-monitoring
│
├── README.md
├── architecture
│   └── architecture.png
│
├── screenshots
│   ├── dashboard.png
│   ├── successful_logins_4624.png
│   ├── failed_logins_4625.png
│   ├── privileged_logons_4672.png
│   ├── new_user_4720.png
│   ├── top_users.png
│   └── login_timeline.png
│
├── spl_queries
│   └── windows_security_queries.txt
│
└── reports
    └── windows_security_monitoring_report.pdf
```

---

## Skills Demonstrated

- Splunk Enterprise
- Security Monitoring
- Windows Event Log Analysis
- Authentication Monitoring
- SPL (Search Processing Language)
- Dashboard Development
- Incident Investigation
- SOC Analyst Workflow

---

## Future Enhancements

- Brute Force Detection Alert
- Email Notifications
- MITRE ATT&CK Mapping
- Threat Intelligence Integration

---

## Author

**T. Venkata Sai Siva Ramakrishna**

Aspiring SOC Analyst | Splunk | Windows Security Monitoring | Cybersecurity