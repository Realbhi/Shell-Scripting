## **What Are Foreground and Background Processes?**

###  Foreground Process

A process that **runs directly in your terminal**
→ It takes your focus
→ You cannot use the terminal until it finishes
→ Usually requires **user interaction** (like `read`, `vim`, `cat`, etc.)

###  Background Process

A process that **runs behind the scenes**
→ You can keep using your terminal
→ It does NOT require user interaction
→ Ends by itself after some time
→ Started by putting `&` at the end

---

## **Understanding Background Processes (`&`)**

### Example:

```bash
sleep 5 &
```

The `&` tells shell:

> “Start `sleep 5` but do NOT block the shell.
> Continue running the rest of the script.”

So the script prints:

```
Background process started.
```

**immediately**, while the `sleep 5` runs silently in the background.

---

## **Understanding `wait`**

When you run a command in the background, the shell continues executing.

If you want the shell to **pause** until background tasks are complete:

```bash
wait
```

It ensures the script continues only after all background jobs finish.

---

**Walkthrough of Example Script (Background Process)**

```bash
sleep 5 &
echo "Background process started."
wait
echo "Background process completed."
```

**Step-by-step:**

`sleep 5 &`
Runs for 5 seconds **in background**

`echo "Background process started."`
Printed immediately (no waiting)

`wait`
Script pauses here until background process finishes

Print:

```
Background process completed.
```

---

## **Foreground Process Example (requires user input)**

```bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

This is a **foreground** process because:

* script stops and waits for user input
* terminal is blocked until the user types a name

Example interaction:

```
Enter your name:
John
Hello, John!
```

---

## **Another Background Process Example**

Run two tasks in parallel:

```bash
sleep 3 &
sleep 5 &
echo "Both processes started."
wait
echo "Both finished."
```

Output:

```
Both processes started.
Both finished.
```

Command finishes only when **both** sleeps are done.

---

## **Mixing Background + Foreground**

```bash
echo "Updating logs..."
( sleep 3; echo "Backup done." ) &
echo "You can continue doing other things..."
wait
echo "All tasks completed."
```

---

**Summary Table**

| Process Type   | Starts With    | Allows Using Terminal?        | Needs user input? |
| -------------- | -------------- | ----------------------------- | ----------------- |
| **Foreground** | Normal command |  No                           |  Often            |
| **Background** | command `&`    |  Yes                          |  No               |
| **Wait**       | `wait`         | Waits for all background jobs | —                 |

