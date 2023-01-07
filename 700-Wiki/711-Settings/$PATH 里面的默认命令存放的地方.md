# $PATH 里面的默认命令存放的地方
5.2 PATH variable

The PATH variable is a special variable. When we type a command in the bash shell, it searches for the command in the directories mentioned, in the PATH variable. We can see the current PATH value using the echo command.

```shell
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/fedora/.local/bin:/home/
*→*fedora/bin
```

The different directories are separated by :. You can see the /home/fedora/bin directory is mentioned in the path.

This means if we have that directory, and an executable fifile is in there, we can use it as a normal command in our shell.

We will see an example of this, later in the book.