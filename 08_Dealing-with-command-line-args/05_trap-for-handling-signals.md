##  **What are Signals in Linux?**

A *signal* is a message sent to a process by the operating system or user.

Examples:

* `SIGINT` → Sent when you press **Ctrl + C**
* `SIGTERM` → Request to gracefully terminate
* `SIGKILL` → Force kill
* `SIGHUP` → Terminal closed
* `SIGQUIT` → Ctrl + \
* `SIGTSTP` → Ctrl + Z

Signals allow processes to react or exit gracefully.

---

## **What is `trap` in shell scripting?**

`trap` allows your script to **catch** signals and run specific commands *before* the script exits.

Syntax:

```bash
trap <commands> <signal>
```

Meaning:

> “When this signal happens, run these commands.”

---

## **Understanding the Example Script**

```bash
#!/bin/bash

cleanup() {
    echo "Cleaning up..."
    # Additional cleanup steps can be added here
    exit 1
}

trap cleanup INT

echo "Running..."
sleep 10
```

Let’s break it down.

**Step-by-Step Explanation**

## **Define a function named `cleanup`**

```bash
cleanup() {
    echo "Cleaning up..."
    exit 1
}
```

This function:

* prints **Cleaning up…**
* exits the script with status `1` → meaning the script ended because of an interruption

You can also add:

* delete temporary files
* close database connections
* stop background jobs
* unlock files

---

## **The trap command**

```bash
trap cleanup INT
```

This means:

> If the script receives the SIGINT signal (Ctrl + C), run the `cleanup` function.

Normally, pressing Ctrl + C would **immediately stop** the script.

But with `trap`, Bash runs your custom handler first.

---

## **Script execution starts**

```bash
echo "Running..."
```

Outputs:

```
Running...
```

---

## **sleep 10**

```bash
sleep 10
```

The script pauses for 10 seconds.

During this time, if you press **Ctrl + C**, normally the script would stop.
**But here, trap intercepts that signal.**

---

## **Pressing Ctrl + C triggers trap**

The terminal prints:

```
^C
Cleaning up...
```

**What happens:**

* SIGINT is received
* `trap cleanup INT` catches it
* shell executes:

  ```bash
  cleanup
  ```
* cleanup prints its message
* cleanup exits the script

This allows controlled shutdown.

---

## Why is this useful?

### **1. Prevent data loss**

If your script:

* is writing to a file
* is connecting to DB
* is downloading something

Trap lets you clean up properly.

### **2. Prevent half-written files**

You can remove temporary files:

```bash
rm -f /tmp/file.tmp
```

### **3. Stop background processes**

Useful in automation scripts.

### **4. Close network connections**

Good for DevOps/Cloud scripts.

---

##  Common signals you can trap

| Signal | Number | Trigger              |
| ------ | ------ | -------------------- |
| `INT`  | 2      | Ctrl + C             |
| `TERM` | 15     | `kill pid`           |
| `EXIT` | —      | Script ends normally |
| `HUP`  | 1      | Terminal closed      |
| `QUIT` | 3      | Ctrl + \             |
| `TSTP` | 20     | Ctrl + Z             |

Example: Run cleanup when script ends:

```bash
trap cleanup EXIT
```

This runs cleanup even if no error happens.

---

##  Another useful example

```bash
trap "echo 'Stopping script safely...'; exit" INT TERM
```

Catches both Ctrl + C and kill command.

