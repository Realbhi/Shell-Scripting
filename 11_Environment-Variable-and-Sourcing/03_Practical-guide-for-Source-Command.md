let’s do **hands-on practical exercises** step by step.
You will run these directly in your terminal.
Each task teaches you something important:

* sourcing files
* environment variables
* understanding subshell vs current shell

---

## **Task 1 — Create and Source Your Own Config File**

### Step 1: Create a new config file

Run:

```
nano myconfig.sh
```

Put this inside:

```
export MYNAME="Ash"
export MYNUMBER=42
```

Save and exit.

---

### Step 2: Source it

Run:

```
source myconfig.sh
```

---

### Step 3: Verify that variables exist

Run:

```
echo $MYNAME
echo $MYNUMBER
```

Expected output:

```
Ash
42
```

Great — you’ve just sourced your own config file successfully.
Now let’s move to the next task.

---

## **Task 2 — Test the Difference Between Sourcing and Running Normally**

This exercise helps you understand why `source` is important.

## **Step 1: Modify your file**

Open it again:

```
nano myconfig.sh
```

Add this new line at the bottom:

```
export COLOR="blue"
```

Save and exit.

---

## Step 2: Run the file *normally* instead of sourcing:

```
./myconfig.sh
```

(You may need to make it executable first: `chmod +x myconfig.sh`)

---

## Step 3: Now check the variable:

```
echo $COLOR
```

You should see **nothing**.

This is because running the script executes in a **subshell**, and exports don’t reach your current shell.

---

## Step 4: Now source it properly:

```
source myconfig.sh
```

---

## Step 5: Check again:

```
echo $COLOR
```

You should now see:

```
blue
```

---

the difference between:

running a script (subshell → variables not kept)

sourcing a script (current shell → variables kept)





