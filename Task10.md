# Cron job Scheduling.

## Objective
The objective of this task is to learn how to automate repetitive tasks in Linux using Cron Jobs. In this task, different cron schedules are created to execute commands at specific intervals, such as every minute, every 15 minutes, every Monday, on the first day of every month, and automatically at system startup.

##  Open the Crontab file.
```bash
crontab -e
```
**Breakdown :**
- **crontab** = Utility used to manage cron jobs for the current user.
- **-e** = Opens the user's cron table in the default text editor for editing.
---
## 1. Add Cron job for Every Minute.
```bash
* * * * * echo "Cron job for Every Minute" >> ~/cron_log.txt
```
**Syntax Breakdown :**
| Field | Value | Meaning |
|-------|-------|---------|
| Minute | `*` | Every minute |
| Hour | `*` | Every hour |
| Day of Month | `*` | Every day |
| Month | `*` | Every month |
| Day of Week | `*` | Every day of the week |
| Command | `echo "Cron Job Every Minute" >> ~/cron_log.txt` | Writes text into the log file |

---
## 2. Add Cron job for Every 15 Minutes.
```bash
*/15 * * * * echo "Cron job for Every 15 Minutes" >> ~/cron_log.txt
```
- ***/15** = That executes every 15 minute interval.
---

## 3. Add Cron Job for Every Monday on  9 AM.

```bash
0 9 * * 1 echo "Happy Monday" >> ~/cron_log.txt
```
> **0 9 * * 1** = So it will run a cron job on every monday at 9 AM.

---
## 4. Add Cron Job for the First Day of Every Month.
```bash
0 0 1 * * echo "First day of the month" >> ~/cron_job.txt
```
> 0 0 1 * * = It will run the cron job on every first day of the month.

---
## 5. Add Cron Job at System Startup.

```bash
@reboot echo "System started" >> ~/cron_job.txt
```
- **@reboot** = Run the cmd automatically on every time the system boots.

---
## Save and exit (if we are using vi (or vim) ).
> fist click on ESC button,

**Then**
```bash
:wq!
```
- so it will save the file and exit sussecfully.

## Verify the Cron jobs
```bash
crontab -l
```
**Breakdown :**
- crontab = Cron table utility.
- -l = list all cron jobs configuration for the current user.
---

## Cron Job Syntax formate.
```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of Week(0–7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of Month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)
```
---
## Where are cron jobs stored.

**For a user's personal cron jobs (created with crontab -e), they are typically stored in:**

```text
/var/spool/cron/crontabs/<username>    # Debian/Ubuntu
```
## Where are cron executation logs stored.
**Cron execution events are usually recorded in system log files.**

> grep CRON /var/log/syslog

**or**
> journalctl -u cron
---
