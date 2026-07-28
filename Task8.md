# Linux Environment and Shell Configuration.

## Objective
**We understand the Linux shell environment and how environment variables, shell aliases, and the PATH variable affect command execution. It also demonstrates how to customise the shell environment and make these changes persistent across login sessions.**

## Display all Enviroment variables.
```bash
printenv
```
**Alternative :**
```bash
env
```
**Output**
```bash
USER=ubuntu
HOME=/home/ubuntu
SHELL=/bin/bash
PATH=/usr/local/bin:/usr/bin:/bin
LANG=en_US.UTF-8
```
---
## Create custom Enviroment variable
```bash
export PROJECT_NAME="LinuxLab"
```
**Verify**
```bash
echo $PROJECT_NAME
```
**Output**
> LinuxLab
---
## Make the Variable Persistent Across Login Sessions.
- Open the Bash configuration file :
```bash
nano ~/.bashrc
```
- Add the following line at the end.
```baswh
export PROJECT_NAME="LinuxLab"
``` 
- save the file and reload it :
```bash
source ~/.bashrc
```
**Verify**
```bash
echo $PROJECT_NAME
```
---
## Configure a custom shell alias.
- Create a alias :
```bash
alias ll='ls -alF'
```
**Test it**
```bash
ll
```
**To make it permanent, add it to .bashrc :**
```bash
nano ~/.bashrc
```
**Add :**
```bash
alias ll='ls -alF'
```
**Reload :**
```bash
source ~/.bashrc
```
## Display your current shell.
```bash
echo $SHELL
```
**Output**
> /bin/bash

**Alternative :**
```bash
ps -p $$
```
---
## Explain and modify the PATH variable.
- Display the current PATH.
```bash
echo $PATH
```
**Output**
> /usr/local/bin:/usr/bin:/usr/local/sbin.
- Temporarily add a new directory.
```bash
export PATH=$PATH:/home/ubuntu/scripts
```
**Verify**
```bash
echo $PATH
```
- To make it permanent, add the following to  .bashrc :
```bash
export PATH=$PATH:/home/ubuntu/scripts
```
**Reload :**
```bash
source ~/.bashrc
```
---

## Breakdown of Each Linux Command

| Command | Purpose | Why it is Required |
|----------|---------|--------------------|
| `printenv` | Displays all environment variables. | Helps view the current shell environment and system configuration. |
| `env` | Shows environment variables. | Alternative command for viewing environment settings. |
| `export PROJECT_NAME="LinuxLab"` | Creates a new environment variable. | Makes the variable available to the current shell and child processes. |
| `echo $PROJECT_NAME` | Prints the value of the variable. | Verifies that the variable was created successfully. |
| `nano ~/.bashrc` | Opens the Bash configuration file. | Used to save environment variables and aliases permanently. |
| `source ~/.bashrc` | Reloads the updated configuration file. | Applies changes immediately without logging out. |
| `alias ll='ls -alF'` | Creates a shortcut command. | Improves productivity by shortening frequently used commands. |
| `ll` | Executes the alias. | Confirms the alias works correctly. |
| `echo $SHELL` | Displays the current shell. | Identifies which shell is running (e.g., Bash, Zsh). |
| `ps -p $$` | Displays information about the current shell process. | Alternative method to identify the active shell. |
| `echo $PATH` | Displays the `PATH` variable. | Shows the directories searched when executing commands. |
| `export PATH=$PATH:/home/ubuntu/scripts` | Adds a new directory to the `PATH` variable. | Allows executables in the specified directory to run without typing the full path. |
---

## Explanation of the Linux PATH Variable.

**The PATH variable is an environment variable that contains a list of directories where Linux searches for executable programs. When a command is entered, the shell checks each directory listed in PATH until it finds the matching executable.**

> For example, if /home/ubuntu/scripts is added to PATH, any executable file in that directory can be run directly:
```bash
myscript
```
**Instead of :**
> / home/ubuntu/scripts/myscript

- (Without the space: /home/ubuntu/scripts/myscript.)

> Adding a directory to **PATH** improves convenience by allowing commands to be executed from any location without specifying their full path.
---

## Summary.

- Displayed all environment variables using **printenv** and **env** .
- Created a custom environment variable with **export** .
- Made the variable persistent by editing **~/.bashrc** .
- Created and saved a custom shell alias.
- Identified the current shell using **echo $SHELL** .
- Examined and modified the **PATH** variable.
- Learned the purpose of each command and why it is essential for configuring the Linux shell environment.