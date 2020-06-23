# Bandit Solutions 0 through 10
<!-- TOC -->autoauto- [Bandit Solutions 0 through 10](#bandit-solutions-0-through-10)auto    - [Bandit 0](#bandit-0)auto        - [Solution](#solution)auto            - [The cat Command])auto                - [Displaying File Contents](#displaying-file-contents)autoauto<!-- /TOC -->
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

Now, in order to get the password, we just need to display the contents of the **readme.txt** file.

```shell
# Connect to the game user using ssh
ssh bandit0@bandit.labs.overthewire.org -p 2220

# Print the contents of the file in the STDOUT
cat ./readme
```

And the password is:
*boJ9jbbUNNfktd78OOpsqOltutMc3MY1*
