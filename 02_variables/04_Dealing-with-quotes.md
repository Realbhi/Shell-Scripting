## In Bash, **the type of quotes you use changes how variables and special characters behave**.

Let’s break them down:

---

#  **1. Double Quotes → Variable Expands**

```bash
echo "Using double quotes: $variable"
```

Output:

```
Using double quotes: Hello World
```

Inside **double quotes**:

* `$variable` → **expands**
* `\n`, `\t` → interpreted
* `" "` → preserved (spaces stay)

Double quotes = **safe string + expansion allowed**

---

#  **2. Single Quotes → Literal, No Expansion**

```bash
echo 'Using single quotes: $variable'
```

Output:

```
Using single quotes: $variable
```

Inside **single quotes**:

* `$variable` → **NOT expanded**
* Everything treated literally
* You cannot escape characters except ending `'`

Single quotes = **raw text**

---

#  **3. No Quotes → Word Splitting Happens**

```bash
echo Using no quotes: $variable
```

Because there are **spaces** inside the variable, Bash splits them:

`$variable` → becomes two words: `Hello` and `World`

So the command becomes:

```
echo Using no quotes: Hello World
```

---

#  **4. Double Quotes Inside Double Quotes**

```bash
echo "Using double quotes: '$variable'"
```

Output:

```
Using double quotes: 'Hello World'
```

Here:

* Outer quotes are `" "`
* Inner `' '` are literal characters
* `$variable` expands normally

This is just formatting.

---

#  Best Practice (Important)

### **Always use double quotes around variables unless you have a good reason not to.**

Example:

```bash
"$variable"
```

Prevents bugs with:

* spaces
* glob characters (`*`, `?`)
* newlines

