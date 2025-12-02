# Problems you faced

# 🧰 Shell Script Backup – Real-world Lesson

This document explains a real scenario faced during the automation of a log backup process using a shell script. It includes the problem encountered, solution implemented, and the final working script.

---

## 📝 Task

Write a shell script to:

1. Find `.log` files older than 14 days from a source directory  
2. Zip them and move the archive to a destination directory  
3. Delete the original log files from the source  
4. Log all actions and errors to a log file  

---

## ✅ Initial Success

- Script tested with a single log file — worked perfectly  
- Scheduled the script using `crontab` for automation  

---

## ❌ Problem Faced

After a few days, the number of `.log` files in the source directory increased and the script started failing.

**Root Cause:**  
The variable `$FILES` contained multiple filenames — some with **spaces or newlines**.  
This line failed:


```bash
echo $FILES | zip -@ "$ZIP_FILE"
```
### Fix Implemented:
Replaced:
```bash
echo $FILES | zip -@ "$ZIP_FILE"
```
With:
```
echo "$FILES" | tr ' ' '\n' | zip -@ "$ZIP_FILE"
```

This ensures each filename is correctly passed to zip using newline delimiters.

✅ After the change, the script worked even when the directory had many .log files with spaces in names.