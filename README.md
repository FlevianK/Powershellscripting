# Powershellscripting
This repo holds my powershell learning scripts

# 10 fundamental concepts for PowerShell scripting
## 1. Psl files
Powershell files are simple text files containing Powershell commands, each command written in a new line. They use the `.psl` extention.
## 2. Execution polices
Powershell enforces a policy to prevent malicous scripts from being executed.
**There are 4 types of policies that one can enforces depending on the one's needs**
* `Restricted` - Does not allowed any script to be executed. It is the default setting.
* `RemoteSigned` - It only allows scripts written locally to be executed, the downloaded cannot be executed.
* `AllSigned` - Allows scripts signed by trusted publishers to be executed
* `Unrestricted` - Allows all scripts to be run, despite their origin or whether they are signed
## 3.  Running a script
If you are not on the folder containing the script, you have to type the full path of the script for it to be executed e.g  
```psl 
C:\users\scripts\scriptname.pls
```
If you are in the script’s folder, type 
```psl
.\scriptname.psl
``` 
The execution happens on the command line.
## 4. Pipelining
Pipeline (`|`) is used to feed output of one command to be the input of the next command. 	
For instance, If you want to get a list of processes in an orderly manner, will have to get the processes and pass the through sorting command as follows: 
```psl
Get-Process | Sort-Object ID
```
## 5. Variables
It is used when the output of a certain command or multiple comands is needed to be used
later. To store an out of a single command: 
```psl
    $a = Get-process 
```
And to store the output of multple commands:
```psl
     $a = (Get-Process | Sorted-Object ID)
```
$a is the name of the variable, to print or call it it just type 
```psl
$a
```
## 6. The @ symbol
It is used to turn the content of list into an array, used as follows:
```psl
$procs = @{name=”explorer”, “svchost”}
```
It can also be used to ensure a variable is treated as an array not a single value. For example, get the number of processes used by the window exporer and svchost: 
```psl
Get-Process $procs
```
## 7. Split
Split operater split a text string based on the character designated. For instance, 
```psl
“Hello Flevian Kanaiza, how are you doing” -split” “
```
The results will be:
```psl
    	Hello
    	Flevian
    	Kanaiza,
    	how
    	are 
    	you 
    	doing
```
## 8. Join
Join operator combine a multplie block of texts into one. For instance, 
```psl
“Kanaiza”, “Flevian”, “where”, “are”, “you?”  -join” ”
```
will be: 
```psl
Kanaiza Flevian where are you?
```
## 9. Breakpoints
It helpful for testing newly written by breaking at specified line to avoid encountering bugs or when you want to break a script when variable content changes. Examples:
```psl
New-PSBreakpoint -Script C:\Scripts\Script.ps1 -Line 4
```
Or 
```psl
New-PSBreakpoint -Script C:\scripts\Script.ps1 -variables a
```
When using varaiable on the command line dollar is not supposed to be included.  `New`, `Get`, `Enable`, `Disable` and `Remove` are verbs that can be used by PSBreakpoint
## 10. Step
It is useful for debugging newly written scripts. Using `step`, script will be executed line by line hence avoiding running into bugs that might take alot of time to debug.
**Commands to be used:**
* `Step-Into cmdlet` - This causes the script to stop at every line regardless whether breakpoint exits.
* `Step-Out cmdlet` - Stops the window from stepping through the script.
* `Step-Over cmdlet` -Is used when the script contains function and you want the whole function to executed without windows stepping at every line in the function.