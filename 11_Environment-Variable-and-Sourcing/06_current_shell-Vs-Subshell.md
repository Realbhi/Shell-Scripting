

## Short answer 

> **A normal command you run in the shell runs in a child process (subshell).
> Built-ins run in the current (present) shell.**

Now let’s unpack that carefully.

---

## **Two kinds of commands in the shell**

### A) **External commands**

Examples:

```bash
ls
grep
cat
python
docker
```

These are **executables on disk** (`/bin/ls`, `/usr/bin/grep`, etc.).

**They run in a child process (subshell)**

What this means:

* The shell forks a new process
* That process runs the command
* When it exits, the process dies
* **Any changes it made are lost**

Example:

```bash
VAR=10
ls
echo $VAR
```

`VAR` is unchanged because `ls` ran in a separate process.

---

### B) **Shell built-ins**

Examples:

```bash
cd
export
source
.
read
alias
```

These are **part of the shell itself**.

**They run in the current shell**

They must, otherwise they wouldn’t work.

Example:

```bash
cd /tmp
pwd
```

If `cd` ran in a subshell, you’d jump back immediately — so it *has* to run in the current shell.

---

##  **What about shell scripts?**

### Running a script normally

```bash
./script.sh
bash script.sh
```

Script runs in a **subshell**

So:

```bash
# script.sh
export X=100
```

After running:

```bash
./script.sh
echo $X
```

`X` is NOT available

Because the script ran in a child shell.

---

### Running a script with `source` (or `.`)

```bash
source script.sh
# or
. script.sh
```

Script runs in the **current shell**

So:

```bash
source script.sh
echo $X
```

`X` **is available**

This explains your earlier `export` confusion perfectly.

---

## **Pipes create subshells (important)**

```bash
echo "hello" | read VAR
echo $VAR
```

`VAR` is empty

Why?

* `read` runs in a **subshell created by the pipe**
* Variable dies when subshell exits

---

## **Redirection does NOT create a subshell**

```bash
echo "hello" > file.txt
```

* `echo` runs normally
* Output is redirected
* No extra shell is created

---

## **How to tell if something is a builtin**

```bash
type cd
type ls
```

Output example:

```
cd is a shell builtin
ls is /bin/ls
```

---

## **Final table (very important)**

| Action                 | Runs where?   |
| ---------------------- | ------------- |
| `ls`, `grep`, `cat`    | Subshell      |
| `cd`, `export`, `read` | Current shell |
| `./script.sh`          | Subshell      |
| `source script.sh`     | Current shell |
| Command in a pipe      | Subshell      |

---

## Final one-line rule (lock this in)

> **Only built-ins and sourced scripts affect your current shell; everything else runs in a subshell and dies when it exits.**

