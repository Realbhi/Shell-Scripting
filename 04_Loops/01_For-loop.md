### Looping:

Looping structures help you repeat a set of commands multiple times.


Here are the **most commonly used** `for` loop styles in shell scripting (Bash), with clear examples.

---

**1. Basic For Loop (List of Values)**

```bash
for item in one two three
do
    echo "Item: $item"
done
```

Output:

```
Item: one
Item: two
Item: three
```

---

**2. For Loop with a Range of Numbers**

### **Using brace expansion**

```bash
for i in {1..5}
do
    echo "Number: $i"
done
```

Output:

```
1
2
3
4
5
```

---

**3. For Loop with Steps**

```bash
for i in {1..10..2}
do
    echo "Step: $i"
done
```

Output:

```
1
3
5
7
9
```

---

**4. C-Style For Loop (Like in C/Java)**

```bash
for (( i=1; i<=5; i++ ))
do
    echo "Value: $i"
done
```

Output:

```
1
2
3
4
5
```

---

**5. Loop Through Files in a Directory**

```bash
for file in *.txt
do
    echo "Found file: $file"
done
```

- Bash does not think *.txt is a directory. It simply expands the glob (*.txt) in whatever directory you're currently in.

- So the loop is really:

  - Look at current folder

  - Expand *.txt into all matching filenames
 
  - Loop over them

