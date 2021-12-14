# Linux-Interactive-Shell
Interactive Linux shell with the following functionalities-:


This unix type shell will read commands from the user and execute them appropriately. There are two types of commands that can be expected from the user : 
a user-defined command and a system-command. The following are the specifications for the project. For each of the requirement the appropriate example is given along with it.

Specification -1 : Display requirement

When you execute your code a shell prompt of the following form must appear:

<username@system_name:curr_dir>.

E.g., <daksh@iitjammu:~>

The directory from which the shell is invoked will be the home directory of the shell and should be indicated by "~"

If the user executes "cd" change dir then the corresponding change must be reflected in the shell as well.

E.g., ./a.out
<daksh@iitjammu:~>cd newdir
<daksh@iitjammu:~/newdir>

Specification -2 :  User-defined commands

The following commands must be supported by the shell
-pid : prints the process id of your shell program

E.g., 
<daksh@iitjammu:~>pid
command name: ./a.out  process id: 234

-pid current : prints the list of the process ids of the processes that are created by the shell and currently active
<daksh@iitjammu:~>pid current
List of currently executing processes spawned from this shell:
command name: emacs   process id: 235
command name: xbiff   process id: 448
command name: xcalc   process id: 459

-pid all : prints the list of process ids of all commands that were executed so far by the shell (including the currently executing processes)

E.g.,
<daksh@iitjammu:~>pid current
List of all processes spawned from this shell:
command name: ls      process id : 112
command name: cd      process id : 124
command name: emacs   process id : 235
command name: xbiff   process id : 448
command name: xcalc   process id : 459



-HISTN: list of last "N" commands executed by the shell. If the number of commands is less than "n" then the shell should print only the available number of commands. 

E.g.,
<daksh@iitjammu:~>HIST5 (Say print last 5 commands assuming the above history of commands)

1. emacs
2. xbiff
3. xcalc
4. vi
5. ps


-!HISTN : execute history command number "n" (assuming the first command is numbered 1)

E.g.,
<daksh@iitjammu:~>!HIST4 (assuming above history of commands)
vi


-!HIST(N1, N2, N3...)

Execute in order the commands with numbers N1, N2 and N3 (or more)

-Retain existing support for EXEC, HISTORY FULL, HISTORY BRIEF


Notes
1. Handle all special cases like: HIST HIST, or !HIST (without proper command number), etc, with grace.
2. No segmentation faults when arguments are missing or improperly specified, e.g., !HIST_ABC (alphabets instead of numbers)



Specification 5:  General notes

1. Use exec family of commands to execute system commands. If the command cannot be run or returns an error it should be handled approiately. Look at perror.h for appropriate routines to handle errors.

2. Use fork() for creating child processes where needed and wait() for handling child processes

3. Use signal handlers to process signals from exiting background processes. Marks will be deducted if proper signal handling is not done.

4. You can use : uname, hostname, whomai commands to get the shell display working.  For respective header libraries use: man <cmd>

5. The user can type the command anywhere in the command line i.e., by giving spaces, tabs etc. Your shell should be able to handle such scenarios appropriately. 

6. Use pipe, dup, dup2, wait(), exit(status) for handling IPC of child and parent.

7. Segmentation faults at the time of grading will be penalized.

8.System commands with and without arguments in foreground or background

All other commands (other than what user-defined commands like HIST) are treated as system commands like : ls, emacs, vi and so on.
 The shell must be able to execute them either in the backgroud or in the foreground.

--Foreground processes: For example, executing a "vi" command in the foreground implies that your shell will wait for this process to complete and regain control when this process exits.

--Background processes: Any command invoked with "&" is treated as background command. This implies that your shell will spawn that process and doesn't wait for the process to exit.
 It will keep taking user commands. If the background process  exits then the shell must display the appropriate message to the user.

