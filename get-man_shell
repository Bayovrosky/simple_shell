.\"Created by OGUNWOMOJU ADEBAYO B.
.TH HSH 27 "May 2023" "ALX" "SHELLEX - Simple Shell man page"

.SH NAME
hsh\fR \- a simple UNIX command interpreter

.SH SYNOPSIS
soda\fR [\fIfilename\fR]

.SH COPYRIGHT
hsh is Copyright (C) 202 by OGUNWOMOJU ADEBAYO B.

.SH DESCRIPTION
hsh\fR serves as a sh-compatible command language interpreter, capable of executing commands read from the standard input or from a file.

.SH ARGUMENTS
In cases where arguments remain after option processing, the first argument is assumed to be the name of a file containing shell commands. hsh reads and executes commands from this file, then terminates. The exit status of hsh is determined by the exit status of the last command executed in the script. If no commands are executed, the exit status is 0. An attempt is made to open the file in the current directory. If no file is found, the shell searches the directories in the PATH environment variable for the script.

.SH INVOCATION
Sodash is initiated with the standard input connected to the terminal, as determined by the \fIisatty(3)\fR function, allowing for interactive mode execution. Additionally, non-interactively, Sodash can be executed with command line arguments treated as the first argument.

.SH DEFINITIONS
Throughout the rest of this document, the following definitions are employed:

- \fIblank\fR: Refers to a space or tab character.

- \fIword\fR: Denotes a sequence of characters considered as a single unit by the shell, commonly known as a token.

- \fIname\fR: Represents a word consisting only of alphanumeric characters and underscores, commencing with an alphabetic character or an underscore. It is also referred to as an identifier.

- \fRcontrol operator\fR: Refers to a token that performs a control function. It encompasses symbols such as ||, &, &&, ;, and ;;.

.SH Command Execution
Upon splitting a command into words, if it results in a simple command along with an optional list of arguments, the following actions are taken:

If the command name lacks slashes, the shell attempts to locate it. In case a shell function with the same name exists, that function is invoked. If no match is found, the shell searches for it among the list of shell builtins. If a match is found, the corresponding builtin is invoked.

If the name neither corresponds to a shell function nor a builtin and lacks slashes, \hsg\fR searches each element of the \fIPATH\fR for a directory containing an executable file with that name. To remember the full pathnames of executable files, \fIhsh\fR employs a hash table. A complete search of the directories specified in the \fIPATH\fR variable is performed only if the command is not found in the hash table. If the search yields no result, the shell checks for a defined shell function named "command not found." If such a function exists, it is invoked with the original command and its arguments, and the exit status of the function becomes the exit status of the shell. If the "command not found" function is not defined, the shell displays an error message and returns an exit status of 127.

If the search is successful or the command name contains one or more slashes, the shell executes the named program in a separate execution environment. Argument 0 is set to the given name, while the remaining arguments to the command are set accordingly, if provided.

.SH Environment
\fBhsh\fR copies the environment from the parent process (where it was executed) based on the \fBBash\fR environment. The environment is represented as an array of strings containing variables in the format of name=value pairs.

During invocation, the shell scans its own environment and creates a parameter for each encountered name, automatically marking it for export to child processes. Executed commands inherit this environment. The \fBexport\fR and \fBdeclare -x\fR commands enable adding or removing parameters and functions from the environment.

.SH Exit Status
The exit status of Shellex\fR, after executing a command, is determined by the value returned by the \fBwaitpid\fR system call or an equivalent function. A command that exits with a zero status is considered successful. An exit status of zero indicates success, while a non-zero exit status signifies failure.

If a command is not found, the child process created to execute it returns a status of 127.

All builtins return zero upon successful execution and one or two in case of incorrect usage, as indicated by a corresponding error message.

.SH BUILTINS
The following builtin commands are supported:

.B env

- Prints the current environment.

.B setenv [Variable] [Value]

- Creates a new environment variable or modifies an existing one.

.B unsetenv [Variable]

- Removes an environmental variable.

.B exit [Status]

- Exits the shell.

.B cd [Directory]

- Changes the current directory of the process to DIRECTORY. If no argument is provided, the command is interpreted as cd $HOME. If the argument is "-", the command is interpreted as cd $OLDPWD. After changing the directory, the environment variables PWD and OLDPWD are updated accordingly.

.B help

- Displays a help message for builtin commands.

.SH SEE ALSO
\&access(2), chdir(2), execve(2), \&_exit(2), exit(3), fflush(3), fork(2), free(3), isatty(3), getcwd(3), malloc(3), open(2), read(2), sh(1), signal(2), stat(2), wait(2), write(2)

Shellex\fR incorporates the fundamental functionalities of the \fBsh\fR shell. This man page is based on the man page for bash(1).

.SH AUTHORS
OGUNWOMOJU ADEBAYO B.

