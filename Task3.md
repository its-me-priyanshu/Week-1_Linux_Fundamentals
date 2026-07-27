# Task 3 - Process Managment

## Objective

The objective is to understand how Linux manages running processes and how we can monitor and control them. By performing this task, We will learn how to start, identify, stop, restart, and verify processes using commonly used Linux commands.
---
## What is a Process?

A process is simply a program that is currently running on the Linux operating system.

### For example:

- When you open Google Chrome, Chrome becomes a process.
- When you run python app.py, Python becomes a process.
- When you start Nginx, it runs as one or more processes.

### Every process has its own:

- Process ID (PID)
- Memory allocation
- CPU usage
- Parent process
- State (Running, Sleeping, Stopped, Zombie, etc.)
 
### Sometimes these services:

- Consume too much CPU
- Consume excessive memory
- Stop responding
- Crash unexpectedly
- Need restarting after configuration changes

>  **Linux provides process management commands to monitor and control these services.** 
---

## 1. Foreground process

```bash
python app.py
```

- It occupies your terminal.
- You can't use that terminal until it finishes (unless you open another terminal).

## 2. Background process

```bash
python app.py &
```

- The **&** tells the shell to start it in the background.

## 3.  Service (Daemon)
-  **A service is designed to run independently of any user terminal.**

```bash
sudo systemctl start nginx
```
- Check it:
```bash
systemctl status nginx
```

### Characteristics:

- Starts during boot if enabled.
- Keeps running without any terminal.
- Automatically managed by systemd.
- Can be restarted automatically if configured.
- Runs under a specific user (often root or a service account).
---

## Identify the Highest CPU-Consuming Process

### First Method 

```bash
top
```
**Output:**
```bash
PID USER  PR NI VIRT RES SHR S %CPU %MEM COMMAND

3412 root 20 0 980M 90M 12M R 98.4 2.5 java
1123 root 20 0 450M 55M 10M S 15.0 1.2 nginx
```

| Column | Meaning | Example |
|--------|---------|---------|
| PID | Process ID – Unique identifier for every running process. | 3412 |
| USER | User who owns the process. | root |
|
| %CPU | CPU usage percentage. | 98.4 |
| %MEM | RAM usage percentage. | 2.5 |
| COMMAND | Name of the running program or command. | java |

---

## Second Method.

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

**Explanation**

- -e → Show every process
- -o → Display selected columns
- --sort=-%cpu → Sort by CPU descending
- head → Show top entries

---

## Identify the Highest Memory-Consuming Process

```bash
ps -eo pid,cmd,%mem,%cpu --sort=-%mem | head
```

- The highest value indicates the largest memory consumer.
> look the **%MEM** part, so we can find  which process uses the most **RAM**.

## How to stop One Process Gracefully.
**Greacefuly Mean** :- A graceful stop allows the application to:
- Save data
- Close files
- Finish ongoing requests
- Release memory
- Exit safely

> Linux uses SIGTERM for graceful termination.

## Step 1.

```bash
ps -ef | python 
```
**Output**
> root 2345 pythoon3 -m http.server

- Note :- Here we can find PID.

**And**
```bash
top
```
## Step 2. 
```bash
kill 2345
```
**or**
```bash
kill -15 2345
```
-  Both send SIGTERM.

```bash
kill -9 PID
```
- it will kill the process forefully.

**Verify**

```bash
ps -p 2345
```
**Output**
> it will not show any think.

## How to Restart the Process.

```bash
puthon3 -m http.server 8000 &
```
**Verify**
```bash
ps -ef | grep http.server
```
- Now it will Restart the service.
---
## Restart System Service.

- If its a system service.
```bash
sudo systemctl restart nginx
```
**Verify**
```bash
systemctl status nginx
```
**Or**
```bash
systemctl is-active nginx
```
- It will show service is active or not.
---
## Verify the Process status
> There are Multupile ways.

**Method 1.**
```bash
ps -ef | grep nginx
```
**Method 2.**
```bash
ps -p 2345
```
**Method 3.**
```bash
top
```
---

# Documentation
## SIGKILL
**SIGKILL :-** SIGKILL (Signal 9) forcefully terminates a process immediately.

- Cannot ignore the signal
- Cannot save data
- Cannot clean up resources
- Stops instantly

## Difference Between kill and pkill

- **kill** sends a signal to a process using its Process ID (PID).

```bash
kill 2345
```
> You must know the corrct **PID** for using **Kill**

- pkill sends a signal using the process name instead of the PID.
```bash
pkill nginx
```
> Linux automatically finds matching processes and sends the signal.
---