# Replacing string :

---

## **1. Replace First Occurrence**

```bash
string="I love apples and apples"
result="${string/apples/oranges}"
echo "$result"
```

Output:

```
I love oranges and apples
```

- Replaces only the **first** match
- Pattern matching is allowed (not regex, but glob-style patterns)

---

## **2. Replace All Occurrences**

```bash
string="apple apple apple"
result="${string//apple/orange}"
echo "$result"
```

Output:

```
orange orange orange
```

- `//` means replace **every** match in the string

---

##  **3. Replace Only at the Beginning of String**

```bash
string="apple pie apple"
result="${string/#apple/orange}"
echo "$result"
```

Output:

```
orange pie apple
```

- `#` anchors match to the **start**

---

##  **4. Replace Only at the End of String**

```bash
string="apple pie apple"
result="${string/%apple/orange}"
echo "$result"
```

Output:

```
apple pie orange
```

- `%` anchors match to the **end**

---

##  **Pattern Matching (NOT Regular Expressions)**

Bash uses shell-style glob patterns:

Example:

```bash
string="file123.txt"
result="${string/[0-9]*/fileX}"
echo "$result"
```

Output:

```
filefileX
```

---

##  **Practical DevOps Examples**

---

## **5. Replace spaces with underscores**

```bash
filename="my project file"
echo "${filename// /_}"
```

Output:

```
my_project_file
```

---

## **6. Replace dots in IP address**

```bash
ip="192.168.1.10"
echo "${ip//./-}"
```

Output:

```
192-168-1-10
```

---

## **7. Replace path prefix**

```bash
path="/var/www/html"
echo "${path/\/var\/www/\/opt\/web}"
```

Output:

```
/opt/web/html
```

(Quotes escape slashes)

---

## **8. Remove extension (replace with nothing)**

```bash
file="backup.tar.gz"
echo "${file%.gz}"     # remove .gz
echo "${file%.tar.gz}" # remove .tar.gz
```

---

#  **Summary Table**

| Expression         | Meaning                            |
| ------------------ | ---------------------------------- |
| `${str/pat/repl}`  | Replace **first** match            |
| `${str//pat/repl}` | Replace **all** matches            |
| `${str/#pat/repl}` | Replace only if match at **start** |
| `${str/%pat/repl}` | Replace only if match at **end**   |

---

