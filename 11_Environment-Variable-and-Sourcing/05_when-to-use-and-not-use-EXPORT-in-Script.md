

##  **1. What `export` really means**

`export VAR=value` marks a variable as an **environment variable**.

Meaning:

* It will be passed **to child processes** (programs or subshells)
* It is visible to commands you run from the shell

Example:

```bash
NAME="Ash"
export AGE=20
```

If you run:

```
env
```

You will only see:

```
AGE=20
```

`NAME=Ash` stays in the shell but is **not inherited** by other processes.

---

##  **2. Do you need `export` when using `source`?**

###  **NO — Not for your current shell.**

When you do:

```
source script.sh
```

or:

```
. script.sh
```

The script runs **inside your current shell**, so:

```bash
NAME="Ash"
```

already creates a variable in the current shell.

You do **not** need export for that.

So:

```bash
source script.sh
```

with this inside:

```bash
MYNAME="Ash"
```

→ You will still have `$MYNAME` in your shell afterwards.

---

##  **3. So when do you need `export`?**

###  You need `export` **only if a child process must see the variable.**

Child process examples:

* commands you run
* subshells created by `( )`
* scripts run normally (`./script.sh`)
* programs like `python`, `node`, `grep`, etc.

For example:

```bash
MYNAME="Ash"
( echo "Inside subshell: $MYNAME" )
```

Output:

```
Inside subshell:
```

(empty, because variable not exported)

But:

```bash
export MYNAME="Ash"
( echo "Inside subshell: $MYNAME" )
```

Output:

```
Inside subshell: Ash
```

---


