### Substring Extraction :

---

**1. Basic Substring Extraction**

Extract *portion by index and length*.

```bash
string="Hello, World!"
echo "${string:7:5}"   # World
```

* `7` = starting index (0-based)
* `5` = number of characters

---

**2. Extract All Characters From Position**

If you don’t specify a length:

```bash
echo "${string:7}"   # World!
```

Extracts from index `7` until end of string.

---

**3. Substring From the End (Negative Index)**

```bash
echo "${string: -6}"   # World!
```

Important: **space before minus is required** so Bash doesn’t confuse it with a parameter.

---

**4. Substring With Negative Length**

You can trim characters from the end.

```bash
echo "${string:0:-7}"   # Hello,
```

Means:

* start at position 0
* go up to (but not including) last 7 characters or can take it as **Extract everything except last 7**

##

**Summary Table**

| Operation             | Syntax                | Meaning                  |
| --------------------- | --------------------- | ------------------------ |
| Index + length        | `${str:start:length}` | basic substring          |
| From index to end     | `${str:start}`        | no length                |
| From end              | `${str: -n}`          | negative index           |
| Negative length       | `${str:start:-n}`     | trim from right          |
| Remove prefix (short) | `${str#pattern}`      | remove minimal beginning |
| Remove prefix (long)  | `${str##pattern}`     | remove maximal beginning |
| Remove suffix (short) | `${str%pattern}`      | remove minimal end       |
| Remove suffix (long)  | `${str%%pattern}`     | remove maximal end       |

