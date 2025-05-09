# Top 20 Shell Scripting Scenario-Based Interview Questions and Answers (with Examples)

## 1. Scenario: You need to automate backup of logs daily. How do you do it?
**Answer:** Write a shell script using tar and cron to schedule daily log backups.

**Example:**
```bash
#!/bin/bash
tar -czf /backup/logs_$(date +%F).tar.gz /var/log/*.log
```

## 2. Scenario: You want to check disk space and email admin if usage > 80%. How?
**Answer:** Use `df` and conditional logic to trigger email alerts.

**Example:**
```bash
#!/bin/bash
USAGE=$(df / | grep / | awk '{print $5}' | sed 's/%//')
if [ $USAGE -gt 80 ]; then
  mail -s "Disk space alert" admin@example.com <<< "Disk usage is ${USAGE}%"
fi
```

## 3. Scenario: You need to rename all `.txt` files to `.bak`. How?
**Answer:** Use a for loop and `mv` to rename matching files.

**Example:**
```bash
for file in *.txt; do mv "$file" "${file%.txt}.bak"; done
```

## 4. Scenario: How do you parse a CSV file line by line?
**Answer:** Use `while IFS=','` and `read` to loop through rows.

**Example:**
```bash
while IFS=',' read -r col1 col2; do
  echo "$col1 -> $col2"
done < file.csv
```

## 5. Scenario: You need to find and delete files older than 30 days. How?
**Answer:** Use `find` with `-mtime` and `-delete`.

**Example:**
```bash
find /tmp -type f -mtime +30 -delete
```

## 6. Scenario: You want to check if a process is running. If not, restart it.
**Answer:** Use `pgrep` or `ps`, then start the service if not found.

**Example:**
```bash
if ! pgrep nginx > /dev/null; then
  systemctl start nginx
fi
```

## 7. Scenario: How do you accept user input and use it in a script?
**Answer:** Use `read` to take input from the user.

**Example:**
```bash
read -p "Enter name: " name
echo "Hello, $name"
```

## 8. Scenario: How to check if a file exists and is readable?
**Answer:** Use `-f` and `-r` test options.

**Example:**
```bash
if [ -f file.txt ] && [ -r file.txt ]; then
  echo "File is readable"
fi
```

## 9. Scenario: You need to monitor memory usage and log if it exceeds threshold.
**Answer:** Use `free` or `vmstat` and write condition to log high usage.

**Example:**
```bash
mem=$(free -m | awk '/Mem:/ {print $3/$2 * 100.0}')
if (( $(echo "$mem > 90.0" | bc -l) )); then
  echo "High memory usage: $mem%" >> /var/log/mem_alert.log
fi
```

## 10. Scenario: How do you pass arguments to a shell script?
**Answer:** Use `$1`, `$2`, etc. for positional parameters.

**Example:**
```bash
#!/bin/bash
echo "User: $1, File: $2"
```

## 11. Scenario: You want to read a config file and export values. How?
**Answer:** Source the file or read line by line and export.

**Example:**
```bash
. ./env.conf
export DB_USER
```

## 12. Scenario: How do you print the 5th column of a file?
**Answer:** Use `awk` to extract the column.

**Example:**
```bash
awk '{print $5}' data.txt
```

## 13. Scenario: You need to check internet connectivity in a script. How?
**Answer:** Ping a known server and test result code.

**Example:**
```bash
ping -c 1 8.8.8.8 > /dev/null || echo "No internet!"
```

## 14. Scenario: How do you create a menu in shell script?
**Answer:** Use select loop or case block with options.

**Example:**
```bash
echo "1. Start"
echo "2. Stop"
read choice
case $choice in
  1) echo "Starting...";;
  2) echo "Stopping...";;
esac
```

## 15. Scenario: You want to schedule a shell script every 10 minutes. How?
**Answer:** Use crontab entry for 10-minute interval.

**Example:**
```bash
*/10 * * * * /path/to/script.sh
```

## 16. Scenario: How do you capture output of a command into a variable?
**Answer:** Use backticks or `$()`.

**Example:**
```bash
DATE=$(date)
echo "Today is $DATE"
```

## 17. Scenario: How do you handle script errors and exit safely?
**Answer:** Use `set -e` or `trap` to handle signals and errors.

**Example:**
```bash
set -e
trap 'echo Error on line $LINENO' ERR
```

## 18. Scenario: You want to create a multi-line string or heredoc?
**Answer:** Use `<<EOF` syntax.

**Example:**
```bash
cat <<EOF
Line1
Line2
EOF
```

## 19. Scenario: You need to loop through files in a directory. How?
**Answer:** Use `for file in /path/*` loop.

**Example:**
```bash
for f in /var/log/*.log; do
  echo "Log: $f"
done
```

## 20. Scenario: How do you debug a shell script?
**Answer:** Use `bash -x script.sh` or insert `set -x`.

**Example:**
```bash
set -x
# commands
set +x
```
