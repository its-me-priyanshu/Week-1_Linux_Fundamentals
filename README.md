# Week-1_Linux_Fundamentals
## DevOps Internship – Progressive Assessment (Week 1)

### Overview

This repository contains my solutions for the **Week 1 Linux Fundamentals** assessment as part of the **DevOps Internship – Progressive Assessment**.

The objective of this assessment is to develop practical Linux administration skills through hands-on exercises covering user management, permissions, process management, storage analysis, log investigation, file handling, compression, and shell configuration.

Each task has been documented separately with:

* Objective
* Commands Used
* Command Breakdown & Explanation
* Verification Steps
* Screenshots
* Final Output
* Errors Faced
* Resolution
* Key Learnings

---

## Assessment Information

| Item            | Details                                    |
| --------------- | ------------------------------------------ |
| Assessment      | DevOps Internship – Progressive Assessment |
| Week            | Week 1                                     |
| Topic           | Linux Fundamentals                         |
| Environment     | Ubuntu 22.04 LTS                           |
| Duration        | 1 Week                                     |
| Expected Effort | 15–20 Hours                                |

---

# Repository Structure

```text
Week1/
│
├── README.md
├── Task1.md
├── Task2.md
├── Task3.md
├── Task4.md
├── Task5.md
├── Task6.md
├── Task7.md
├── Task8.md
│
├── screenshots/
│
└── scripts/
```

---

# Tasks Overview

## Task 1 – User and Group Management

**Objective**

Perform Linux user and group administration.

**Topics Covered**

* User creation
* Group creation
* Group membership
* Password aging
* Password expiry
* Forced password reset
* Configuration verification

---

## Task 2 – Linux Permissions

**Objective**

Understand Linux ownership and permission management.

**Topics Covered**

* Directory creation
* Ownership management
* File permissions
* Group permissions
* Shared directory access
* Permission verification

---

## Task 3 – Process Management

**Objective**

Learn how Linux manages running processes.

**Topics Covered**

* Background processes
* Process monitoring
* CPU usage
* Memory usage
* Process termination
* Process restart
* Signal handling
* Process verification

---

## Task 4 – Disk Usage Investigation

**Objective**

Analyse disk and storage usage using Linux utilities.

**Topics Covered**

* Disk usage analysis
* Largest files
* Largest directories
* Recently modified files
* Root-owned files
* Storage reporting

---

## Task 5 – Linux Log Analysis

**Objective**

Investigate Linux system logs.

**Topics Covered**

* Failed login attempts
* SSH login history
* Boot history
* Shutdown history
* Failed services
* Linux logging system

---

## Task 6 – File Search and Text Processing

**Objective**

Search, filter, and analyse files using standard Linux tools.

**Topics Covered**

* File searching
* Log file discovery
* Large file identification
* Text searching
* Word counting
* File inspection
* Unique line extraction

---

## Task 7 – File Compression and Archiving

**Objective**

Understand Linux backup and archive utilities.

**Topics Covered**

* Archive creation
* File compression
* Archive extraction
* Compression comparison
* Backup verification
* Archive formats

---

## Task 8 – Linux Environment and Shell Configuration

**Objective**

Understand the Linux shell environment and user configuration.

**Topics Covered**

* Environment variables
* Persistent variables
* Shell aliases
* Current shell information
* PATH configuration
* Shell customization


**Skills Demonstrated .**

* Linux User Administration
* Group Management
* File Permissions
* Process Management
* Storage Analysis
* Log Investigation
* File Searching
* Text Processing
* Archiving & Compression
* Shell Configuration
* Linux Command-Line Operations
* Troubleshooting & Documentation

**Learning Outcome .**

By completing this assessment, I gained practical experience with essential Linux administration tasks commonly used in DevOps environments. The exercises strengthened my understanding of Linux system management, command-line utilities, troubleshooting techniques, and documentation best practices.

---

# Week 2 Tasks : Linux Administration & Automation.

## Task 9 - Systemd Service Managment.
**Objective :**

he goal of this task is to understand how to create and manage a custom systemd service in Linux. The service is designed to execute a shell script that periodically logs the current date and time, automatically restarts if it stops, and starts automatically whenever the system boots.

**Overview .**

In this task, I:

- Created a shell script that appends the current date and time to a log file at regular intervals.
- Created a custom systemd service to manage the script.
- Configured the service to restart automatically using the Restart=always directive.
- Enabled the service to start automatically after every system reboot.
- Verified the service status and confirmed that log entries were being generated correctly.

**Key Concepts learned .**

Key Concepts Learned
- Creating and managing custom systemd services.
- Writing basic shell scripts for automation.
- Configuring automatic service recovery.
- Enabling services to start during system boot.
- Monitoring service status and logs using systemctl and journalctl.

**Outcome .**
Successfully deployed a custom Linux service that continuously records timestamps to a log file, automatically recovers from failures, and runs persistently across system reboots.


## Task 7 – Cron Job Scheduling

## Objective

This task demonstrates how to automate tasks in Linux using Cron Jobs. Different scheduling patterns are configured to execute commands automatically at predefined times.

## What I Did

- Opened the user's crontab using `crontab -e`.
- Created a cron job that runs every minute.
- Created a cron job that runs every 15 minutes.
- Scheduled a cron job to execute every Monday.
- Scheduled a cron job to run on the first day of every month.
- Configured a cron job that executes automatically when the system starts using `@reboot`.
- Verified all scheduled cron jobs using `crontab -l`.

## Outcome

Successfully learned Linux task scheduling using Cron. Different cron expressions were used to automate tasks at regular intervals, weekly, monthly, and during system startup. All scheduled jobs were verified using the `crontab -l` command, and each job appends a message to `cron_log.txt`, confirming successful execution.
---