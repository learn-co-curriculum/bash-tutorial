## Intro

Bash is a text-based shell for controlling your computer (or operating system). Bash is actually an acronym which stands for Bourne-Again SHell. It replaced the Bourne shell and "bashed together" the unix programs sh, csh and ksh. From it you can navigate the files on your computer and execute programs.

You can also connect to other computers and basically do everything you can do in your GUI Operating System (like OS X or Windows).

When you open a terminal, you're basically within your file system, or in a directory, just like you are when you open a Finder window or an Explorer window.

## Navigation

Open up command prompt or terminal. Type in: `pwd` and hit return.

You should see some output describing the directory you are currently within.

`/Users/avi`

*Note that avi is my username, yours will vary*

That output is describing a location on your computer. You have a file system and within that file system are directories and files.

The command `pwd` stands for print working directory.

`/User/avi` means that I am currently working within a directory `/Users` on the root of my machine, and then within that directory, a directory named `avi`.

That's my home directory. It belongs to the user I am currently logged in as. A short cut for a user's home directory is the `~` (pronounced tilde) character.

Try this:

*Note that any time you see the '$' character, you shouldn't type it in. This is just a standard way to represent a bash prompt. Yours may or may not be a '$'.*

```bash
$ cd ..
$ pwd
```

You should now see that you are one directory above where you were, in my case

`/Users`

The `cd` command stands for change directory
The `..` command stands for the directory above the working directory.

Try this:

```bash
$ cd .
$ pwd
```

You can see you are still in the same directory.

The `.` command is a shortcut for the current directory.

So here are three shortcuts within your filesystem:

- `~` Home directory
- `.` current directory
- `..` directory above

You can supply any path to the `cd` command to navigate to that location.

Try this:

```bash
$ ls
```

You should see a list of all the files within your working directory.

The command `ls` stands for "list".

Try this:

```bash
$ cd /Users/avi
$ pwd
```

The working directory is back to `/Users/avi`.

## Paths

The path supplied to the `cd` command, for example `/Users/avi`, is known as an absolute path.

Systems can use either *absolute* or *relative* paths.

An absolute path is a path that points to the same location on the file system regardless of the working directory. They start with `/` because that is the root of your file system.

This is an absolute path: `/Users/avi`.

A relative path is a path **relative** to the working directory of the user or application, so the full absolute path will not have to be given. They start with the name of a directory or a file.

This is a relative path: `avi/Documents`.

Paths use `/` to denote levels.

How many levels are within the following path?

`/Users/avi/Development/code/flatiron-school/mixtape-app`

- [The One True Path](http://blog.seldomatt.com/blog/2012/10/08/bash-and-the-one-true-path/)
- [More on paths - Wikipedia](http://en.wikipedia.org/wiki/Path_\(computing\))

Knowing where you are in your terminal - what directory you are working in - is very important.

(If you said 6 levels to the question above you are right!!)

## Commands

Another cool command you can you use is `touch`, which simply creates a new file. Try:

```bash
$ touch hello_world.rb
```

Now try:

```bash
$ ls
```

You should see the file you just created, `hello_world.rb`, in the working directory.

From within a shell you can also execute programs. Navigate to where you saved your `hello_world.rb` file and try:

```bash
$ ruby hello_world.rb
```

This command is no different than the `cd` command. We're executing the `ruby` program by supplying a path to a file to execute.

Most programs also accept flags or options for execution.

A flag is denotated by a `-`. *Note that in some programs, options are passed directly to the command, not via flags*

A common flag 99% of programs and commands accept is `h`, for help.

```bash
$ ruby -h
```

Now try:

```bash
$ ls -lah
```

What that did is add a bunch of extra formatting and output options to our `ls` command. Namely, the `l` is for a vertical list of files, the `a` is for all information, including permissions, and the `h` is for human readable formats. Notice that you can combine flags with only one `-`.

You have a lot of programs and commands available to you. Useful ones include `cat`, `ps`, and `open`.

The `open` command is interesting because it will trigger the default action associated with the file type. So `open .` will popup a finder window with the current directory in finder (because remember that `.` is an alias to the current directory). Entering `open hello_world.rb` will open that file in your default editor.

Entering `cat [file-name]` reads a file and prints the content to your command line.

Entering `ps` lists the current processes being run by your terminal.

## Tab Completion

As you type in commands you can use tab completion. Tab completion allows the shell to be smart and to try and guess what command you want to run when you hit tab.  If there's only one logical way to complete your command it will auto populate, or will show you the possibilities and you can keep typing more letters until you can tab complete your command.

For example let's say we have the following directory structure:

```bash
/flatiron_school
/flatiron_building
```

If I'm in my root directory (typing `pwd` gives me `/Users/avi`) and I type `cd f` and then hit tab, it will fill in everything up until the conflict so I'll see `cd flatiron_`.  If I then add the `s` and hit tab it will fill in `cd flatiron_school` and I can hit enter.

## Login Routine

Every time you open your terminal or a new tab, you are relogging into your shell. Your system has a login routine of things to do when you login. One of the things it does is read a file called `.bash_profile`. Try this:

```bash
$ cd ~
```

(This command moves you to your home directory). Then type:

```bash
ls -lah
```

You may or may not see a `.bash_profile` file listed. If not, don't worry. We'll make one and add some cool stuff to it later.

### Hidden Files

Type in:

```bash
ls -lah
```

Notice that at the top of the file output there are a bunch of files that start with a `.`, like `.DS_Store`

But try `open .` and just `ls`, those files, like `.DS_Store`, are not listed. That's because files that start with a `.` are hidden files. Your `.bash_profile` is a hidden file in your home directory.  If you want to see the hidden files you can add the a flag to `ls` by typing `ls -a`.

If you're interested in where this convention came from check out [The history of hidden files](https://plus.google.com/101960720994009339267/posts/R58WgWwN9jp) .

### PATH and Environment Variables

You may be wondering what the computer is actually doing when you type a command at the command line.  It's running an executable program.  But how does the computer know what to do when I type `ls whatever`?  The PATH variable gives the computer an ordered list of directories to search in to find an executable with the name you typed.  In our case, it's going to search for the `ls` executable.  If you type `ls /bin`, you'll see that this is an actual program or "binary" which is why it's usually found in the `bin` directory (short for binary).  If you're trying to run a ruby program and typing `ruby myprogram.rb` the computer goes through all the files in the path until it finds an executable called `ruby` and then runs that code with the provided argument (`myprogram.rb`).  If you type `echo $PATH` you can see what your path is.  If you're using [RVM](https://rvm.io/) (if you don't know what this is at the moment don't worry), it will look something like this:

```
/Users/blake/.rvm/gems/ruby-1.9.3-p392/bin:/Users/blake/.rvm/gems/ruby-1.9.3-p392@global/bin:/Users/blake/.rvm/rubies/ruby-1.9.3-p392/bin:/Users/blake/.rvm/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/bin:/usr/local/sbin:/Users/blake/bin:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin
```
(This code box is scrollable to the right.)

Each directory in the path is separated by the `:` (colon).

If you ever get errors where you type something in the terminal and it says it can't be found, the executable you're trying to run needs to be added to the path. If the wrong executable is getting run, the order of directories in your path is wrong.

The PATH variable is an environmental variable. These are variables you can set specific to your computer's environment which can then be used in other programs. For example, in Ruby you can type `ENV[name_of_variable]` to access an environmental variable. These are typically set in your bash profile, in a bash script, or at the command line.

**Tip:** If you want to find out where the program being run is located when you type a command at the command line, use the which command; entering `which ruby` will tell you where the Ruby binary is located.

#### `/usr, /usr/local`, `/usr/local/bin`

These directories are directories that are typically specific to an individual.

If you look in /usr/local you'll see a Cellar directory where Homebrew installs its programs.

## Random Bonus: Piping |

Piping, a verb derived from the `|` symbol named "pipe", will send the output of one command into the input of another command.
The most common command you'll probably use is piping the process list to [grep](http://en.wikipedia.org/wiki/Grep) to search for a running program.

`ps aux | grep ruby`

This would run the `ps` command with the `a`, `u`, and `x` flags and send the output of that to `grep` (a search utility) which would then search for the term "ruby".

## More Resources:

- [Lifehacker on the Command Line](http://lifehacker.com/5633909/who-needs-a-mouse-learn-to-use-the-command-line-for-almost-anything)
- [Environment Variables](http://cbednarski.com/articles/understanding-environment-variables-and-the-unix-path/)
- [Built-in Shell Commands](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html) *Very useful*
- [15 Useful Bash Commands](http://www.thegeekstuff.com/2010/08/bash-shell-builtin-commands/)
