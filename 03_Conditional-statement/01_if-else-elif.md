### Conditional Statement :

---

Conditional statements allow your script to make decisions and execute different code paths based on certain conditions.

### `if`, `else`, `elif`:

The `if` statement is used to execute code block(s) conditionally. You can use `else` to define what should be done if the condition is not met, and `elif` to add more conditions.

```bash
#!/bin/bash

num=10

if [ $num -gt 10 ]; then
    echo "Number is greater than 10"
elif [ $num -eq 10 ]; then
    echo "Number is equal to 10"
else
    echo "Number is less than 10"
fi
```

### More-Info :

---

`-gt` is a **numeric comparison operator** used inside Bash’s `[ ]` test command.

**Other numeric comparison operators in Bash**

| Operator | Meaning               | Example         |
| -------- | --------------------- | --------------- |
| `-eq`    | equal to              | `[ $a -eq $b ]` |
| `-ne`    | not equal to          | `[ $a -ne $b ]` |
| `-gt`    | greater than          | `[ $a -gt $b ]` |
| `-ge`    | greater than or equal | `[ $a -ge 10 ]` |
| `-lt`    | less than             | `[ $a -lt 5 ]`  |
| `-le`    | less than or equal    | `[ $a -le 20 ]` |

These are for **integer comparisons only**.

---

###  Why can't you use `>` directly?

Because:

* `>` is a **file redirection operator** in Bash, not a numeric operator
* `[ ]` uses special operators like `-gt`, `-lt`, etc.

If you accidentally try:

```bash
if [ $num > 10 ]; then   # WRONG
```

`>` will try to **create a file named “10”** — not compare numbers.

---

###  Using modern syntax with `(( ))`

You *can* use normal math operators if you switch to arithmetic evaluation:

```bash
if (( num > 10 )); then
    echo "Number is greater than 10"
fi
```

Inside `(( ))`:

* `>`, `<`, `>=`, `<=` all work normally
* No need for `$` before variable names


