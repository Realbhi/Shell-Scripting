## An environment variable is:
a key=value pair stored inside a process’s environment

Important consequences:
	•	The kernel holds it for each process
	•	A process inherits env vars from its parent
	•	Files do not own env vars — files only set them
  
So $PATH, $HOME, $USER live in memory, not in a file.

**Files like:**
	•	.bashrc
	•	/etc/profile
	•	/etc/environment
  
are just startup scripts.

They are executed:
when a shell or login starts. And they 
And inside those files you’ll see lines like:

export JAVA_HOME=/usr/lib/jvm/java-17
export PATH=$PATH:/opt/maven/bin

These lines create environment variables at startup.

##

**Lets go step by step :**

1️⃣ Kernel / login manager (earliest)

When you log in (SSH, GUI, TTY):

	•	login process sets basics like:
	◦	USER
	◦	LOGNAME
	◦	HOME
	◦	SHELL

These are not from .bashrc.
They come from:
	•	/etc/passwd
	•	PAM modules
Example:
getent passwd $USER


2️⃣ System-wide environment files

These affect all users.

/etc/environment

	•	Pure KEY=value
	•	No export
	•	No shell syntax
  
Example:

JAVA_HOME=/usr/lib/jvm/java-17
Loaded by PAM at login.

/etc/profile

	•	Executed for login shells
	•	Can contain shell logic
	•	Often sets PATH

/etc/profile.d/*.sh

	•	Modular system-wide configs
	•	Tools drop files here (Java, Maven, etc.)

PATH

PATH is built step by step:

	1	System sets a basic PATH
	2	/etc/profile adds more
	3	.bashrc may add more
	4	You might add more manually
  
So PATH is combined, not defined in one place.

3)  Shell built-ins and defaults

Some variables are:

	•	Created by the shell itself
  
Examples:

PWD
SHLVL
_

Why Jenkins / scripts sometimes don’t see variables

Because:
	•	Jenkins runs non-interactive shells
	•	.bashrc is not executed
	•	So variables defined there are missing
  
That’s why:
	•	Jenkins has its own environment {} block
	•	Docker uses -e VAR=value

Docker case (very simple)
When you run:

docker run -e A=B mongo
Docker:
	•	does not read .bashrc
	•	directly injects A=B into the container process
  
Environment variables go straight into memory of the container process.


Interactive -shell : A shell where you type commands and see a prompt
Non-interactive shell  :A shell that runs commands automatically, without a user typing , No prompt, No waiting for input.

Example : 
bash script.sh
sh -c "echo hello"
jenkins job
cron job
docker CMD

Interactive shell : Reads  :::: ~/.bashrc so variables are accessible in shell 
Non-interactive shell : Does NOT read:::: ~/.bashrc

By default, it reads nothing from your shell config files.


Why Linux does this (design reason) : 

Loading .bashrc would:

	•	slow execution
	•	introduce unpredictable aliases
	•	break scripts

Then how do non-interactive shells get variables?
They get them from:

🔹 Parent process
If parent has variable → child inherits
Example:

export A=1
bash -c 'echo $A'   # prints 1

🔹 Explicit injection
	•	Jenkins environment {}
	•	Docker -e VAR=value
	•	Script export VAR=value

🔹 System-wide env files
	•	/etc/environment
	•	systemd service files

One sentence to remember (interview safe)
A non-interactive shell runs commands automatically and does not read user shell startup files, so environment variables defined there are missing.










