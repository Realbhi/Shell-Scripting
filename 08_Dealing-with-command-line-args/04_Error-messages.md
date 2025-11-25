## **Error Messages:**
Custom error messages help users understand what went wrong. You can use `echo` to print error messages along with relevant information.

Example Program (`example_error_messages.sh`):

```bash
#!/bin/bash

file="nonexistent-file.txt"

if [ ! -f "$file" ]; then
    echo "Error: File '$file' does not exist."
    exit 1
fi

echo "File '$file' exists."
```

Output:

```
Error: File 'nonexistent-file.txt' does not exist.
```

Here, the script checks for the existence of a file. Since the file doesn't exist, an error message is printed, and the script exits with an exit code of 1.
