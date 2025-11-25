### Case Statements (Switch):

The `case` statement allows you to compare a variable against multiple values and execute code based on the match.

```bash
#!/bin/bash

fruit="apple"

case $fruit in
    "apple")
        echo "It's an apple"
        ;;
    "banana")
        echo "It's a banana"
        ;;
    "orange")
        echo "It's an orange"
        ;;
    *)
        echo "Unknown fruit"
        ;;
esac
```
