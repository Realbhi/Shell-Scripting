## String Concatination :

Concatenating strings in shell scripting is very simple — Bash does it automatically when you place strings next to each other.

Here are all the common ways with clear examples.

---

**1. Simple Concatenation (Most Common Way)**

```bash
str1="Hello"
str2="World"

result="$str1$str2"
echo "$result"
```

Output:

```
HelloWorld
```

If you want a space:

```bash
result="$str1 $str2"
echo "$result"
```

Output:

```
Hello World
```

---

**2. Add extra text between variables**

```bash
first="Dev"
second="Ops"

combined="${first}-${second}"
echo "$combined"
```

Output:

```
Dev-Ops
```

---

**3. Using `+=` operator**

```bash
msg="Hello"
msg+=" World"
echo "$msg"
```

Output:

```
Hello World
```

---

**4. Concatenate inside echo**

```bash
name="Ash"
echo "Hello "${name}", welcome!"
```

Output:

```
Hello Ash, welcome!
```

---

## **Practical Example: Build a file path**

```bash
dir="/home/dev"
file="script.sh"

path="${dir}/${file}"
echo "$path"
```

Output:

```
/home/dev/script.sh
```

---

## **Another Example: Add numbers into a string**

```bash
version="1."
version+="$((2 + 3))"
echo "$version"
```

Output:

```
1.5
```

---

