
## What is a “job”?

A *job* is any command you start in the foreground, background, or suspend using `Ctrl+Z`.

Examples of jobs:

* `sleep 10 &`
* a paused program
* commands running in background

These jobs are stored in a **job table** in the shell.

You can see them using:

```
jobs
```

Example output:

```
[1]+  Running    sleep 10 &
[2]-  Stopped    vim file.txt
```

Here:

* `[1]` and `[2]` are **job numbers**
* They are not PIDs

---

## **What `%1` means**

`%1` refers to **job number 1** from the `jobs` command.

Example:

```
bg %1
fg %1
kill %1
```

All of these operate on job **1**.

---

## **Why do we use % ?**

Because `%` tells the shell:

> “I am referring to a job specifier, not a PID.”

Without `%`, the shell thinks you mean a PID.

Example:

```
kill 1234     → kill process with PID 1234
kill %1       → kill job number 1 (from job table)
```

Two completely different things.

---

## Other job specifiers

The most common:

### `%1`, `%2`, etc.

Refers to exact job number.

### `%+`

The **current job**, usually the most recent one.

### `%-`

The **previous job** before the current one.

Example:

```
jobs
[1]+  Running    sleep 5 &
[2]-  Stopped    nano file.txt
```

Here:

* `%+` refers to job 1
* `%-` refers to job 2

### `%sleep`

If the job’s command name starts with "sleep", this refers to it.

---

## Example demonstration

Start two background jobs:

```
sleep 20 &
sleep 40 &
```

Run:

```
jobs
```

Output:

```
[1]+  Running    sleep 20 &
[2]-  Running    sleep 40 &
```

Now:

```
fg %1     → brings sleep 20 to foreground
fg %2     → brings sleep 40 to foreground
bg %-     → resumes the previous job in background
kill %+   → kills the current job
```

---

## Summary

| Symbol  | Meaning                              |
| ------- | ------------------------------------ |
| `%1`    | Job number 1                         |
| `%2`    | Job number 2                         |
| `%+`    | Current job (most recent)            |
| `%-`    | Previous job                         |
| `%name` | Job whose command starts with `name` |

Job numbers come from the **jobs table**, not system PIDs.

##

## summary about which jobs can be foregrounded and bacgrounded :

| Job State              | `fg` works?                        | `bg` works? | Behavior                                   |
| ---------------------- | -----------------------------------| ----------- | ------------------------------------------ |
| **Foreground Running** |  No (must Ctrl-Z or suspend first) |  No        | Can't background a running FG job directly |
| **Foreground Stopped** |  Yes (brings to FG again)          |  Yes       | bg resumes it in background                |
| **Background Running** |  Yes                               |  No        | fg brings it to FG; bg does nothing        |
| **Background Stopped** |  Yes                               |  Yes       | bg resumes it in background                |



