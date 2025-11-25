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
