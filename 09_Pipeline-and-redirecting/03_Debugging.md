## **Shell Script Debugging:**

Debugging shell scripts involves identifying and fixing errors in your scripts. Proper debugging techniques can help you locate issues quickly and efficiently. Two common techniques for debugging shell scripts are printing/debugging techniques and using `set -x` and `set -e`.

**1. Printing/Debugging Techniques:**
One of the simplest ways to debug shell scripts is to use print statements to display variable values, execution paths, and other relevant information. You can use `echo`, `printf`, or `logger` commands to print messages to the console or system logs.

Example Script:
```bash
#!/bin/bash

name="John"
age=25

echo "Debug: Starting script..."
echo "Debug: Name is $name"
echo "Debug: Age is $age"

result=$((age * 2))
echo "Debug: Result is $result"

echo "Debug: Script completed."
```

**Output:**
```
Debug: Starting script...
Debug: Name is John
Debug: Age is 25
Debug: Result is 50
Debug: Script completed.
```

While this technique is simple, it can become overwhelming for larger scripts and might not provide a structured view of the script's execution flow.

**2. Using `set -x` and `set -e`:**
The `set -x` command, when added at the beginning of a script, enables the debugging mode. It prints each line before executing it, allowing you to see the exact commands being executed.

The `set -e` command, when added, makes the script exit immediately if any command returns a non-zero exit status. This helps catch errors early in the script execution.

Example Script:
```bash
#!/bin/bash

set -x
set -e

name="John"
age=25

echo "Debug: Starting script..."
echo "Debug: Name is $name"
echo "Debug: Age is $age"

result=$((age * 2))
echo "Debug: Result is $result"

# Introducing an intentional error to demonstrate set -e
ls /nonexistent_directory

echo "Debug: Script completed."
```

**Output:**
```
+ name=John
+ age=25
+ echo 'Debug: Starting script...'
Debug: Starting script...
+ echo 'Debug: Name is John'
Debug: Name is John
+ echo 'Debug: Age is 25'
Debug: Age is 25
+ result=50
+ echo 'Debug: Result is 50'
Debug: Result is 50
+ ls /nonexistent_directory
ls: cannot access '/nonexistent_directory': No such file or directory
```

In this example, the `set -x` command shows each executed command with a `+` sign, and the `set -e` command causes the script to exit immediately after the `ls` command fails.

**Notes:**
- While `set -x` and `set -e` are powerful debugging tools, they may not be suitable for all scenarios. For instance, `set -e` might lead to unexpected exits if you're intentionally handling errors.
- To turn off debugging mode, use `set +x`.
- Debugging tools like `set -x` and `set -e` are usually used for development and testing purposes. In production, it's recommended to minimize debugging outputs and handle errors more gracefully.

---

##  Why use **set +x** instead of removing **set -x**?

Because **`set -x` and `set +x` control debugging at different points during script execution.**

###  `set -x`

Turns **debug mode ON**
→ The shell prints each command before executing it
→ Useful for debugging *part* of a script

###  `set +x`

Turns **debug mode OFF**
→ Stops printing commands
→ You can resume normal output

If you **remove `set -x` completely**, you lose the ability to toggle debugging inside the script.

---

##  Why toggling is useful (the real reason)

Sometimes you want:

* debug **only part** of the script
* not debug everything
* avoid removing and re-adding `set -x` every time

Example:

```bash
echo "Script started"

set -x       # start debugging
ls /tmp      # debug this
date         # debug this
set +x       # stop debugging

echo "Done"
```

This will print debug logs **only for ls & date**, not for the whole script.


Remember that effective debugging involves understanding the script's logic, carefully analyzing error messages, and iteratively refining your code based on the feedback you receive.
