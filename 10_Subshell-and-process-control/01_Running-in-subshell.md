##  **What is a Subshell?**

A **subshell** is a *new, temporary shell* created to run a command or group of commands.

- It runs **inside** your script
- It has its **own environment**
- Changes inside the subshell do **not affect** the main shell

You create a subshell using:

* `$( command )` → **command substitution**
* `( command1; command2 )` → **run multiple commands in subshell**

---

##  **Understanding the Example**

### Script:

```bash
echo "Current working directory: $(pwd)"
echo "Number of files in /tmp: $(ls /tmp | wc -l)"
```

## **Explanation 1: `$(pwd)`**

* `$(pwd)` runs the `pwd` command **inside a subshell**
* The result is substituted into the echo

Example:

```
$(pwd) → /home/user
```

So echo prints:

```
Current working directory: /home/user
```

---

## **Explanation 2: `$(ls /tmp | wc -l)`**

* Runs the whole pipeline in a subshell
* Lists `/tmp`
* Counts the number of files

If `/tmp` has 10 files:

```
$(ls /tmp | wc -l) → 10
```

So output becomes:

```
Number of files in /tmp: 10
```

---

##  **Why use a subshell?**

Because it allows you to:

- capture command output
- isolate changes (like cd, variables, etc.)
- run pipelines
- run commands without affecting your main shell

---

##  **Simple Examples of Subshells**


## **1)Get last modified file**

```bash
last_file=$(ls -t | head -1)
echo "Latest file: $last_file"
```

---

## **2)Change directory inside subshell (does NOT affect main script)**

```bash
echo "Main shell: $(pwd)"

(
    cd /tmp
    echo "Inside subshell: $(pwd)"
)

echo "Back to main shell: $(pwd)"
```

Output:

```
Main shell: /home/user
Inside subshell: /tmp
Back to main shell: /home/user
```

**cd inside subshell does NOT change the main shell directory.**

---

## **3)Group multiple commands in subshell**

```bash
(
    echo "Starting task..."
    sleep 1
    echo "Task completed."
)
```

All 3 commands run in a subshell.

---

## **4)Run pipeline inside subshell and capture output**

```bash
count=$(ps aux | grep bash | wc -l)
echo "Number of bash processes: $count"
```

---

## **5)Run background subshell**

```bash
(
    echo "Running in background..."
    sleep 3
    echo "Done"
) &
```

This runs in background without blocking your main script.

---

#  Summary of Subshell Concepts

| Syntax                   | Meaning                                    |
| ------------------------ | ------------------------------------------ |
| `$( command )`           | Run command in subshell and capture output |
| `( command1; command2 )` | Run multiple commands in subshell          |
| `( ... ) &`              | Run subshell in background                 |
| Changes inside `( )`     | **Do NOT affect** parent shell             |

---

