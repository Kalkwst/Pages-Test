---
title: Over The Wire - Useful Commands 
published: false
description: 
tags: 
//cover_image: https://direct_url_to_image.jpg
---

<!-- TOC depthTo:2 -->

- [The cat Command](#the-cat-command)
- [The ls Command](#the-ls-command)
- [The find Command](#the-find-command)
- [The grep Command](#the-grep-command)
- [The sort Command](#the-sort-command)

<!-- /TOC -->

## The cat Command

The `cat` command is a command line utility for con*cat*tenating files and displaying to the standard output. It can be used to show the contents of a file in the terminal, to write the contents of one file to another, and to combine multiple files into one. It also supports adding line numbers, diplaying special characters and squeezing blank lines.

### How to show the contents of a file

In order to show the contents of a file using `cat` simply pass the name of the file or files you want to view. The contents will be displayed in the standard output and viewable in the terminal. 

The following, displays the contents of the `foo.txt` file:

```shell
cat foo.txt
Hello world!
```

If the contents of a file are very long, the output can be piped (using the pipe operator `|`) through a `less` command. This will display the contents one screenful at a time.

If some specific word or pattern is required, then the [grep](#the-grep-command) can be used using piping.

### How to write the contents of a file to a new file

To write the content of a file to a new file, shell redirection can be used with the `cat` tool. In this case, we are going to use the *output redirection operator*. In the following example, the `foo.txt` file is written into `bar.txt`.

```shell
cat foo.txt > bar.txt
cat bar.txt
Hello World!
```

This will **overwrite** the contents of the `bar.txt` file.

Also, if `bar.txt` does not exist, then the command will create it.

### How to append the contents of a file to another file

To append the contents of one file to another file, we are going to once again use shell redirection. In this case, we are going to use the *append operator*. In the following example, there are two files, `wine.txt` and `beer.txt`.

The `wine.txt` file contains two lines:

```shell
cat wine.txt
Syrah
Chardonnay
```

The `beer.txt` file contains two lines:

```shell
cat beer.txt
Porter
India Pale Ale
```

The `cat` tool can be used with shell redirection to write the contents of one file to the end of another

```shell
cat wine.txt >> beer.txt
cat beer.txt

Syrah
Chardonnay
Porter
India Pale Ale
```

### How to combine multiple files into one

To combine multiple files into one, `cat` can once more be used with shell redirection.

The following will combine `file1.txt`, `file2.txt` and `file3.txt` into `file4.txt`:

```shell
cat file1.txt file2.txt file3.txt > file4.txt
```

It is also possible to use wildcards for that. The following will combine all files with the `.txt` extension in a directory into one file.

```shell
cat *.txt > combined.txt
```

## The ls Command

The `ls` command is a command-line utility for listing the contents of a directory or directories given to it via standard input. It writes results to standard output. The `ls` command supports showing a variety of information about files, sorting on a range of options and recursive listing.

### How to display the contents of a directory

To show the contents of a directory pass the directory name to the `ls` command. This will list the contents of the directory in alphabetical order. If your terminal supports colors you may see the file and directory listings are a different color.

```shell
ls /home/agathoklis
bin     code     dotfiles     Downloads     irc     logs     src
```

### How to display hidden files and folders

To show hidden files and folders pass the `-a` option to `ls`:

```shell
ls -a
.  ..  .bash_logout  .bashrc  .profile  readme
```

### How to append file types to listings

To append an indicator of the file type to a directory listing pass the `-F` option:

```ls
ls -F
bin@    dotfiles/   file.txt    irc/    src/
code/   Downloads/  logs/
```

The following characters are appended based on this option:

- `@` means symbolic link (or that the file has extended attributes).
- `*` means executable.
- `=` means socket.
- `|` means named pipe.
- `>` means door.
- `/` means directory.

### How to sort by size

To sort a directory listing by name pass the `-S` option. In the following example, this is combined with the `-l` option to show a long listing.

```shell
ls -lS
total 56
rwxr-xr-x  2  agathoklis users 32768 Oct  4 09:15 logs
drwxr-xr-x  6 agathoklis users  4096 Oct  4 20:27 code
drwxr-xr-x 10 agathoklis users  4096 Oct  4 09:13 dotfiles
drwx------  3 agathoklis users  4096 Oct  4 11:31 Downloads
drwxr-xr-x  5 agathoklis users  4096 Sep 25 08:30 go
drwx------  3 agathoklis users  4096 Sep 27 10:49 irc
drwxr-xr-x  8 agathoklis users  4096 Oct  2 17:13 src
lrwxrwxrwx  1 agathoklis users    25 Sep 22 14:17 bin -> /home/agathoklis/dotfiles/bin
-rw-r--r--  1 agathoklis users     0 Oct  4 20:42 file.txt
```

### How to sort by modification time

To sort by modification time pass the `-t` option. This will show the most recently modified files or folders at the top of the listing. In the following example, this is combined with the `-l` option to show a long listing.

```shell
ls -lt
total 56
-rw-r--r--  1 agathoklis users     0 Oct  4 20:42 file.txt
drwxr-xr-x  6 agathoklis users  4096 Oct  4 20:27 code
drwx------  3 agathoklis users  4096 Oct  4 11:31 Downloads
drwxr-xr-x  2 agathoklis users 32768 Oct  4 09:15 logs
drwxr-xr-x 10 agathoklis users  4096 Oct  4 09:13 dotfiles
drwxr-xr-x  8 agathoklis users  4096 Oct  2 17:13 src
drwx------  3 agathoklis users  4096 Sep 27 10:49 irc
drwxr-xr-x  5 agathoklis users  4096 Sep 25 08:30 go
lrwxrwxrwx  1 agathoklis users    25 Sep 22 14:17 bin -> /home/agathoklis/dotfiles/bin
```

### How to sort by access time

To sort by access time pass the `-u` option. This causes the output to show the most recently accessed files of folders at the top of the listing. In the following example, this is combined with the `-l` option to show a long listing.

```shell
ls -lu
total 56
lrwxrwxrwx  1 agathoklis users    25 Oct  4 09:01 bin -> /home/agathoklis/dotfiles/bin
drwxr-xr-x  6 agathoklis users  4096 Oct  4 20:23 code
drwxr-xr-x 10 agathoklis users  4096 Oct  4 11:21 dotfiles
drwx------  3 agathoklis users  4096 Oct  4 11:24 Downloads
-rw-r--r--  1 agathoklis users     0 Oct  4 20:42 file.txt
drwxr-xr-x  5 agathoklis users  4096 Sep 26 16:46 go
drwx------  3 agathoklis users  4096 Oct  4 09:38 irc
drwxr-xr-x  2 agathoklis users 32768 Oct  4 09:15 logs
drwxr-xr-x  8 agathoklis users  4096 Oct  2 17:12 src
```

### How to show file size in a human-readable format

```shell
ls -lh
total 4.0K
-rw-r----- 1 bandit1 bandit0 33 May  7 20:14 readme
```

### How to show a recursive listing

To display a recursive listing pass the `-R` option. This causes folders and files within a folder to be listed.

```shell
ls -R tree
tree:
file.txt    folder1     folder2

tree/folder1:
file.txt

tree/folder2:
```

## The find Command

The `find` command is a command-line utility for walking a file hierarchy. It can be used to find files and directories and perform subsequent operations on them. It supports searching by file, folder name, creation date, modification date, owner, and permissions.

Furthermore, by using the `-exec` option, other UNIX commands can be executed on files or folders found.

### How to find a single file by name

To find a single file by name pass the `-name` option to `find` along with the name of the file you are looking for.

Suppose that the following directory structure exists, as the output of a `tree` command.

```shell
foo
├── bar
├── baz
│   └── foo.txt
└── bop
```

The file `foo.txt` can be located with the `find` command by using the `-name` option.

```shell
find ./foo -name foo.txt
./foo/baz/foo.txt
```

### How to find a directory

To find a directory specify the option `-type d` with `find`.

```shell
find ./foo -type d -name bar
./foo/bar
```

### How to find files by permission

To find files by permission use the `-perm` option and pass the value you want to search for. The following example will find files that everyone can read, write and execute.

```shell
find ./foo -perm 777
```

### How to find a file owned by a specific user

To find files owned by a specific user, use the `-user` option and pass the value you want to search for. The following example will find files owned by the user `agathoklis`.

```shell
find ./foo -user agathoklis
```

It is possible to search for several users using the `-o` option between each user. The following example will find files owned by the user `agathoklis` or the user `agisilaos`.

```shell
find ./foo -user agathoklis -o -user agisilaos
```

### How to find a file owned by a specific group

To find files owned by a specific group, use the `group` option and pass the value you want to search for. The following example will find files owned by the group `ftpusers`.

```shell
find ./foo -group ftpusers
```

### How to find and operate on files

To find and operate on a file, use the `-exec` option. This will allow a command to be executed on files that are found.

```shell
find ./foo -type f -name bar -exec chmod 777 {} \;
```

Another use of combining `find` with `exec` is to search for text within multiple files

```shell
find ./foo -type f -name "*.txt" -exec grep 'foo' {} \;
```

## The grep Command

The `grep` command in UNIX is a command line utility for printing lines that match a pattern. It can be used to find text in a file and search a directory structure of files recursively. It also supports showing the context of a match by showing lines before and after the result and has support for regular expressions in pattern matching.

### How to find text in a file

To find text in a file pass the strings you are looking for to `grep` followed by the name of the file or files.

The `grep` tool will print occurrences that it finds to standard output.

### How to list line numbers for matches

To list line numbers and file names pass the `-n` option to grep. This prints matches to standard output along with the line number it was found on.

```shell
grep 'computer' -n /usr/share/dict/words
40565:computer
```

### How to print lines before and after a match

To print lines before and after a match the `-A` and `-B` options can be used. `-B` option refers to the lines before the match, and the `-A` option refers to the lines after the match. Both expect a number and will print this number of lines.

```shell
grep -B 2 -A 2 'computer' /usr/share/dict/words
computativeness
compute
computer
computist
computus
```

A further option is available in `-C` that will print the context of the match. This is equivalent to using both `-A` and `-B`.

```shell
grep -C 2 'computer' /usr/share/dict/words
computativeness
compute
computer
computist
computus
```

### How to count the number of matches

To count the number of matches use the `-c` option. This outputs a number count to standard output.

```shell
grep -c 'comput*' /usr/share/dict/words
50
```

### How to print the filename for a match

To print the filename for a match use the `-H` option. This is automatically invoked when `grep` is given more than one file to search.

```shell
grep -H 'computer' /usr/share/dict/words
/usr/share/dict/words:computer
```

### How to search recursively

To search a pattern recursively, use the `-R` option. This will search through all files in the directory tree that you have permission to read.

```shell
grep -R 'passwd' /etc
/etc/pam.d/su:# NIS (man nsswitch) as well as normal /etc/passwd and
/etc/pam.d/chpasswd:# The PAM configuration file for the Shadow 'chpasswd' service
```

### How to search for the inverse of a pattern
To searcdh for the inverse of a pattern use the `-v` option. This will print inverse matches to standard output.

```shell
grep -v 'computer' /usr/share/dict/words
A
a
aa
aal
....
```

### How to ignore case when searching

To ignore the case when searching use the `-i` option. By default `grep` will respect case.

```shell
grep 'COMPUTER' /usr/share/dict/words
# no match

grep -i 'COMPUTER' /usr/share/dict/words
computer
```

### How to use basic regular expressions when searching

To use basic regular expressions all versions of `grep` support basic character matches. In the following example the pattern matches `'ia'` characters at the end of the line.

```shell
grep 'ia$' /usr/share/dict/words
abasia
Abelia
abepithymia
...
```

### How to use extended regular expressions when searching

To use extended regular expressions use the `-e` option. The following line matches lines that do not contain the words `'foo'` or `'bar'`.

```shell
grep -v -e 'foo' -e 'bar'
```

Note that in the GNU version of `grep` there is no difference in available functionality between basic and extended syntaxes.

## The sort Command

The `sort` command is a command line utility for sorting lines of text files. It supports sorting alphabetically, in reverse order, by number, by month and can also remove duplicates. The sort command can also sort by items not at the beginning of the line, ignore case sensitivity and return whether a file is sorted or not.

### How to sort alphabetically

The `sort` tool will sort lines alphabetically by default. Running `sort filename` writes the contents of the `filename` in alphanetical order to standard output.

Suppose a file exists with the following list of metal bands that needs to be sorted in alphabetical order. The file is saved as `bands.txt`.

```
Motörhed
AC/DC
Sepultura
Carcass
Opeth
Below The Bottom
```

The `sort` command allows us to sort the file alphabetically.

```shell
sort bands.txt
AC/DC
Below The Bottom
Carcass
Motörhead
Opeth
Sepultura
```

### How to sort in reverse order

To sort in reverse order pass the `-r` option to `sort`. This will sort in reverse order and write the results to standard output.

Using the same list of metal bands from the previous example this file can be sorted in reverse order with the `-r` option.

```shell
sort -r bands.txt
Sepultura
Opeth
Motörhed
Carcass
Below The Bottom
AC/DC
```

### How to sort mixed-case text

To sort mixed-case text pass the `-f` option to `sort`. This will ignore case sensitivity when sorting and write the result to standard output.

If a file has uppercase and lowercase content `sort` will order uppercase first.
Suppose a file exists with a list of names in a file called `names.txt`.

```
Sam
sally
Sarah
steven
```

By default the `sort` tool will sort uppercase characters first.

```shell
sort names.txt
Sam
Sarah
sally
steven
```

To sort and ignore case use the `-f` option.

```shell
sort -f names.txt
sally
Sam
Sarah
steven
```

### How to check if a file is already sorted

To check if a file is already sorted, pass the `-c` option to `sort`.  This will write to standard output if there are lines that are out of order.

Suppose a file exists wit a list of cars called `cars.txt`.

```
Audi
Cadillac
BMW
Dodge
```

The `sort` tool can be used to understand if this file is sorted and which lines are out of order.

```shell
sort -c cars.txt
sort: cars.txt:3: disorder: BMW
```

If there is no output then the file is considered to be already sorted.

### How to sort and remove duplicates

To sort and remove duplicates pass the `-u` option to `sort` This will write a sorted list to standard output and remove duplicates.

Suppose a file exists with a list of breakfast cereals to sort. This file contains a number of duplicates. This is saved in the file `breakfast.txt`.

```
Cornflakes
Sultana Bran
Weetabix
Sultana Bran
Cornflakes
Shredded Wheat
Cherrios
Weetabix
```

By using the `-u` option this file can be sorted and stripped of duplicates.

```shell
sort -u breakfast.txt
Cherrios
Cornflakes
Shredded Wheat
Sultana Bran
Weetabix
```

