## Function Arguments and Return Values:

Shell functions can accept arguments just like command-line scripts. You access these arguments using special variables: `$1` for the first argument, `$2` for the second, and so on. To access all the arguments, you use `$@` or `$*`.

Here's an example of a function that takes two arguments and prints them:

```bash
# Declare a function named print_args
print_args() {
    echo "First argument: $1"
    echo "Second argument: $2"
}

# Call the print_args function with arguments
print_args "Hello" "World"
```

Shell functions can't directly return values like functions in some other programming languages. However, you can use the exit status of a function to convey success (0) or failure (non-zero). If you need to pass values back from a function, you can print them and capture the output using command substitution.

##

Here's an example of a function that calculates the sum of two numbers and returns it through the exit status and output:

```bash
# Declare a function named calculate_sum
calculate_sum() {
    local num1="$1"
    local num2="$2"
    local sum=$((num1 + num2))
    echo "$sum"
    return $sum
}

# Call the calculate_sum function and capture the output
result=$(calculate_sum 10 20)
echo "Sum: $result"
```


---

##  Now let's explain your function step by step

Your script:

```bash
calculate_sum() {
    local num1="$1"
    local num2="$2"
    local sum=$((num1 + num2))
    echo "$sum"
    return $sum
}
```

**Function arguments (`$1`, `$2`)**

When you call:

```
calculate_sum 10 20
```

Inside the function:

* `$1` = 10
* `$2` = 20

So:

```bash
local num1="$1"   # 10
local num2="$2"   # 20
```

---

**Arithmetic substitution**

```bash
local sum=$((num1 + num2))    # evaluates to 30
```

---

**Echoing the value**

```bash
echo "$sum"
```

This prints **30** to stdout.

Command substitution captures that output:

```bash
result=$(calculate_sum 10 20)
```

So `result="30"`.

**This is the correct way to return values from functions in Bash.**

---
More about return in next section.




