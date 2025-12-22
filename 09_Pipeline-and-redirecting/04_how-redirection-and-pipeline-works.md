

## How `ls > file.txt` works (Redirection)

### First: every command has streams

Every Linux command runs with **three standard streams**:

| Stream | Number | Purpose       |
| ------ | ------ | ------------- |
| stdin  | 0      | input         |
| stdout | 1      | normal output |
| stderr | 2      | error output  |

By default:

* **stdin** → keyboard
* **stdout** → terminal
* **stderr** → terminal

---

## What happens with just `ls`

```bash
ls
```

Flow:

```
ls → stdout → terminal
```

`ls` writes filenames to **stdout**, and the terminal displays them.

---

## What happens with `ls > file.txt`

```bash
ls > file.txt
```

Key idea:

> `>` **replaces where stdout goes**

### Step-by-step:

1. Shell sees `>`
2. Shell opens `file.txt`

   * creates it if it doesn’t exist
   * truncates it if it exists
3. Shell **redirects stdout (fd 1)** to `file.txt`
4. Shell runs `ls`
5. `ls` writes output to stdout
6. stdout now points to `file.txt`, not terminal

So the flow is:

```
ls → stdout → file.txt
```

- Nothing is printed to the terminal
- `ls` does **not know** about the file
- Redirection is handled by the **shell**, not the command

---

## Important clarification (your question)

> “Is output going to stdout and then to file?”

No — **stdout itself is redirected**.

Think of it like unplugging a cable:

* stdout was connected to terminal
* now stdout is connected to `file.txt`

---

## Error output is NOT redirected here

```bash
ls nofile > file.txt
```

* Error message still appears on terminal
* Because `stderr (fd 2)` is untouched

To redirect errors:

```bash
ls nofile 2> error.txt
```

for :
```
ls nofile 2> error.txt
```

What this means (literally):

2> → redirect stderr

error.txt → destination file

So:

stderr is redirected to error.txt

##

**What happens to stdout here?**
Nothing.

- stdout is not redirected
- stdout still goes to the terminal
- But in this command, stdout is empty anyway

**&> : will redirect both stdout and strout to file and not to terminal**

---

## How Pipeline (`|`) works

### What pipeline means

Pipeline connects:

> **stdout of command A → stdin of command B**

Example:

```bash
ls | grep ".txt"
```

### Step-by-step:

1. Shell creates a pipe (kernel buffer)
2. Shell runs `ls`
3. Shell runs `grep`
4. stdout of `ls` → pipe
5. stdin of `grep` ← pipe

Flow:

```
ls → stdout → pipe → stdin → grep → stdout → terminal
```

---

## Combining both (very common)

```bash
ls | grep ".txt" > files.txt
```

Flow:

```
ls → grep → files.txt
```

* `ls` writes to pipe
* `grep` reads from pipe
* `grep` writes to stdout
* stdout is redirected to `files.txt`

---


## One-line summary you can safely say

> **Redirection sends a command’s output to a file, while pipelines send a command’s output to another command. Both work by rewiring stdin/stdout at the shell level.**



