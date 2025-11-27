
#  Bash: Script Execution & Subshell Behavior 

##  **Running a Script Normally (`./script.sh`)**

When you run:

```
./script.sh
bash script.sh
sh script.sh
```

###  What happens:

* A **new shell process** is created → a **subshell**.
* The script runs **inside this subshell**.
* **The subshell inherits the current working directory (PWD)** from your terminal.

### Example:

```
$ pwd
/home/user/projects
$ ./script.sh
```

Inside `script.sh`:

```bash
echo $(pwd)
```

Output:

```
/home/user/projects     ← inherited PWD
```

###  Effects:

* `cd` inside the script → does NOT affect your terminal
* variables inside script → do NOT affect your terminal
* everything is isolated to the subshell

---

##  **Subshells Created with `( ... )`**

### Syntax:

```
( command1; command2; ... )
```

### Behavior:

* Always runs in a **new subshell**, even if the script itself is already running inside a subshell.
* This nested subshell also **inherits the current working directory** from the parent shell/script.

###  Example:

```bash
echo "Before: $(pwd)"

(
    cd /tmp
    echo "Inside subshell: $(pwd)"
)

echo "After: $(pwd)"
```

Output:

```
Before: /start/location
Inside subshell: /tmp
After: /start/location
```

---

##  **Sourcing a Script (`source script.sh`)**

When you run:

```
source script.sh
. script.sh
```

###  Behavior:

* The script runs in **your current shell** — no new shell process.
* The script inherits the **current shell’s working directory**.
* Any variables or directory changes **affect your real shell**.

### BUT:

### `( ... )` inside a sourced script **still creates a subshell**,

and that subshell **still inherits your current working directory**, but remains isolated.

---

##  **Summary Table (Including PWD inheritance)**

| Action             | New Shell? | Inherits Current PWD? | Affects Current Shell? | `( )` Still Makes Subshell? |
| ------------------ | ---------- | --------------------- | ---------------------- | --------------------------- |
| `./script.sh`      |  Yes      |  Yes                 |  No                   |  Yes                       |
| `bash script.sh`   |  Yes      |  Yes                 |  No                   |  Yes                       |
| `source script.sh` |  No       |  Yes                 |  Yes                  |  Yes                       |
| `( commands )`     |  Yes      |  Yes                 |  No                   |  (always)                  |



