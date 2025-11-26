## **Combining Subshells and Process Control:**

Subshells can be combined with process control techniques to manage complex scenarios.

**Example Script 4: Combining Subshells and Process Control**

```bash
#!/bin/bash

# Running commands in a subshell and background process
(
    echo "Subshell working directory: $(pwd)"
    sleep 3 &
    echo "Subshell background process started."
    wait
    echo "Subshell background process completed."
)
echo "Main shell continues."
```

**Output:**
```
Subshell working directory: /home/user
Subshell background process started.
[1]+  Done                    sleep 3
Subshell background process completed.
Main shell continues.
```

In the example above, the subshell is used to run commands, including a background process. The main shell continues executing while the subshell is running. This demonstrates the isolation and concurrent execution of subshells.

In summary, subshells allow you to isolate commands and variables within a separate shell instance. Process control techniques like running processes in the background or foreground enhance the efficiency and usability of shell scripts. By combining these concepts, you can create powerful and flexible shell scripts for various tasks.
