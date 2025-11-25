## Declaring and Using Functions:

In shell scripting, functions allow you to group a series of commands together and give them a name, making your code more organized and modular. To declare a function, you use the following syntax:

```bash
function_name() {
    # Commands to be executed
}
```

Here's an example of a simple function that prints a greeting:

```bash
# Declare a function named greet
greet() {
    echo "Hello, how are you?"
}

# Call the greet function
greet
```
