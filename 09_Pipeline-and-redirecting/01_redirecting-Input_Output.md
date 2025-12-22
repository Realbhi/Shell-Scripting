##  **Shell I/O Redirection**

Shell redirection allows you to **control where a command gets its input from** and **where it sends its output**.
Instead of typing into commands manually, you can use files as input or output.

---

## **1. Output Redirection**

### **Overwrite a file**

```
command > file
```

Writes the output of the command into the file (replaces previous content).

**Example:**

```
echo "Hello" > msg.txt
```

### **Append to a file**

```
command >> file
```

Adds output to the end of the file.

**Example:**

```
echo "World" >> msg.txt
```

---

## **2. Input Redirection**

### **Redirect input from a file**

```
command < file
```

Makes the command read from the file instead of the keyboard.

**Example:**

```
sort < names.txt
```

---

## **3. Redirecting Errors (stderr)**

### **Redirect errors only**

```
command 2> errors.txt
```

### **Redirect errors + normal output**

```
command > output.txt 2>&1
```

OR

```
command &> output.txt
```

---

## **4. Redirecting Both Input and Output**

```
sort < unsorted.txt > sorted.txt
```

Flow:

```
unsorted.txt → sort → sorted.txt
```

---

##  **Special Redirection Operators**

### **Here Document**

A *Here Document* lets you give **multiple lines** of input to a command.

The text between `EOF` and `EOF` is treated as **input** to the command.


###  Syntax:

```
command <<EOF
line1
line2
line3
EOF
```


```
cat <<EOF
Line 1
Line 2
EOF
```

##  Example: Writing to a file

```bash
cat <<EOF > notes.txt
Line A
Line B
Line C
EOF
```

Now `notes.txt` contains:

```
Line A
Line B
Line C
```

---

### **Here String(one-line input)**

A *Here String* is like Here Document but for **ONE line** only.

It sends the string as **input** to the command.

---

###  Syntax:

```
command <<< "text"
```

```
grep "apple" <<< "apple banana cherry"
```

##  Example: grep one-line string

```bash
grep "apple" <<< "apple banana cherry"
```

**First: what grep actually does**

- grep does NOT extract words.
- grep filters lines.

If a line matches the pattern, grep prints the entire line.

Output:

```
apple banana cherry
```

















