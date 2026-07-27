# Task 4 :- Disk Usage Investigation
## objective
**Investigate and analyse disk storage usage in a Linux system using basic commands. It includes creating files totaling at least 1 GB, identifying the largest files and directories, finding recently modified and root-owned files, and generating a short storage usage report.**

## 1. Create files totaling at least 1 GB.

**Create a text directory and generate sample files.**
```bash
mkdir disk_usage_test
cd disk_usage_test
```
**Then**
```bash
fallocate -l 400M file1
fallocate -l 350M file2
fallocate -l 150M file3
fallocate -l 120M file4
```
## Breakdown
- fallocate → Creates a file by allocating disk space.
- -l → Length (size of the file).
- 500M → File size (500 MB).
- file1 → Name of the file.

**Verify**
```bash
du -sh .
```
**Output**
> 1.2 GB

## 2. Find the 10 largest files.

**Method 1.**

```bash
find . -type f | xargs ls -lhS | head
```
- This command **finds all files, sorts them by size**, and **shows the first 10 largest files.**

## Breakdown 

- find : searches for files and directories.
- **.**  means current directory.
- -type : Specify the type of item to search.
- f = files.
- d = Directory
- xargs : Its list down of file name from **find** and passes them as arguments to another cmd.
- lhS : Make it long listing format so human can read size and short files by size, with the largest first.

**Or**
```bash
ls -lhS
```
**Method 2.**
```bash
find . -type f -exec du -h {} + | sort -hr | head -10
```
## Breakdown
- find : searches for files and directories.
- **.**  means current directory.
- -type : Specify the type of item to search.
- f = files.
- d = Directory
- -exec : That tell **find** to **execute another command** on the files it finds.
- du : Displays the disk usage of files or directories.
- -h : Shows sizes in a human-readable format (KB, MB, GB)
- {} : its a placeholder, its represents each files found by the **find** cmd.
- plus : The + tell **find** to pass multiple files at once to du, making it faster.
- short -hr : short the output and make it human readable form.
- r : Reverse order ( largest first).
---
## 3. Find top 5 largest directories.
```bash
du -sh * | sort -hr | head -5
```
**Breakdown**
- du -sh : Disk space  and summary in human readable form.
- star : Every files and folder in the current directory.
sort -hr : Sort lines to understands size like MB and GB.
- r : Reverse order ( largest first).
- head -5 : Shows only the first 5 lines. 
> This command lists directory sizes, sorts them from largest to smallest, and displays the top five.
---

## 4. Files modified in the last 24 hrs.

```bash
find . -type f -mtime -1
```
**Breakdown**
- find : Search for files.
- . : Search in the current directory.
- -mtime : Modification time.
- -1 : Less than one day (last 24 hours).

> **find** searches for files. **-mtime -1** filters files modified within the last 24 hours.

---
## 5. Find files owned by root.

```bash
sudo find / -user root
```
**Breakdown**
- find → Search command.
- / → Search from the root directory (entire filesystem).
- -user → Search by file owner.
- root → Owner's username.

> This command searches the entire filesystem for files owned by the root user.
---
