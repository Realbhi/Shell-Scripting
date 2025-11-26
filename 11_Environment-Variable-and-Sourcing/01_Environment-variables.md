## **Environment Variables and Their Usage:**
Environment variables are dynamic values that affect the behavior of processes running on a system. They provide a way to pass information from the shell to processes when they are created. Here are some commonly used environment variables and their usage:

- `PATH`: Contains a colon-separated list of directories where the shell looks for executable files. It determines which commands can be run without specifying their full path.
- `HOME`: Points to the current user's home directory.
- `USER` or `LOGNAME`: Represents the current username.
- `SHELL`: Specifies the default shell for the user.
- `PWD`: Holds the current working directory.
- `LANG` or `LC_ALL`: Determines the language and locale settings for the user interface.
- `PS1`: Defines the primary prompt string used by the shell.
- `PS2`: Defines the secondary prompt string used when input spans multiple lines.

Example:
```bash
echo "PATH: $PATH"
echo "Home Directory: $HOME"
echo "Username: $USER"
echo "Current Directory: $PWD"
echo "Language: $LANG"
echo "Primary Prompt: $PS1"
```
