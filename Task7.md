# File Compression and Archiving

## Objective

**The objective is How to archive and compress files in Linux using different compression utilities. It also demonstrates how to extract archived files, compare compression efficiency, and verify that the extracted files are identical to the original files.**

## Create a directory with multiple files.
```bash
mkdir backup_demo
```
- it will create a directory.

```bash
echo "Linux file 1" > backup_demo/file1.txt
echo "Linux file 2" > backup_demo/file2.txt
echo "Linux file 3" > backup_demo/file3.txt
```
- It will create files like file1, 2, 3. with the content.

---
## Archive the directory.
```bash
tar -cvf backup.tar backup_demo/
```
**Breakdown**
- tar → Linux archiving utility.
- -c → Create a new archive.
- -v → Verbose mode (shows files being archived).
- -f → Specifies the archive filename.
- backup.tar → Name of the archive.
- backup_demo/ → Directory to archive.

---
## Compress using Gzip.

```bash
gzip -k backup.tar
```
**Breakdown**
- gzip → Compresses files using Gzip.
- -k → Keeps the original file.
- backup.tar → Archive to compress.
---

## Compress using Bzip.
```bash
bzip2 -k backup.tar
```
**Breakdown**
- bzip2 → Compresses files using Bzip2.
- -k → Keeps the original archive.
- backup.tar → Archive being compressed.
---
## Compress using XZ.
```bash
xz -k backup.tar
```
**Breakdown**
- xz → Compresses files using the XZ algorithm.
- -k → Keeps the original archive.
- backup.tar → Archive to compress.

---
## Compare compressed file sizes.

```bash
ls -lh backup.tar*
```
**Breakdown**
- ls → Lists files.
- -l → Long listing format.
- -h → Displays sizes in KB/MB (human-readable).
- backup.tar* → Shows all archive and compressed versions.

---
## Extract the file in different directory.
- Create a destination directory.
```bash
mkdir extracted_files 
```
- Extract the archive.
```bash
tar -xvf backup.tar -C extracted_files/
```
**Breakdown**

- tar → Archive utility.
- -x → Extract archive.
- -v → Displays extracted files.
- -f → Archive filename.
- backup.tar → Archive to extract.
- -C extracted_files/ → Extract into the specified directory.

---
## Verify extracted files.
```bash
diff -r backup_demo extracted_files/backup_demo
```
**Breakdown**
- diff → Compares files/directories.
- -r → Recursively compares directories.
- backup_demo → Original directory.
- extracted_files/backup_demo → Extracted directory.

> If no output appears, the files are identical.
---
##  Comparison of Compression Formats

| Format | Compression Speed | Compression Ratio | Best Use |
|--------|-------------------|-------------------|----------|
| **tar** | No compression | None | Bundling multiple files into one archive |
| **tar.gz (Gzip)** | Fast | Medium | General backups, log files, software packages |
| **tar.bz2 (Bzip2)** | Moderate | Better than Gzip | Long-term storage where smaller size is preferred |
| **tar.xz (XZ)** | Slowest | Highest | Archiving large files when maximum compression is needed |

---

### When to Use Each Format

> 1. TAR (.tar)
-  No compression.
- Preserves directory structure and file permissions.
- Suitable when compression is unnecessary or handled separately.
---
> 2. TAR + Gzip (.tar.gz)
- Fast compression and extraction.
- Widely supported across Linux and Unix systems.
- Ideal for everyday backups and software distribution.
---
> 3. TAR + Bzip2 (.tar.bz2)
- Provides better compression than Gzip.
- Takes longer to compress.
- Useful when reducing archive size is more important than speed.
---
> 4. TAR + XZ (.tar.xz)
-  Offers the highest compression ratio.
- owest compression process.
-Best for long-term archival, distributing large software packages, or saving storage space.
---
