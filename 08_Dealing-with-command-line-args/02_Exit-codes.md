## **Exit Codes:**

Exit codes are numeric values returned by commands upon completion. Conventionally, an exit code of 0 indicates success, while non-zero values indicate errors.


## What does $? mean?

$? holds the exit status of the most recently executed command.

```
0 → success
non-zero (1–255) → error / failure
```

It is automatically updated by the shell after every command.

##

Example Program (`example_exit_codes.sh`):

```bash
#!/bin/bash

echo "Starting script..."

ls /nonexistent-directory
if [ $? -eq 0 ]; then
    echo "Directory exists."
else
    echo "Directory does not exist."
fi

echo "Script finished."
```

Output:

```
Starting script...
ls: cannot access '/nonexistent-directory': No such file or directory
Directory does not exist.
Script finished.
```

In this example, the `ls` command fails to list the contents of a nonexistent directory. The exit code is checked using `$?`, and the script handles the failure by printing an error message.
