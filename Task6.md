# File Search and Text Processing.

## Objective
**Here we see, how to search, filter, and analyse files efficiently using commands. It helps in locating files, extracting useful information from text files, and processing log files for system administration and troubleshooting.**

## 1. Create a simple directory structure.

```bash
mkdir  -p task6/logs task6/docs task6/data
```
- It will create a directory called **task6** and inside we get directorys like **(logs, docs, data)**

## 2. Create sample files.
```bash
touch task6/logs/server.log
touch task6/logs/error.log
touch task6/docs/readme.txt
touch task6/data/sample.txt
```
- It will create such files  like **(server.log, error.log, readme.txt, sample.txt)**

## Add sample data.
```bash
echo "Linux is powerful" > task6/data/sample.txt
echo "Linux makes administration easier" >> task6/data/sample.txt
echo "Learning Linux commands" >> task6/data/sample.txt
echo "Error: Disk Full" > task6/logs/error.log
echo "Error: Permission Denied" >> task6/logs/error.log
```
**Breakdown**
- echo → Prints text.
-  Writes (>) output to a file (overwrites existing content).
-  Appends output to the (>>) end of a file without deleting existing content.

## 3. Find all .log files.
**Method  1.**

```bash
find task6 -name "*.log"
```
**Output**
```bash
./logs/error.log
./logs/system.log
```
**Breakdown**
- find → Searches for files and directories.
- . → Start searching from the current directory.
- -type f → Search only for files (f = file).
- -name "*.log" → Match files ending with .log.
- *.log → Wildcard (*) means any filename ending in .log.
> It searches recursively, and works for nested folder that is help for large directory trees.

**Method 2.**
```bash
ls task6/logs/*.log
```
> It searches only specified directory, and its a simple for one folder.

---
## 4. Find files larger than 100 MB.
```bash
find task6 -type -f -size +100M
```
**Breakdown**
- find → Searches files/directories.
- task6 → Search location.
-type f → Search only regular files.
- -size +100M
  +Greater than.
- 100M → 100 Megabytes.

---
## 5. Search for a Specific Word Inside All Files.
**Method 1.**
```bash
grep -r "error" task6 
```
**Breakdown**
- grep : Searches text inside files.
- -r : Recursive search.
- "error" : Word to search.
- task6 : Directory to search.
 
> grep -r is a simpler and faster.

**Method 2.**
```bash
find task6 -type f -exec grep "error"{} \;
```
**Breakdown**
- -exec → Executes a command on each file found.
- {} → Placeholder for each filename.
- \; → Ends the -exec command.

> **find -exec grep** is more flexible and it can combine multiple search conditions.

---
## 6. Count the Number of Occurrences of a Word.
```bash
grep -ro "error" task6 | wc -l
```
**Breakdown**
- -r → Recursive search.
- -o → Prints each matched word separately.
- "error" → Word to count.
- | → Pipe (passes output to the next command).
- wc → Word count utility.
- -l → Counts the number of lines (each match is on a separate line).

---
## 7. Display the First 20 and Last 20 Lines of a Large Log File.
**First 20 lines.**
```bash
head -20 task6/logs/server.log
```
**breakdown**
- head - Displays the beginning of a file.
- -20 - Shows the fist 20 lines.

**Last 20 lines.**
```bash
tail -20 task6/logs/server.log
```
**Breakdown**
- tail - Display the end of a files.
-20 - Shows the last 20 lines.

---
## 8. Extract Only Unique Lines From a File.
```bash
sort task6/data/simple.txt | uniq
```
**Breakdown**
- sort → Sorts the file alphabetically.
- | → Sends sorted output to another command.
- uniq → Removes consecutive duplicate lines.

---
## A simple memory trick.
> Think of Linux commands like this:

- 📂 Files/Folders → ls, find, mkdir, touch
- 🔍 Search → find, grep
- 📄 View files → cat, head, tail, less
- ✏️ Create/Edit → echo, nano, vim
- 📊 Count → wc
- 🔄 Sort/Unique → sort, uniq
- 💾 Disk usage → du