**Arrays**
--

**Declaring and Using Arrays:**
In shell scripting, you can declare an array by assigning values to consecutive indices. Arrays in shell scripts are 0-indexed.

Example:
```bash
#!/bin/bash

# Declare an array with values
fruits=("Apple" "Banana" "Orange")

# Access array elements
echo "First fruit: ${fruits[0]}"
echo "Second fruit: ${fruits[1]}"
echo "Third fruit: ${fruits[2]}"
```
Output:
```
First fruit: Apple
Second fruit: Banana
Third fruit: Orange
```

---

## **Looping Through Arrays:**
You can use loops to iterate through array elements.

Example:
```bash
#!/bin/bash

fruits=("Apple" "Banana" "Orange")

# Loop through array using for loop
echo "Using for loop:"
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# Loop through array using while loop and index
echo "Using while loop:"
index=0
while [ $index -lt ${#fruits[@]} ]; do
    echo "Fruit at index $index: ${fruits[$index]}"
    index=$((index + 1))
done
```
Output:
```
Using for loop:
Fruit: Apple
Fruit: Banana
Fruit: Orange

Using while loop:
Fruit at index 0: Apple
Fruit at index 1: Banana
Fruit at index 2: Orange
```
---

## **Additional Info:**

script :

```
fruits=("Apple" "Banana" "Orange") 
index=0 
while [ $index -lt ${#fruits[@]} ]; do 
     echo "Fruit at index $index: ${fruits[$index]}" 
     index=$((index++)) 
done
```

**The problematic line :**

index=$((index++))

**In Bash arithmetic:**

- index++ returns the OLD value, then increments index.
- This is called post-increment.


## **What actually happens step by step**

Assume:

index=0

Now evaluate:

index=$((index++))

**Step 1: evaluate index++**

- Value produced: 0 (old value)
- Side effect: index becomes 1

**Step 2: assignment happens**

index=0

- The assignment overwrites the increment.
- Final result: index == 0


So yes — the increment did happen briefly, but you immediately undid it.


## **Why ((index++)) works but $((index++)) doesn’t**

This works:
((index++))


Because:

- No assignment
- Increment happens and sticks

  
This does NOT work:
index=$((index++))


Because:

- Expansion happens first
- Assignment overwrites the increment


**If you REALLY want assignment + increment**

Use pre-increment:
```
index=$((++index))
```

Why this works:

- ++index increments first
- returns the new value
- assignment keeps it
