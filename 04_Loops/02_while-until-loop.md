## `while` Loop:

The `while` loop repeatedly executes a block of code as long as a condition is true.

```bash
#!/bin/bash

count=1

while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

## `until` Loop:

The `until` loop is similar to the `while` loop but continues executing until a condition becomes true.

```bash
#!/bin/bash

num=0

until [ $num -ge 5 ]; do
    echo "Number: $num"
    ((num++))
done
```
