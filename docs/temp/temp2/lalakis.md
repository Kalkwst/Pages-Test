# Bandit Solutions 0 through 10

## Bandit 0

> **Level Goal**
>
> The password for the next level is stored in a file called **readme** located in the home 
> directory. Use this password to log into bandit1 using SSH. Whenever you find a password 
> for a level, use SSH (on port 2220) to log into that level and continue the game.

### Solution

#### The cat Command

The `cat` command is probably the most widely used command in Linux. This command can be used to read and con**cat**enate files (this feature gives the command its name), writing its contents to the standard output.

##### Displaying File Contents

The most common usage of the cat command is to read the contents of files.

For example, the following command will display the contents of the `/etc/readme.txt` file in the terminal:

```shell
# Display the contents of /etc/readme.txt file in the terminal
cat /etc/issue
```

