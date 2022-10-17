# What do the numbers in a man page mean

source https://unix.stackexchange.com/questions/3586/what-do-the-numbers-in-a-man-page-mean

So, for example, when I type man ls I see LS(1). But if I type man apachectl I see APACHECTL(8) and if I type man cd I end up with cd(n).

I'm wondering what the significance of the numbers in the parentheses are, if they have any.

Answer：

The number corresponds to what section of the manual that page is from; 1 is user commands, while 8 is sysadmin stuff. The man page for man itself (man man) explains it and lists the standard ones:

MANUAL SECTIONS

The standard sections of the manual include:

  

1 User Commands

2 System Calls

3 C Library Functions

4 Devices and Special Files

5 File Formats and Conventions

6 Games et. al.

7 Miscellanea

8 System Administration tools and Daemons

  

Distributions customize the manual section to their specifics,

which often include additional sections.

There are certain terms that have different pages in different sections (e.g. printf as a command appears in section 1, as a stdlib function appears in section 3); in cases like that you can pass the section number to man before the page name to choose which one you want, or use man -a to show every matching page in a row:

$ man 1 printf

$ man 3 printf

$ man -a printf

---

You can tell what sections a term falls in with man -k (equivalent to the apropos command). It will do substring matches too (e.g. it will show sprintf if you run man -k printf), so you need to use ^term to limit it:

$ man -k '^printf'

printf (1) - format and print data

printf (1p) - write formatted output

printf (3) - formatted output conversion

printf (3p) - print formatted output

printf [builtins] (1) - bash built-in commands, see bash(1)

Note that the section can sometimes include a subsection (e.g., the p in 1p and 3p above). The p subsection is for POSIX specifications; the x subsection is for X Window System documentation.

  

Other Reference:

[https://superuser.com/questions/297702/what-do-the-parentheses-and-number-after-a-unix-command-or-c-function-mean](https://superuser.com/questions/297702/what-do-the-parentheses-and-number-after-a-unix-command-or-c-function-mean)

0     Header files

0p    Header files (POSIX)

1     Executable programs or shell commands

1p    Executable programs or shell commands (POSIX)

2     System calls (functions provided by the kernel)

3     Library calls (functions within program libraries)

3n    Network Functions

3p    Perl Modules

4     Special files (usually found in /dev)

5     File formats and conventions eg /etc/passwd

6     Games

7     Miscellaneous  (including  macro  packages and conventions), e.g. man(7), groff(7)

8     System administration commands (usually only for root)

9     Kernel routines

l     Local documentation

n     New manpages