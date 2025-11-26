#  **Pipelines (|) – Notes**

A pipeline connects the output of one command to the input of the next.

### **Basic Syntax**

```
command1 | command2
```

Output of `command1` becomes input of `command2`.

---

## **Examples**

### **Filter lines containing a word**

```
ls /etc | grep conf
```

### **Count how many times a pattern appears**

```
grep "ERROR" logfile.txt | wc -l
```

### **Sort a file and remove duplicate lines**

```
sort file.txt | uniq
```

Pipeline flow:

```
command1 → command2 → command3 → ...
```


