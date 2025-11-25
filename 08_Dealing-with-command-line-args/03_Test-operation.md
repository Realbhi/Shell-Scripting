##  **What Are Test Operators in Shell Scripting?**

Test operators are special flags used inside condition statements like:

```bash
if [ condition ]; then
```

These operators let you **check the state of files, strings, numbers, and commands**.

Examples:

* Check if a file exists
* Check if a number is greater than another
* Check if a string is empty
* Check directory permissions

Test operators are used with:

* `[` … `]`
* `test`
* `[[` … `]]` (advanced)

---

##  **1. File Test Operators**

Used to check **files and directories**.

| Operator  | Meaning                           |
| --------- | --------------------------------- |
| `-e file` | File exists (any type)            |
| `-f file` | File exists AND is a regular file |
| `-d file` | Directory exists                  |
| `-s file` | File exists AND is not empty      |
| `-r file` | File exists AND is readable       |
| `-w file` | File exists AND is writable       |
| `-x file` | File exists AND is executable     |
| `!`       | NOT operator — reverses condition |

**Example:**

```bash
if [ -f "data.txt" ]; then
    echo "File exists"
fi
```

---

## **2. Numeric Test Operators**

Used for comparing **numbers (integers)**.

| Operator | Meaning          |
| -------- | ---------------- |
| `-eq`    | equal            |
| `-ne`    | not equal        |
| `-gt`    | greater than     |
| `-ge`    | greater or equal |
| `-lt`    | less than        |
| `-le`    | less or equal    |

**Example:**

```bash
if [ $a -gt 10 ]; then
    echo "Greater than 10"
fi
```

---

## **3. String Test Operators**

Used for comparing **text values**.

| Operator             | Meaning                         |
| -------------------- | ------------------------------- |
| `-z string`          | True if string is **empty**     |
| `-n string`          | True if string is **not empty** |
| `string1 = string2`  | Strings are equal               |
| `string1 != string2` | Strings are not equal           |

**Example:**

```bash
if [ -z "$name" ]; then
    echo "Name is empty"
fi
```

---

## **4. Logical Operators**

Used to combine conditions.

| Operator | Meaning                        |   
| -------- | ------------------------------ | 
| `!`      | NOT                            |  
| `-a`     | AND (inside `[ ]`)             |  
| `-o`     | OR (inside `[ ]`)              |   
| `&&`     | AND (safer, used with `[[ ]]`) |   


---

## **5. Advanced Test (Double Brackets `[[ ]]`)**

Recommended for modern scripts.

Advantages:

* No need to quote variables as strictly
* Uses `&&` and `||`
* Supports pattern matching

Example:

```bash
if [[ $name == A* ]]; then
    echo "Starts with A"
fi
```

---

##  **Summary**

Test operators allow you to check:

* file existence
* numeric comparison
* string comparison
* logical conditions

They are essential for writing `if`, `while`, `for`, and complex automation scripts.


