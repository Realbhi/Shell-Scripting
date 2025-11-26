
## What Happens When You Use `source file`


When you run:

```
source file
```

or

```
. file
```

the shell **reads the file and executes its commands inside the current shell**, *as if you typed them manually*.

This means:

* environment variables become available immediately
* functions get loaded
* aliases become active
* directory changes affect your current terminal
* no new shell is created
* no subshell is used
* no separate environment is created

The commands inside the file run **in the same environment** as your existing shell session.

---

## Why This Matters

Let’s compare:

### 1) Normal execution

```
./file.sh
```

This starts a **new subshell**.

Anything that happens inside:

* exports
* variable changes
* directory changes
* function definitions

does **NOT** affect your current shell.

The subshell dies after finishing the script.

---

### 2) Using `source file.sh`

This runs inside your **current shell**.

So anything inside the file:

* changes your variables
* changes your PATH
* adds aliases
* defines functions
* changes directories

and these changes **stay** after the file finishes.

---

## **A Simple Example**

Inside a file:

```
export X=10
cd /tmp
```

Run the file normally:

```
./test.sh
echo $X        → (empty)
pwd            → unchanged
```

Because it ran in a subshell.

Now **source** it:

```
source test.sh
echo $X        → 10
pwd            → /tmp
```

Because it ran inside your *current* shell.

---

## **Why do we use `source`?**

You use `source` when you want:

* to load variables
* to load functions
* to reload `.bashrc`
* to load environment settings
* to update PATH
* to apply configuration changes immediately

You *do not* use `source` to run scripts that should run independently.

---

## **What happens internally (step-by-step)**

`source file` does this:

1. Open the file
2. Read each line
3. Parse the line exactly like shell input
4. Execute it **inside the existing shell process**
5. Apply any changes to the current shell environment
6. Continue the session normally

There is **no new process**, **no fork**, **no subshell**.

---

## **Important difference in a single line:**

* `./script.sh` → runs in **a new shell**
* `source script.sh` → runs in **the current shell**


