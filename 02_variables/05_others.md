### Substitution , readonly , unsetting , Escape-character and reading user input ::

---

**Substitution :**

You can capture the output of a command and assign it to a variable using command substitution. There are two ways to do this:

```bash
# Using Backticks
current_date=`date`
echo "Current date: $current_date"

# Using $(...)
current_time=$(date +%H:%M:%S)
echo "Current time: $current_time"
```
---

**Readonly Variables:**

You can declare variables as readonly to prevent their values from being changed after initial assignment:

```bash
readonly pi=3.14159
pi=3.14  # This will result in an error
```

---

**Unsetting Variables:**

You can unset (delete) a variable using the `unset` command:

```bash
unset variable_name
```

---

**Escaping Characters:**

If you need to include special characters within a variable, you can escape them using backslashes:

```bash
special_char="\$"
echo "Variable: $special_char"  # Output: Variable: $
```

---

**Reading User Input:**

To read user input in a shell script, you can use the `read` command. It reads input from the user until the Enter key is pressed and assigns the input to a variable. Here's an example:

```bash
#!/bin/bash

# Prompt the user for their name
echo "Please enter your name:"
read name

# Display a greeting using the user's input
echo "Hello, $name! Nice to meet you."
```

In this example, the user's input is stored in the `name` variable, and the script uses that input to display a greeting.

---

### Input with Prompting:

You can also use the `read` command with a prompt message directly, eliminating the need for separate `echo` commands:

```bash
#!/bin/bash

# Read input with a prompt message
read -p "Enter your favorite color: " color

echo "Your favorite color is $color."
```

**Using `read` Options:**

The `read` command has various options to customize its behavior. For example:

- `-p` specifies a prompt message.
- `-r` disables interpreting backslashes, useful for reading file paths.
- `-t` sets a timeout for input.
- `-s` hides input (useful for passwords).

```bash
#!/bin/bash

# Read password without echoing characters
read -s -p "Enter your password: " password
echo "Password entered."

# Read input with timeout
read -t 5 -p "Enter something in 5 seconds: " timed_input
echo "Y
```
