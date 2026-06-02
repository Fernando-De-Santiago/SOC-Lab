# SOC Lab – SSH Brute Force Investigation

## Overview
This project simulates a basic Security Operations Center (SOC) investigation in a controlled virtual lab environment. The goal is to analyze failed SSH authentication attempts, identify patterns of suspicious activity, and document findings in an incident-style report.

The lab demonstrates foundational SOC analyst skills including log analysis, Linux command-line usage, and basic incident documentation.

---

## Objective
- Simulate SSH brute-force attempts in a controlled environment
- Collect and analyze authentication logs from a Linux server
- Identify patterns of failed login activity
- Document findings in a structured SOC incident report

---

## Lab Environment

| System        | IP Address       | Role              |
|---------------|------------------|------------------|
| Kali Linux    | 192.168.56.102   | Attacker VM      |
| Ubuntu Server | 192.168.56.101   | Target System     |
| Windows VM    | 192.168.56.103   | Secondary Host    |

All systems are connected in a private virtual network.

---

## Tools Used
- VirtualBox / VMware (virtual lab environment)
- Ubuntu Linux (log source system)
- Kali Linux (attack simulation)
- SSH (remote access protocol)
- grep (log filtering)
- cat / less / tail (log inspection)

---

## Investigation Summary

The investigation focused on analyzing `/var/log/auth.log` for failed SSH login attempts.

Key activities:
- Filtering failed authentication attempts using grep
- Identifying source IP addresses
- Observing repeated login attempts across multiple days
- Documenting findings in a structured incident report

---

## Key Findings
- Multiple failed SSH authentication attempts were detected
- Attempts targeted common usernames such as "admin" and "root"
- Activity was consistent with brute-force login behavior
- No successful authentication or system compromise occurred
- All activity was contained within a controlled lab environment

---

## Evidence
Evidence collected from:
- `/var/log/auth.log`

Filtered using:
```bash
grep -a "Failed password" /var/log/auth.log
