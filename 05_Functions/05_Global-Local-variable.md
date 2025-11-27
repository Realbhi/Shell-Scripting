## Scope of Variables:

Variables declared within a function have local scope, meaning they're only accessible within that function. To create local variables, use the `local` keyword. Variables declared outside functions have global scope and can be accessed from anywhere.

Here's an example illustrating local and global variables:

```bash
# Declare a global variable
global_var="I'm global"

# Declare a function with local variables
local_variables() {
    local local_var="I'm local"
    echo "Inside function: $local_var"
    echo "Inside function: $global_var"
}

# Call the local_variables function
local_variables

# Access global variable outside the function
echo "Outside function: $global_var"
# Attempting to access local_var here will result in an error
```

In the example above, the `local_var` is accessible only within the `local_variables` function, while `global_var` is accessible both inside and outside the function.

Remember that each instance of a function call has its own set of local variables, ensuring that they don't interfere with each other.

## Important Note :

In Bash, **variables are NOT local by default inside functions.**
This is one of the biggest gotchas in shell scripting.

## **Key rule**

**Bash variables are global unless you explicitly declare them `local`.**

So yes — you **must** use `local` inside a function if you want a variable to be local.

If you don’t add `local`, the variable becomes **global and will overwrite any variable with the same name outside the function.**

---

##  Demonstration

**Case 1: With `local`**

```bash
my_func() {
    local x=10
}
my_func
echo "$x"   # x is undefined (good)
```

**Case 2: Without `local`**

```bash
my_func() {
    x=10      # becomes GLOBAL
}
my_func
echo "$x"   # prints 10 (bad if you didn’t want this)
```

Without `local`, **every assignment inside the function leaks outside**.

---

##  **Why this matters**

If you write:

```bash
local_var="I'm local"
```

Inside a function **without** the `local` keyword, you are actually creating / modifying a **global** variable.

This can cause:

* accidental overwrites
* hard-to-debug scripts
* unexpected behavior when functions change global state

---

##  **Final Answer**

- **Yes — you MUST use `local` in Bash to create local variables.**
- **No — variables are NOT local by default.**

Only:

```bash
local var="value"
```

will keep `var` scoped to the function.


