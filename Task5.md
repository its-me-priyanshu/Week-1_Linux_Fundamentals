# Linux Log Analysis

## Objective

**To understand how Linux stores system logs and how to analyse them for security incidents, system events, and service failures.**

## 1. To find failed Login Attempts

**Method 1.**
```bash
sudo lastb
```
- **lastb** is read thr **btmp** log file which records unsuccessfull login attempts.

**Method 2.**
```bash
sudo journalctl -u ssh
```
- **journalctl -u ssh** is display **SSH** service logs on systems login systemd.

**Method 3.**
```bash
sudo grep "failed password" /var/log/auth.log
```
- **grep** searches authentication logs for failed password attempets.

**Output**
> user     ssh:notty 192.168.1.25  Mon Jul 21 15:32 - 15:32 (00:00)
---

## 2. System Boot History

**Method 1.**
```bash
last reboot
```
- **last reboot** is display previous system reboot records.

**Method 2.**
```bash
journalctl --list-boots
```
- **journalctl --list-boots** is list every boot recorded by the systemd journal.
 
 **Output**

 > reboot system boot 6.8.0-60-generic Mon Jul 21 08:12 still running

## 3. SSH login History

**Method 1.**
```bash
last
```
- **last** is reads the wtmp database and shows successful user logins.

**Method 2.**
```bash
grep "Accepted" /var/log/auth.log
```
- Authentication logs contain detailed SSH login information, including accepted connections.

**Output**
> student pts/0 192.168.1.15 Mon Jul 21 09:05 - 10:18

## 4. Last Shutdown

**Method 1.**

```bash
last shutdown
```
- **last shutdown** displays previous shutdown events from the **wtmp** log.

**Method 2.**

```bash
journalctl | grep shutdown
```
- **journalctl** provides additional shutdown messages recorded by systemd.

**Output**
> shutdown system down Mon Jul 21 18:45

## 5. Failed Services

**Method 1.**
```bash
systemctl --failed 
```
- **systemctl --failed** lists services that failed to start or are currently in a failed state.

**Method 2.**

```bash
journalctl -p err -b
```
- **journalctl -p err -b** displays error messages from the current boot.

**Output**

- UNIT                 LOAD   ACTIVE SUB    DESCRIPTION
- apache2.service      loaded failed failed Apache Web Server

---
### Explain.
---

## Linux Stores Logs

**Linux stores logs in the /var/log/ directory.**
- Common log files include:

## Common Linux Log Files

| Log File            | Purpose                                             |
| ------------------- | --------------------------------------------------- |
| `/var/log/auth.log` | Authentication and SSH login events (Debian/Ubuntu) |
| `/var/log/secure`   | Authentication logs (RHEL/CentOS/Fedora)            |
| `/var/log/syslog`   | General system messages (Debian/Ubuntu)             |
| `/var/log/messages` | General system logs (RHEL/CentOS)                   |
| `/var/log/kern.log` | Kernel messages                                     |
| `/var/log/boot.log` | Boot process information                            |
| `/var/log/wtmp`     | Successful login history                            |
| `/var/log/btmp`     | Failed login attempts                               |
| `/var/log/lastlog`  | Last login for each user                            |

---
## Commands Used and Their Purpose

## Useful Linux Log Analysis Commands

| Command              | Purpose                           | Why Appropriate                                                            |
| -------------------- | --------------------------------- | -------------------------------------------------------------------------- |
| `lastb`              | Displays failed login attempts    | Reads the `btmp` database specifically for failed logins.                  |
| `last reboot`        | Shows reboot history              | Retrieves historical system boot events from `wtmp`.                       |
| `last`               | Displays successful login history | Reads `wtmp`, the standard login history database.                         |
| `last shutdown`      | Shows previous shutdown events    | Retrieves recorded shutdown events.                                        |
| `systemctl --failed` | Lists failed services             | Quickly identifies services that did not start or have failed.             |
| `journalctl`         | Views systemd journal logs        | Provides detailed, searchable logs for services, boots, and errors.        |
| `grep`               | Searches log files                | Efficiently filters log entries for specific events, such as SSH failures. |
---