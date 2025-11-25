## What is “substitution” in shell scripting?**

**Substitution means the shell replaces something with its evaluated value before running the command.**

Common types:

---

**1. Command Substitution — `$( )` or backticks**

Meaning:

> Run the command inside `$( … )`
> Capture its **output**
> Store it in a variable

Example:

```bash
name=$(whoami)
echo "User: $name"
```

If the logged-in user is `dev1`, this becomes:

```
name="dev1"
```

So the whole line expands to:

```bash
echo "User: dev1"
```

**Command substitution executes a command and substitutes its output.**

---

**2. Variable substitution — `$variable` or `${variable}`**

Example:

```bash
greet="Hello"
echo "$greet World"
```

The shell replaces `$greet` with `"Hello"`.

---

**3. Arithmetic substitution — `$(( ))`**

Example:

```bash
sum=$((5 + 10))
```

The shell evaluates the math and substitutes the result:

```
sum=15
```

---

###  Summary of Substitution Types

| Type                    | Syntax       | What It Does                 |
| ----------------------- | ------------ | ---------------------------- |
| Command substitution    | `$(command)` | Replaces with command output |
| Variable substitution   | `$var`       | Replaces with variable value |
| Arithmetic substitution | `$(( ))`     | Computes numbers             |
| Parameter expansion     | `${var}`     | Access/modify variable       |


