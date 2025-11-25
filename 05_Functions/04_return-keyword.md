
##  The `return` statement

You wrote:

```bash
return $sum
```


In Bash:

### `return` does NOT return values

It only returns **exit codes** (0–255).

So:

```bash
return 30
```

Means:

> Set function exit status to 30.

It **does not** return the number 30 to the caller.

---

## **1. Exit status / return status in Bash**

When a function or command finishes, it returns a number from **0–255**.

This number is called:

* exit status
* return status
* exit code

You can see it using:

```bash
echo $?
```

**What’s happening behind the scenes?**

$? always holds: The exit code of the most recently executed command or function.

```
0 → success
non-zero → error/failure
```

```bash
check_number() {
    if [ "$1" -gt 10 ]; then
        return 0      # success
    else
        return 1      # failure
    fi
}

check_number 15
echo $?    # prints 0 because 15 > 10

check_number 5
echo $?    # prints 1 because 5 <= 10
```

---

## **2. What do the numbers mean?**

**0 means SUCCESS**

This is universal.

* No errors
* Everything executed correctly

Example:

```bash
return 0
```

Means:
Function ran successfully.

---

**Non-zero means FAILURE**

Any number between **1–255** means something went wrong.

Example:

```bash
return 1
```

Means:
Function failed.

**Important:**

The numbers **do not have fixed meanings** globally.

* You *decide* what each exit code means inside your script.
* Other tools define their own codes.

---

##  Why only 0–255?

Because exit codes are stored in **1 byte**, and 1 byte = **256 possible values**.

If you try:

```bash
return 350
```

Bash converts it using modulo 256:

```
350 % 256 = 94
```

So the return value becomes **94**, not 350.

---

#  Summary

| Code      | Meaning                                            |
| --------- | -------------------------------------------------- |
| **0**     | Success                                            |
| **1–255** | Error (type depends on your script or the program) |

Exit codes **do NOT have preset meanings** except:

* `0 = success`
* non-zero = error

The script author decides the meaning of each code.



