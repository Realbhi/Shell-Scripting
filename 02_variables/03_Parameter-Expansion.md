## Parametre Expansion :


**What `${...}` Means**

` ${...}` in Bash is called **parameter expansion** 

It tells Bash:

> “Expand, manipulate, or extract information from a variable.”

It is more powerful than simple `$variable`.

---

### 1. **Basic Variable Expansion**

```bash
name="Ash"
echo ${name}
```

Same as `echo $name`, but braces prevent ambiguity.

---

### 2. **String Length**

```bash
var="Shell Scripting"
echo ${#var}   # 15
```

---

### 3. **Substring Extraction (Slicing)**

### Syntax:

```
${var:position:length}
```

### Examples:

```bash
var="ShellScripting"

echo ${var:0:5}     # Shell
echo ${var:5}       # Scripting (from index 5 to end)
echo ${var:6:3}     # cri
echo ${var: -3}     # last 3 chars: "ing"  (note the space before -)
```

---

### 4. **Replace Text**

**Replace first occurrence:**

```bash
text="I like apples"
echo ${text/apples/oranges}
# I like oranges
```

**Replace all:**

```bash
text="apple apple apple"
echo ${text//apple/orange}
# orange orange orange
```

---

### 5. **Remove Prefix / Suffix Using Patterns**

These are *super useful* in DevOps (file names, paths, URLs).

**Remove shortest prefix match**

```
${var#pattern}
```

**Remove longest prefix match**

```
${var##pattern}
```

The key idea:

- **# = shortest match from the start**  
- **## = longest match from the start**

**Example:**

```bash
path="/var/www/html/index.html"

echo ${path#*/}      # var/www/html/index.html
echo ${path##*/}     # index.html  (remove everything up to last /)
```
##

**Remove suffix:**

Patterns:

- **% = remove shortest suffix match**
- **%% = remove longest suffix match**
- **Patterns match from the end of the string**

```bash
file="backup.tar.gz"

echo ${file%.*}      # backup.tar
echo ${file%%.*}     # backup
```


---

### 6. **Default, Fallback, and Error Handling**

These are *critical* in production scripts.

### Use default **if variable is empty or unset**

```bash
echo ${user:-"unknown"}
```

Behavior
If user is unset or empty

- Prints "unknown"
- user remains unchanged

### Use default **and assign it**

```bash
echo ${user:="guest"}   # user becomes guest if empty
```

Behavior
If user is unset or empty

- Assigns user="guest"
- Prints "guest"


**overwrite with :="**

Assignment happens only if var is:

- unset, or
- set but empty (var="")

| Variable state | `:-`         | `:=`            |
| -------------- | ------------ | --------------- |
| Unset          | Uses default | Assigns default |
| Empty          | Uses default | Assigns default |
| Non-empty      | Uses value   | Uses value      |


| Operator | Unset   | Empty   | Non-empty | Assigns?             |
| -------- | ------- | ------- | --------- | -------------------- |
| `:-`     | default | default | value     | ❌                    |
| `:=`     | default | default | value     | ✅ (only unset/empty) |
| `=`      | default | empty   | value     | ✅ (unset only)       |


### Throw error if variable is empty

```bash
echo ${AWS_KEY:?"Error: AWS_KEY must be set"}
```

---

### 7. **Remove from Beginning or End Using Patterns**

Super useful for trimming:

```bash
text="HelloWorld"
echo ${text%World}   # Hello
echo ${text#Hello}   # World
```

---

### 8. **Uppercase / Lowercase Conversion (Bash 4+)**

```bash
str="devops"
echo ${str^^}   # DEVOPS
echo ${str,,}   # devops
echo ${str^}    # Devops (capitalize first)
echo ${str,}    # dEVOPS (lowercase first)
```

---

### 9. **Get List of Variable Names (ADV)**

```bash
echo ${!var*}
echo ${!var@}
```

---

### 10. **Indirect Expansion**

Use a variable *whose value is the name of another variable*:

```bash
a="hello"
b="a"
echo ${!b}   # prints "hello"
```

Useful for dynamically generating variable names.

---

### **Real DevOps Examples You’ll See in the Wild**

**Extract file extension:**

```bash
file="photo.jpeg"
echo ${file##*.}   # jpeg
```

**Extract filename without extension:**

```bash
echo ${file%.*}    # photo
```

**Extract basename from path:**

```bash
echo ${path##*/}   # filename
```

**Remove trailing slash:**

```bash
dir="/var/www/html/"
echo ${dir%/}      # /var/www/html
```

**Replace spaces with underscores:**

```bash
name="my project files"
echo ${name// /_}   # my_project_files
```

**Default AWS Region if unset:**

```bash
REGION=${AWS_REGION:-"us-east-1"}
```





