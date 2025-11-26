### Job Control in Linux 

Job control allows you to pause, resume, move to background, or bring to foreground the processes running in your shell.

---

### 1. Stop a foreground process

Press:

```
Ctrl + Z
```

This pauses the running command and marks it as "Stopped".

Example:

```
sleep 100
Ctrl + Z
[1]+  Stopped   sleep 100
```

---

### 2. View background and stopped jobs

Use:

```
jobs
```

Example output:

```
[1]+  Stopped   sleep 100
```

---

### 3. Resume a stopped job in background

Use:

```
bg %1
```

or simply:

```
bg
```

This makes the job continue running in the background.

---

### 4. Bring a job to the foreground

Use:

```
fg %1
```

The job now takes control of your terminal again.

---

### 5. Start a command directly in background

Append `&` at the end:

```
sleep 10 &
```

This runs without blocking your terminal.

---

### 6. Kill a job

Use the job number:

```
kill %1
```

Or kill by process PID:

```
kill 1234
```

---

### 7. Run a command even after logout (nohup)

Use:

```
nohup command &
```

Example:

```
nohup python3 server.py &
```

This prevents the command from stopping when the terminal closes.

---

### 8. Disown a job

To remove a job from the shell's job table:

```
disown %1
```

After this:

* It will not appear in `jobs`
* It will not terminate when the terminal closes

---

### Summary Table

| Command         | Purpose                          |
| --------------- | -------------------------------- |
| Ctrl + Z        | Pause the foreground job         |
| jobs            | List background and stopped jobs |
| bg %n           | Resume job n in background       |
| fg %n           | Bring job n to foreground        |
| command &       | Run command in background        |
| kill %n         | Kill a background job            |
| nohup command & | Run command even after logout    |
| disown %n       | Remove job from job control      |

---

