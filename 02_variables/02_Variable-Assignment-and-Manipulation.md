## Variable Assignment and Manipulation:

---

You can assign values to variables using the assignment operator `=`. Here are examples of various types of variable assignments and manipulations:

**String Variable**
```bash
name="John"
echo "Hello, $name!"  # Output: Hello, John!
```

NOTE : Spaces are not allowed around = in variable assignment
In Bash:
```
sum=value     :: valid
sum = value   :: invalid (Bash thinks `sum` is a command)
```

**Integer Variable**
```
age=25
echo "Age: $age years"  # Output: Age: 25 years
```

**Arithmetic Operations**
```
x=10
y=5
sum=$((x + y))
echo "Sum: $sum"  # Output: Sum: 15
```

If you wrote:
```
sum=$x + $y
```

Bash would interpret it as:

Assign $x to sum , Then try to execute a command named + with argument $y. $x + $y is just a string, NOT math which obviously fails. So Bash does not do arithmetic automatically inside assignments.

**Concatenation**
```
greeting="Hello"
subject="World"
message="$greeting, $subject!"
echo $message  # Output: Hello, World!
```
