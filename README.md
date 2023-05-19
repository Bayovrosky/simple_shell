**Shellex**: An Elegant Shell Program :shell:

Experience the simplicity of **Shellex**, a UNIX command interpreter developed as part of ALX's low-level programming and algorithm track.

## Overview :speech_balloon:

**Shellex** serves as a user-friendly UNIX command language interpreter that efficiently processes commands from various sources and executes them flawlessly.

### Invocation :rocket:

Usage: **shellex** [filename]

To activate **Shellex**, simply compile all the `.c` files within the repository and execute the resulting binary:

```
gcc *.c -o shellex
./shellex
```

**Shellex** is versatile and can be invoked in both interactive and non-interactive modes. In the absence of a connected terminal, it dutifully reads and executes commands received in the specified order.

Example:
```
$ echo "echo 'hello'" | ./shellex
'hello'
$
```

For an interactive experience, when **Shellex** is invoked with a standard input connected to a terminal (determined by [isatty](https://linux.die.net/man/3/isatty)(3)), it opens an *interactive* shell. In interactive mode, **Shellex** waits for user input and displays the `$ ` prompt to indicate its readiness to receive a command.

Example:
```
$./shellex
$
```

Alternatively, if command line arguments are provided during invocation, **Shellex** treats the first argument as a file containing a sequence of commands. Each command should occupy a separate line within the file. **Shellex** executes the commands in the order specified and then exits.

Example:
```
$ cat test
echo 'hello'
$ ./shellex test
'hello'
$
```

### Environment :deciduous_tree:

Upon activation, **Shellex** inherits and replicates the environment from its parent process. This environment consists of an array of *name-value* string pairs, representing variables in the format *NAME=VALUE*. Notable environmental variables include:

#### HOME
The home directory of the current user and the default directory argument for the **cd** builtin command.

```
$ echo "echo $HOME" | ./shellex
/home/vagrant
```

#### PWD
The present working directory, as set by the **cd** command.

```
$ echo "echo $PWD" | ./shellex
/home/vagrant/ALX/simple_shell
```

#### OLDPWD
The previous working directory, as set by the **cd** command.

```
$ echo "echo $OLDPWD" | ./shellex
/home/vagrant/ALX/printf
```

#### PATH
A collection of directories, separated by colons, in which the shell looks for executable commands. An empty directory name in the **PATH** (indicated by two consecutive colons, an initial colon, or a trailing colon) signifies the current directory.

```
$ echo "echo $PATH" | ./shellex
/home/vagrant/.cargo/bin:/home/vagrant/.local/bin:/home/vagrant/.rbenv/plugins/ruby-build/bin:/home/vagrant/.rbenv/shims:/home/vagrant/.rbenv/bin:/home/vagrant/.nvm/versions/node/v10.15.3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/vagrant/.cargo/bin:/home/vagrant/workflow:/home/vagrant/.local/bin
```

### Command Execution :thumbsup:

Upon receiving a command, **Shellex** intelligently tokenizes it into separate words using a space (" ")

### Remarkable Comments :hash:

**Shellex** possesses a unique capability to handle comments, disregarding any words or characters preceding a `#` symbol on a line.

Example:
```
$ echo "echo 'hello' #this will be completely ignored!" | ./shellex
'hello'
```

### Special Operators :guitar:

**Shellex** boasts special interpretation of the following operator characters:

#### ; - Command Terminator
Commands separated by a `;` symbol are executed sequentially, one after another.

Example:
```
$ echo "echo 'hello' ; echo 'world'" | ./shellex
'hello'
'world'
```

#### && - Logical AND Operator
The `command1 && command2` expression executes `command2` only if `command1` returns an exit status of zero (indicating success).

Example:
```
$ echo "error! && echo 'hello'" | ./shellex
./shellex: 1: error!: not found
$ echo "echo 'all good' && echo 'hello'" | ./shellex
'all good'
'hello'
```

#### || - Logical OR Operator
The `command1 || command2` expression executes `command2` only if `command1` returns a non-zero exit status (indicating failure).

Example:
```
$ echo "error! || echo 'but still runs'" | ./shellex
./shellex: 1: error!: not found
'but still runs'
```

Both `&&` and `||` operators hold equal precedence, followed by `;`.

### Essential Builtin Commands of shellex :nut_and_bolt:

#### cd
  * Usage: `cd [DIRECTORY]`
  * Modifies the current process directory to `DIRECTORY`.
  * If no argument is provided, the command is interpreted as `cd $HOME`.
  * If the argument `-` is given, the command is interpreted as `cd $OLDPWD`, and the path of the new working directory is printed to standard output.
  * If the argument `--` is given, the command is interpreted as `cd $OLDPWD`, but the path of the new working directory is not displayed.
  * The environment variables `PWD` and `OLDPWD` are updated after a directory change.

Example:
```
$ ./shellex
$ pwd
/home/vagrant/ALX/simple_shell
$ cd ../
$ pwd
/home/vagrant/ALX
$ cd -
$ pwd
/home/vagrant/ALX/simple_shell
```

#### alias
  * Usage: `alias [NAME[='VALUE'] ...]`
  * Manages aliases within the shell.
  * `alias`: Prints a list of all aliases, with each alias displayed on a separate line in the format `NAME='VALUE'`.
  * `alias NAME [NAME2 ...]`: Prints the aliases `NAME`, `NAME2`, etc., with each alias displayed on a separate line in the format `NAME='VALUE'`.
  * `alias NAME='VALUE' [...]`: Defines an alias for each `NAME` specified, with its corresponding `VALUE`. If `NAME` already exists as an alias, its value is replaced with the new `VALUE`.

Example:
```
$ ./shellex
$ alias show=ls
$ show
AUTHORS            builtins_help_2.c  errors.c         linkedlist.c        shell.h       test
README.md          env_builtins.c     getline.c        locate.c            shellex
alias_builtins.c   environ.c          helper.c         main.c              split.c
builtin.c          err_msgs1.c        helpers_2.c      man_
```

### New Configuration :gear:

#### Goodbye
  * Usage: `goodbye [CODE]`
  * Terminates the shell.
  * The optional `CODE` argument specifies the exit status of the shell.
  * If no argument is provided, the command is interpreted as `goodbye 0`.

Example:
```
$ ./shellex
$ goodbye
```

#### environment
  * Usage: `environment`
  * Displays the current environment settings.

Example:
```
$ ./shellex
$ environment
NVM_DIR=/home/vagrant/.nvm
...
```

#### config
  * Usage: `config [VARIABLE] [VALUE]`
  * Configures a new shell variable or modifies an existing one.
  * Prints an error message to `stderr` if unsuccessful.

Example:
```
$ ./shellex
$ config NAME Poppy
$ echo $NAME
Poppy
```

#### deleteconfig
  * Usage: `deleteconfig [VARIABLE]`
  * Removes a shell variable.
  * Prints an error message to `stderr` if unsuccessful.

Example:
```
$ ./shellex
$ config NAME Poppy
$ deleteconfig NAME
$ echo $NAME

$
```

## Creators :black_nib:

* **Ogunwomju Adebayo** **||** [Github](https://github.com/Bayovrosky) **|** [Twitter](https://twitter.com/Bayovrosky) **|** [Email](aoluwatosin00@gmail.com)  
* Unavailable

## Acknowledgments :pray:

**shellex** is designed to replicate fundamental features of the **sh** shell. This README draws inspiration from the Linux man pages [sh(1)](https://linux.die.net/man/1/sh) and [dash(1)](https://linux.die.net/man/1/dash).

The creation of this project is a part of the ALX-SE curriculum at Holberton School. Holberton School is a campus-based full-stack software engineering program that prepares students for careers in the tech industry through project-based peer learning. For more information about ALX, please visit [this link](https://www.alxafrica.com/).


