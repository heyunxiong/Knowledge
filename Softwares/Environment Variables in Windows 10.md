# Environment Variables in Windows 10 | Tutorials
https://www.tenforums.com/tutorials/3234-environment-variables-windows-10-a.html

Complete List of Environment Variables in Windows 10
Environment variables are a set of dynamic named values that can affect the way running processes will behave on a computer. The variables can be used both in scripts and on the command line. Environment variables makes it easy when certain standard directories and parameters need to be referenced but where the actual locations or names can vary from computer to computer.
The variable (ex: "%UserProfile%") is used as a type of shortcut of the value (ex: "C:\Users\<username>").
There are two types of environment variables: user environment variables (set only for current user) and system environment variables (set for all users).
This tutorial will show you a complete list of default environment variables that can be used to reference standard directories and parameters in Windows 10.

User environment variables are stored in the registry key below:
HKEY_CURRENT_USER\Environment
System environment variables are stored in the registry key below:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment
You can open a command prompt, type set, and press Enter to display all current environment variables on your PC.
You can open PowerShell, type Get-ChildItem Env:, and press Enter to display all current environment variables on your PC.