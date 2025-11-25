## **Array Manipulation:**
You can modify arrays by adding, removing, and updating elements.

Example:
```bash
#!/bin/bash

fruits=("Apple" "Banana" "Orange")

# Adding an element
fruits+=("Grapes")

# Updating an element
fruits[1]="Mango"

# Removing an element
unset fruits[0]

# Display the modified array
echo "Modified array:"
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done
```
Output:
```
Modified array:
Fruit: Mango
Fruit: Orange
Fruit: Grapes
```

**Note:** Some shell variants, like `sh`, might not support all these features, especially more advanced array manipulation. For extensive array manipulation, consider using a shell like `bash`.
