**Command Line and the Unix Shell**
===================================

**Setup**
=========
You need to download some files to follow this lesson:

Download `data-shell.zip <http://swcarpentry.github.io/shell-novice/data/data-shell.zip>`_ and move the file to your Desktop.


Unzip/extract the file. You should end up with a new folder called data-shell on your Desktop.

Open a terminal and type cd, then press the Enter key. 

That last step will make sure you start with your home folder as your working directory.
In the lesson, you will find out how to access the data in this folder.

`Instructions on how to identify a Unix Shell program and open a new a shell <http://swcarpentry.github.io/shell-novice/setup.html>`_


**Background**
==============
At a high level, computers do four things:

- run programs
- store data
- communicate with each other, and
- interact with us

The graphical user interface (GUI) is the most widely used way to interact with personal computers. We give instructions (to run a program, to copy a file, to create a new folder/directory) with the convenience of a few mouse clicks. This way of interacting with a computer is intuitive and very easy to learn. But this way of giving instructions to a computer scales very poorly if we are to give a large stream of instructions even if they are similar or identical. 

For example if we have to copy the third line of each of a thousand text files stored in thousand different folders/directories and paste it into a single file line by line. Using the tradition GUI approach of clicks will take several hours to do this.

This is where we take advange of the shell - a command-line interface to make such repetitive tasks automatic and fast. It can take a single instruction and repeat it over as it is or with some modification as many times as we want. The task in the example above can be accomplished in a few minutes at most.

The heart of a command-line interface is a read-evaluate-print loop (REPL). It is called so because when you type a command and press **Return** (also known as **Enter**) the shell reads your command, evaluates (or “executes”) it, prints the output of your command, loops back and waits for you to enter another command.

The Shell
~~~~~~~~~
The Shell is a **program which runs other programs** rather than doing calculations itself. Those programs can be as complicated as a climate modeling software and as simple as a program that creates a new folder/directory. **The simple programs which are used to perform stand alone tasks are usually refered to as commands.** The most popular Unix shell is Bash, (the Bourne Again SHell — so-called because it’s derived from a shell written by Stephen Bourne). **Bash** is the default shell on most modern implementations of Unix and in most packages that provide Unix-like tools for Windows.

What does it look like?
A typical shell window looks something like:

|shelllooklike|


The **first line** shows only a prompt, indicating that the shell is waiting for input. Your shell may use different text for the prompt. Most importantly: when typing commands, either from these lessons or from other sources, do not type the prompt, only the commands that follow it.

The part that you type, ls -F / in the second line of the example, typically has the following structure: a command, some options (also called switches or flags) and an argument. Flags start with a single dash (-) or two dashes (--), and change the behaviour of a command. Arguments tell the command what to operate on (e.g. files and directories). Sometimes options and arguments are referred to as parameters. A command can be called with more than one option and more than one argument: but a command doesn’t always require an argument or an option.

In the **second line** of the example above, our **command is ls**, with an **option -F** and an **argument /**. **Each part is separated by spaces**: if you omit the space between ls and -F the shell will look for a command called ls-F, which doesn’t exist. Also, **capitalization matters**: LS is different from ls.

Next we see the **output** that our command produced. In this case it is a listing of files and folders in a location called / - we’ll cover what all these mean later today. Those using a macOS might recognize the output in this example.

**Finally**, the shell again prints the prompt and waits for you to type the next command.


Open a shell window and try executing ls -F / for yourself (don’t forget that spaces and capitalization are important!). 

.. code-block::

    ls -F /
    
Now try

.. code-block::

    ls-F
    $ ls-F: command not found

Usually this means that you have mis-typed the command - in this case we omitted the space between ls and -F.

**To re-enter the same command again use the up arrow to display the previous command. Press the up arrow twice to show the command before that (and so on).**

**Navigating Files and Directories**
====================================
File System
~~~~~~~~~~~
The part of the operating system responsible for managing files and directories is called the file system. It organizes our data into **files, which hold information**, and **directories (also called “folders”), which hold files or other directories.**

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, we’ll go to our open shell window.

First let’s find out where we are by running a command called **pwd** (which stands for “**print working directory**”). Directories are like places - at any time while we are using the shell we are in exactly one place, called our current working directory.** Commands mostly read and write files in the current working directory**, i.e. “here”, so knowing where you are before running a command is important. pwd shows you where you are:

.. code-block::

    $ pwd
    /Users/nelle

Here, the computer’s response is /Users/nelle, which is Nelle’s home directory.

.. Note::

    Home Directory Variation
    The home directory path will look different on different operating systems. On Linux it may look like /home/nelle, and on Windows it will be similar to C:\Documents and Settings\nelle or C:\Users\nelle. (It may look slightly different for different versions of Windows.) In future examples, we’ve used Mac output as the default - Linux and Windows output may differ slightly, but should be generally similar.

To understand what a “home directory” is, let’s have a look at how the file system as a whole is organized. For the sake of this example, we’ll be illustrating the filesystem on our scientist Nelle’s computer. After this illustration, you’ll be learning commands to explore your own filesystem, which will be constructed in a similar way, but not be exactly identical.

On Nelle’s computer, the filesystem looks like this:

|TheFileSystem|

At the top is the **root directory** that holds everything else. We refer to it using a slash character, **/**, on its own; this is the leading slash in /Users/nelle.

Inside that directory are several other directories: 

- **bin** (which is where some built-in programs are stored)
- **data** (for miscellaneous data files)
- **Users** (where users’ personal directories are located)
- **tmp** (for temporary files that don’t need to be stored long-term)

We know that our current working directory /Users/nelle is stored inside /Users because /Users is the first part of its name. Similarly, we know that /Users is stored inside the root directory / because its name begins with /.

.. Note::
    There are two meanings for the / character. When it appears at the front of a file or directory name, it refers to the root directory. When it appears inside a name, it’s just a separator.

Underneath /Users, we find one directory for each user with an account on Nelle’s machine, her colleagues imhotep and larry.

|HomeDirectories|

The user Imhotep’s files are stored in /Users/imhotep, user Larry’s in /Users/larry, and Nelle’s in /Users/nelle. Because Nelle is the user in our examples here, this is why we get /Users/nelle as our home directory.

Typically, when you open a new command prompt you will be in your home directory to start.

Now let’s learn the command that will let us see the contents of our own filesystem. We can see what’s in our home directory by running **ls**, which stands for “**listing**”:

.. code-block:: 

    $ ls
    Applications Documents    Library      Music        Public
    Desktop      Downloads    Movies       Pictures
    
Your results may be slightly different depending on your operating system and how you have customized your filesystem.

**ls prints the names of the files and directories in the current directory**. We can make its output more comprehensible by using the **option -F** (also known as a switch or an option) , which tells ls to add a marker to file and directory names to indicate what they are. A trailing / indicates that this is a directory. Depending on your settings, it might also use colors to indicate whether each entry is a file or directory. You might recall that we used ls -F in an earlier example.

.. code-block::

    $ ls -F
    Applications/ Documents/    Library/      Music/        Public/
    Desktop/      Downloads/    Movies/       Pictures/

Here, we can see that our home directory contains mostly **sub-directories**. Any names in your output that don’t have trailing slashes, are plain old **files**. And note that there is a space between ls and -F: without it, the shell thinks we’re trying to run a command called ls-F, which doesn’t exist.

Getting help
~~~~~~~~~~~~
**ls** has lots of other **options**. There are two common ways to find out how to use a command and what options it accepts:

We can pass a --help option to the command, such as:

.. code-block:: 

    $ ls --help
    
We can read its manual with man, such as:

.. code-block:: 

    $ man ls
    
Depending on your environment you might find that only one of these works (either man or --help). We’ll describe both ways below.

**The --help option**
Many bash commands, and programs that people have written that can be run from within bash, support a --help option to display more information on how to use the command or program.

.. code-block::

    $ ls --help
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
    -a, --all                  do not ignore entries starting with .
    -A, --almost-all           do not list implied . and ..
        --author               with -l, print the author of each file
    -b, --escape               print C-style escapes for nongraphic characters
        --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
    -B, --ignore-backups       do not list implied entries ending with ~
    -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
    -C                         list entries by columns
        --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
    -d, --directory            list directories themselves, not their contents
    -D, --dired                generate output designed for Emacs' dired mode
    -f                         do not sort, enable -aU, disable -ls --color
    -F, --classify             append indicator (one of */=>@|) to entries
        --file-type            likewise, except do not append '*'
        --format=WORD          across -x, commas -m, horizontal -x, long -l,
                               single-column -1, verbose -l, vertical -C
        --full-time            like -l --time-style=full-iso
    -g                         like -l, but do not list owner
        --group-directories-first
                               group directories before files;
                               can be augmented with a --sort option, but any
                               use of --sort=none (-U) disables grouping
    -G, --no-group             in a long listing, don't print group names
     -h, --human-readable      with -l and/or -s, print human readable sizes
                               (e.g., 1K 234M 2G)
         --si                   likewise, but use powers of 1000 not 1024
     -H, --dereference-command-line
                                follow symbolic links listed on the command line
        --dereference-command-line-symlink-to-dir
                               follow each command line symbolic link
                               that points to a directory
        --hide=PATTERN         do not list implied entries matching shell PATTERN
                               (overridden by -a or -A)
        --indicator-style=WORD append indicator with style WORD to entry names:
                               none (default), slash (-p),
                               file-type (--file-type), classify (-F)
    -i, --inode                print the index number of each file
    -I, --ignore=PATTERN       do not list implied entries matching shell PATTERN
     -k, --kibibytes            default to 1024-byte blocks for disk usage
     -l                         use a long listing format
     -L, --dereference          when showing file information for a symbolic
                               link, show information for the file the link
                               references rather than for the link itself
    -m                         fill width with a comma separated list of entries
    -n, --numeric-uid-gid      like -l, but list numeric user and group IDs
    -N, --literal              print raw entry names (don't treat e.g. control
                               characters specially)
    -o                         like -l, but do not list group information
    -p, --indicator-style=slash
                             append / indicator to directories
    -q, --hide-control-chars   print ? instead of nongraphic characters
        --show-control-chars   show nongraphic characters as-is (the default,
                               unless program is 'ls' and output is a terminal)
    -Q, --quote-name           enclose entry names in double quotes
        --quoting-style=WORD   use quoting style WORD for entry names:
                               literal, locale, shell, shell-always,
                               shell-escape, shell-escape-always, c, escape
    -r, --reverse              reverse order while sorting
    -R, --recursive            list subdirectories recursively
    -s, --size                 print the allocated size of each file, in blocks
    -S                         sort by file size, largest first
        --sort=WORD            sort by WORD instead of name: none (-U), size (-S),
                               time (-t), version (-v), extension (-X)
        --time=WORD            with -l, show time as WORD instead of default
                               modification time: atime or access or use (-u);
                               ctime or status (-c); also use specified time
                               as sort key if --sort=time (newest first)
        --time-style=STYLE     with -l, show times using style STYLE:
                               full-iso, long-iso, iso, locale, or +FORMAT;
                               FORMAT is interpreted like in 'date'; if FORMAT
                               is FORMAT1<newline>FORMAT2, then FORMAT1 applies
                               to non-recent files and FORMAT2 to recent files;
                               if STYLE is prefixed with 'posix-', STYLE
                               takes effect only outside the POSIX locale
    -t                         sort by modification time, newest first
    -T, --tabsize=COLS         assume tab stops at each COLS instead of 8
    -u                         with -lt: sort by, and show, access time;
                               with -l: show access time and sort by name;
                               otherwise: sort by access time, newest first
    -U                         do not sort; list entries in directory order
    -v                         natural sort of (version) numbers within text
    -w, --width=COLS           set output width to COLS.  0 means no limit
    -x                         list entries by lines instead of by columns
    -X                         sort alphabetically by entry extension
    -Z, --context              print any security context of each file
    -1                         list one file per line.  Avoid '\n' with -q or -b
        --help     display this help and exit
        --version  output version information and exit

    The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
    Units are K,M,G,T,P,E,Z,Y (powers of 1024) or KB,MB,... (powers of 1000).

    Using color to distinguish file types is disabled both by default and
    with --color=never.  With --color=auto, ls emits color codes only when
    standard output is connected to a terminal.  The LS_COLORS environment
    variable can change the settings.  Use the dircolors command to set it.

    Exit status:
     0  if OK,
     1  if minor problems (e.g., cannot access subdirectory),
     2  if serious trouble (e.g., cannot access command-line argument).



`GNU coreutils online help <http://www.gnu.org/software/coreutils/>`_

`Full documentation <http://www.gnu.org/software/coreutils/ls>`_

Also available locally via: info '(coreutils) ls invocation'

Unsupported command-line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If you try to use an option (flag) that is not supported, ls and other commands                         will usually print an error message similar to:

.. code-block::

    $ ls -j
    ls: invalid option -- 'j'
    Try 'ls --help' for more information.

**The man command**

The other way to learn about ls is to type

.. code-block::

    $ man ls
    
This will turn your terminal into a page with a description of the ls command and its options and, if you’re lucky, some examples of how to use it.

To navigate through the man pages, you may use **↑** and **↓** to move line-by-line, or try **B** and **Spacebar** to skip up and down by a full page. To search for a character or word in the man pages, use **/ followed by the character** or word you are searching for. Sometimes a search will result in multiple hits. If so, you can move between hits using **N** (for moving forward) and **Shift+N** (for moving backward).

**To quit the man pages, press q**.

Manual pages on the web

Of course there is a third way to access help for commands: searching the internet via your web browser. When using internet search, including the phrase unix man page in your search query will help to find relevant results.GNU provides links to its `manuals <http://www.gnu.org/manual/manual.html>`_ including the `core GNU utilities <http://www.gnu.org/software/coreutils/manual/coreutils.html>`_ , which covers many commands introduced within this lesson.

We can also use ls to see the contents of a different directory. Let’s take a look at our Desktop directory by running ls -F Desktop, i.e., the command ls with the -F option and the argument Desktop. The argument Desktop tells ls that we want a listing of something other than our current working directory:

.. code-block::

    $ ls -F Desktop
    data-shell/
    
Your output should be a list of all the files and sub-directories on your Desktop, including the data-shell directory you downloaded at the setup for this lesson. Take a look at your Desktop to confirm that your output is accurate.

Now that we know the data-shell directory is located on our Desktop, we can do two things.

First, we can look at its contents, using the same strategy as before, passing a directory name to ls:

.. code-block::

    $ ls -F Desktop/data-shell
    creatures/          molecules/          notes.txt           solar.pdf
    data/               north-pacific-gyre/ pizza.cfg           writing/

Second, we can actually change our location to a different directory, so we are no longer located in our home directory.

The **command to change locations is cd** followed by a directory name to change our working directory. **cd stands for “change directory”**, which is a bit misleading: the command doesn’t change the directory, it changes the shell’s idea of what directory we are in.

Let’s say we want to move to the data directory we saw above. We can use the following series of commands to get there:

.. code-block::

    $ cd Desktop
    $ cd data-shell
    $ cd data

These commands will move us from our home directory onto our Desktop, then into the data-shell directory, then into the data directory. You will notice that cd doesn’t print anything. This is normal. **Many shell commands will not output anything to the screen when successfully executed.** But if we run pwd after it, we can see that we are now in /Users/nelle/Desktop/data-shell/data. If we run ls without arguments now, it lists the contents of /Users/nelle/Desktop/data-shell/data, because that’s where we now are:

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell/data
    $ ls -F
    amino-acids.txt   elements/     pdb/	        salmon.txt
    animals.txt       morse.txt     planets.txt     sunspot.txt

**We now know how to go down the directory tree, but how do we go up?** We might try the following:

.. code-block::

    $ cd data-shell
    -bash: cd: data-shell: No such file or directory

But we get an error! Why is this?

With our methods so far, cd can only see sub-directories inside your current directory. There are different ways to see directories above your current location; we’ll start with the simplest.

**There is a shortcut in the shell to move up one directory level** that looks like this:

.. code-block::

    $ cd ..
    
**.. is a special directory name meaning “the directory containing this one”**, or more succinctly, the parent of the current directory. Sure enough, if we run pwd after running cd .., we’re back in /Users/nelle/Desktop/data-shell:

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell

The special directory .. doesn’t usually show up when we run ls. If we want to display it, we can give ls the -a option:

.. code-block::

    $ ls -F -a
    ./   .bash_profile  data/       north-pacific-gyre/  pizza.cfg  thesis/
    ../  creatures/     molecules/  notes.txt            solar.pdf  writing/

**-a stands for “show all”**; it forces ls to show us file and directory names that begin with ., such as .. (which, if we’re in /Users/nelle, refers to the /Users directory) As you can see, it also displays **another special directory that’s just called ., which means “the current working directory”**. It may seem redundant to have a name for it, but we’ll see some uses for it soon.

.. Note::
 Most command line tools, multiple options can be combined with a single - and no spaces between the options: ls -F -a is equivalent to ls -Fa.

**Other Hidden Files**
In addition to the hidden directories .. and ., you may also see a file called .bash_profile. This file usually contains shell configuration settings. You may also see other files and directories beginning with .. These are usually files and directories that are used to configure different programs on your computer. The prefix . is used to prevent these configuration files from cluttering the terminal when a standard ls command is used.

**Orthogonality**
The special names . and .. don’t belong to cd; they are interpreted the same way by every program. For example, if we are in /Users/nelle/data, the command ls .. will give us a listing of /Users/nelle. When the meanings of the parts are the same no matter how they’re combined, programmers say they are orthogonal: Orthogonal systems tend to be easier for people to learn because there are fewer special cases and exceptions to keep track of.

**These then, are the basic commands for navigating the filesystem on your computer: pwd, ls and cd.** Let’s explore some variations on those commands. 

What happens if you type cd on its own, without giving a directory?

.. code-block::

    $ cd
    
How can you check what happened? pwd gives us the answer!

.. code-block::

    $ pwd
    /Users/nelle

It turns out that **cd without an argument will return you to your home directory**, which is great if you’ve gotten lost in your own filesystem.

Let’s try returning to the data directory from before. Last time, we used three commands, but we can actually **string together the list of directories to move to data in one step:**

.. code-block::

    $ cd Desktop/data-shell/data

Check that we’ve moved to the right place by running pwd and ls -F

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell/data

If we want to move up one level from the data directory, we could use cd .. but there is another way to move to any directory, regardless of your current location.

So far, when specifying directory names, or even a directory path (as above), we have been using **relative paths**. When you use a relative path with a command like ls or cd, it tries to find that **location from where we are**, rather than from the root of the file system.

However, it is possible to specify the **absolute path** to a directory by including its **entire path from the root directory**, which is indicated by a leading slash. The leading / tells the computer to follow the path from the root of the file system, so it always refers to exactly one directory, no matter where we are when we run the command.

This allows us to move to our data-shell directory from anywhere on the filesystem (including from inside data). To find the absolute path we’re looking for, we can use pwd and then extract the piece we need to move to data-shell.

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell/data
    $ cd /Users/nelle/Desktop/data-shell

Run pwd and ls -F to ensure that we’re in the directory we expect.

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell
    $ ls -F
    creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg
    solar.pdf   writing/
    
**More Shortcuts**

The shell interprets the character **~ (tilde)** at the start of a path to mean “**the current user’s home directory**”. For example, if Nelle’s home directory is /Users/nelle, then ~/data is equivalent to /Users/nelle/data. This only works if it is the first character in the path: here/there/~/elsewhere is not here/there/Users/nelle/elsewhere.

Another shortcut is the **- (dash)** character. cd will translate - into **the previous directory I was in**, which is faster than having to remember, then type, the full path. This is a very efficient way of moving back and forth between directories. The difference between cd .. and cd - is that the former brings you up, while the latter brings you back. You can think of it as the Last Channel button on a TV remote.

Now in her current directory data-shell, Nelle can see what files she has using the command:

.. code-block::

    $ ls north-pacific-gyre/2012-07-03/

This is a lot to type, but she can let the shell do most of the work through what is called tab completion. If she types:

.. code-block::

    $ ls nor

and then presses **Tab (the tab key on her keyboard), the shell automatically completes the directory name** for her:

.. code-block::

    $ ls north-pacific-gyre/

If she presses **Tab again**, Bash will add 2012-07-03/ to the command, since it’s the only possible completion. Pressing Tab again does nothing, since there are 19 possibilities; pressing Tab twice brings up a list of all the files, and so on. This is called tab completion, and we will see it in many other tools as we go on.

**Working with Files and Directories**
======================================

Creating directories
~~~~~~~~~~~~~~~~~~~~
We now know how to explore files and directories, but how do we create them in the first place?

**See where we are and what we already have**

Let’s go back to our data-shell directory on the Desktop and use ls -F to see what it contains:

.. code-block::

    $ pwd
    /Users/nelle/Desktop/data-shell
    $ ls -F
    creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg
    solar.pdf  writing/
    
**Create a directory**

Let’s create a new directory called thesis using the command **mkdir** thesis (which has no output):

.. code-block::

    $ mkdir thesis

As you might guess from its name, **mkdir means “make directory”**. Since thesis is a relative path (i.e., does not have a leading slash, like /what/ever/thesis), the new directory is created in the current working directory:

.. code-block::

    $ ls -F
    creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg
    solar.pdf  thesis/  writing/

.. Note::

    Two ways of doing the same thing
    
    **Using the shell to create a directory** is no different than **using a file         explorer**. If you open the current directory using your operating system’s graphical file explorer, the thesis directory will appear there too. While the shell and the file explorer are two different ways of interacting with the files, the files and directories themselves are the same.

.. Important::

    Good names for files and directories
    
    Complicated names of files and directories can make your life painful when          working on the command line. Here we provide a few useful tips for the names of your files.

    1. Don’t use spaces.

        Spaces can make a name more meaningful, but since spaces are used to separate arguments on the command line it is better to avoid them in names of files and directories. You can use - or _ instead (e.g. north-pacific-gyre/ rather than north pacific gyre/).

    2. Don’t begin the name with - (dash).

        Commands treat names starting with - as options.

    3. Stick with letters, numbers, . (period or ‘full stop’), - (dash) and _ (underscore).

        Many other characters have special meanings on the command line. We will learn about some of these during this lesson. There are special characters that can cause your command to not work as expected and can even result in data loss.

        If you need to refer to names of files or directories that have spaces or other special characters, you should surround the name in quotes ("").

Since we’ve just created the thesis directory, there’s nothing in it yet:

.. code-block::

    $ ls -F thesis

Create a text file
~~~~~~~~~~~~~~~~~~
Let’s change our working directory to thesis using cd, then run a **text editor called Nano** to create a file called draft.txt:

.. code-block::

    $ cd thesis
    $ nano draft.txt

.. Note::
    Which Editor?
    When we say, “nano is a text editor,” we really do mean “text”: it can only work with plain character data, not tables, images, or any other human-friendly media. We use it in examples because it is one of the least complex text editors. However, because of this trait, it may not be powerful enough or flexible enough for the work you need to do after this workshop. On Unix systems (such as Linux and Mac OS X), many programmers use Emacs or Vim (both of which require more time to learn), or a graphical editor such as Gedit. On Windows, you may wish to use Notepad++. Windows also has a built-in editor called notepad that can be run from the command line in the same way as nano for the purposes of this lesson.

    No matter what editor you use, you will need to know where it searches for and saves files. If you start it from the shell, it will (probably) use your current working directory as its default location. If you use your computer’s start menu, it may want to save files in your desktop or documents directory instead. You can change this by navigating to another directory the first time you “Save As…”

Let’s type in a few lines of text. Once we’re happy with our text, we can press **Ctrl+O** (press the Ctrl or Control key and, while holding it down, press the O key) to write our data to disk (we’ll be asked what file we want to save this to: press **Return** to accept the suggested default of draft.txt).

|nano|


Once our file is saved, we can use **Ctrl-X to quit** the editor and return to the shell.

.. Note::

    Control, Ctrl, or ^ Key
    
    The Control key is also called the “Ctrl” key. There are various ways in which using the Control key may be described. For example, you may see an instruction to press the Control key and, while holding it down, press the X key, described as any of:

   - Control-X
   - Control+X
   - Ctrl-X
   - Ctrl+X
   - ^X
   - C-x
   
    In nano, along the bottom of the screen you’ll see ^G Get Help ^O WriteOut. This means that you can use Control-G to get help and Control-O to save your file.

nano doesn’t leave any output on the screen after it exits, but ls now shows that we have created a file called draft.txt:

.. code-block::

    $ ls
    draft.txt

**Creating Files a Different Way**

We have seen how to create text files using the nano editor. Now, try the following command:

.. code-block::

    $ touch my_file.txt

What did the touch command do? 

Use ls -l to inspect the files. How large is my_file.txt?

.. code-block::

    $ ls -l


.. Note::
    You may have noticed that all of Nelle’s files are named “something dot something”, and in this part of the lesson, we always used the extension .txt. This is just a convention: we can call a file mythesis or almost anything else we want. However, most people use two-part names most of the time to help them (and their programs) tell different kinds of files apart. The second part of such a name is called the filename extension, and indicates what type of data the file holds: .txt signals a plain text file, .pdf indicates a PDF document, .cfg is a configuration file full of parameters for some program or other, .png is a PNG image, and so on.

    This is just a convention, albeit an important one. Files contain bytes: it’s up to us and our programs to interpret those bytes according to the rules for plain text files, PDF documents, configuration files, images, and so on.

    Naming a PNG image of a whale as whale.mp3 doesn’t somehow magically turn it into a recording of whalesong, though it might cause the operating system to try to open it with a music player when someone double-clicks it.

Moving files and directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Returning to the data-shell directory,

.. code-block::

    $ cd ~/Desktop/data-shell/

In our thesis directory we have a file draft.txt which isn’t a particularly informative name, so let’s change the file’s name using **mv**, **which is short for “move”**:

.. code-block::

    $ mv thesis/draft.txt thesis/quotes.txt

The **first argument tells mv what we’re “moving”**, while the **second is where it’s to go**. In this case, we’re moving thesis/draft.txt to thesis/quotes.txt, which has the **same effect as renaming the file**. Sure enough, ls shows us that thesis now contains one file called quotes.txt:

.. code-block::

    $ ls thesis
    quotes.txt

One has to be careful when specifying the target file name, since **mv will silently overwrite any existing file with the same name**, which could lead to data loss. An additional option, **mv -i (or mv --interactive), can be used to make mv ask you for confirmation before overwriting**.

.. Note:: 
    mv also works on directories.

Let’s move quotes.txt into the current working directory. We use mv once again, but this time we’ll just use the name of a directory as the second argument to tell mv that we want to keep the filename, but put the file somewhere new. (This is why the command is called “move”.) In this case, the directory name we use is the special directory name . that we mentioned earlier.

.. code-block::

    $ mv thesis/quotes.txt .

The effect is to move the file from the directory it was in to the current working directory. ls now shows us that thesis is empty:

.. code-block::

    $ ls thesis

Further, ls with a filename or directory name as an argument only lists that file or directory. We can use this to see that quotes.txt is still in our current directory:

.. code-block::

    $ ls quotes.txt
    quotes.txt

Copying Files and Directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **cp** command works **very much like mv, except it copies** a file instead of moving it. We can check that it did the right thing using ls with two paths as arguments — like most Unix commands, ls can be given multiple paths at once:

.. code-block::

    $ cp quotes.txt thesis/quotations.txt
    $ ls quotes.txt thesis/quotations.txt
    quotes.txt   thesis/quotations.txt

We can also copy a directory and all its contents by using the **recursive option -r**, e.g. to back up a directory:

.. code-block::

    $ cp -r thesis thesis_backup

We can check the result by listing the contents of both the thesis and thesis_backup directory:

.. code-block::

    $ ls thesis thesis_backup
    thesis:
    quotations.txt

    thesis_backup:
    quotations.txt


Removing files and directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Returning to the data-shell directory, let’s tidy up this directory by removing the quotes.txt file we created. The Unix command we’ll use for this is **rm (short for ‘remove’)**:

.. code-block::

    $ rm quotes.txt

We can confirm the file has gone using ls:

.. code-block::

    $ ls quotes.txt
    ls: cannot access 'quotes.txt': No such file or directory

.. Important::
    **Deleting Is Forever**
    
    The Unix shell doesn’t have a trash bin that we can recover deleted files from (though most graphical interfaces to Unix do). Instead, when we delete files, they are unlinked from the file system so that their storage space on disk can be recycled. Tools for finding and recovering deleted files do exist, but there’s no guarantee they’ll work in any particular situation, since the computer may recycle the file’s disk space right away.

**Using rm Safely**

If we try to remove the thesis directory using rm thesis, we get an error message:

.. code-block::

    $ rm thesis
    rm: cannot remove `thesis': Is a directory

This happens because rm by default only works on files, not directories.

**rm can remove a directory and all its contents if we use the recursive option -r**, and it will do so without any confirmation prompts:

.. code-block::

    $ rm -r thesis

.. Important::
    Given that there is no way to retrieve files deleted using the shell, rm -r should be used with great caution (you might consider adding the interactive option rm -r -i).

Operations with multiple files and directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Oftentimes one needs to copy or move several files at once. This can be done by providing a list of individual filenames, or specifying a naming pattern using wildcards.

**Copy with Multiple Filenames**

For this exercise, you can test the commands in the data-shell/data directory.

In the example below, what does cp do when given several filenames and a directory name?

.. code-block::

    $ mkdir backup
    $ cp amino-acids.txt animals.txt backup/

If given more than one file name followed by a directory name (i.e. the destination directory must be the last argument), cp copies the files to the named directory.

**Using wildcards for accessing multiple files at once**

Wildcards

**\* is a wildcard, which matches zero or more characters**. Let’s consider the data-shell/molecules directory: \*.pdb matches ethane.pdb, propane.pdb, and every file that ends with ‘.pdb’. On the other hand, p\*.pdb only matches pentane.pdb and propane.pdb, because the ‘p’ at the front only matches filenames that begin with the letter ‘p’.

**? is also a wildcard, but it matches exactly one character**. So ?ethane.pdb would match methane.pdb whereas \*ethane.pdb matches both ethane.pdb, and methane.pdb.

Wildcards can be used in combination with each other e.g. ???ane.pdb matches three characters followed by ane.pdb, giving cubane.pdb ethane.pdb octane.pdb.

When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames before running the command that was asked for. As an exception, if a wildcard expression does not match any file, Bash will pass the expression as an argument to the command as it is. For example typing ls \*.pdf in the molecules directory (which contains only files with names ending with .pdb) results in an error message that there is no file called \*.pdf. However, generally commands like wc and ls see the lists of file names matching these expressions, but not the wildcards themselves. It is the shell, not the other programs, that deals with expanding wildcards, and this is another example of orthogonal design.

**Other Useful Tools and Commands**
===================================
**head prints the first few (10 by default) lines of a file**

.. code-block::

    $ head data/sunspot.txt
    (* Sunspot data collected by Robin McQuinn from *)
    (* http://sidc.oma.be/html/sunspot.html         *)

    (* Month: 1749 01 *) 58
    (* Month: 1749 02 *) 63
    (* Month: 1749 03 *) 70
    (* Month: 1749 04 *) 56
    (* Month: 1749 05 *) 85
    (* Month: 1749 06 *) 84
    (* Month: 1749 07 *) 95

**tail prints the last few (10 by default) lines of a file**

.. code-block::

    $ tail data/sunspot.txt
    (* Month: 2004 05 *) 42
    (* Month: 2004 06 *) 43
    (* Month: 2004 07 *) 51
    (* Month: 2004 08 *) 41
    (* Month: 2004 09 *) 28
    (* Month: 2004 10 *) 48
    (* Month: 2004 11 *) 44
    (* Month: 2004 12 *) 18
    (* Month: 2005 01 *) 31
    (* Month: 2005 02 *) 29
    
**history displays the last few hundred commands that have been executed**

.. code-block::

    $history
    1988  cd ..
    1989  ls
    1990  cd data-shell/
    1991  ls
    1992  mkdir thesis
    1993  ls
    1994  ls-F
    1995  ls
    1996  cd Desktop/data-shell/data/
    1997  pwd
    1998  cd ..
    1999  pwd
    2000  ls -F
    2001  cd Desktop/data-shell/
    2002  head data/sunspot.txt 
    2003  tail data/sunspot.txt 
    2004  history

**grep finds and prints lines in files that match a pattern**

.. code-block::

    $ cd
    $ cd Desktop/data-shell/writing
    $ cat haiku.txt
    The Tao that is seen
    Is not the true Tao, until
    You bring fresh toner.

    With searching comes loss
    and the presence of absence:
    "My Thesis" not found.

    Yesterday it worked 
    Today it is not working
    Software is like that.


.. code-block::

    $ grep not haiku.txt
    Is not the true Tao, until
    "My Thesis" not found
    Today it is not working

**find finds files**

To find all the files in the 'writing' directory and sub-directories

.. code-block::

    $ find .
    .
    ./thesis
    ./thesis/empty-draft.md
    ./tools
    ./tools/format
    ./tools/old
    ./tools/old/oldtool
    ./tools/stats
    ./haiku.txt
    ./data
    ./data/two.txt
    ./data/one.txt
    ./data/LittleWomen.txt

To find all the files that end with '.txt'

.. code-block::

    $find -name *.txt
    ./haiku.txt

**echo print stings (text)** 

This is especially useful when writing Bash scripts

.. code-block::

    $echo hello world
    hello world

**> prints output to a file rather than the shell**

.. code-block::

    $ grep not haiku.txt > not_haiku.txt
    $ ls
    data  haiku.txt  not_haiku.txt  thesis  tools

**>> appends output to the end of a file**

.. code-block::

    $ grep Tao haiku.txt >> not_haiku.txt
    $ nano not_haiku.txt

|nano>>|

**| directs output from the first command into the second command (and the second into the third)**

.. code-block::

    $ cd ../north-pacific-gyre/2012-07-03
    $ wc -l *.txt | sort -n | head -n 5
    240 NENE02018B.txt
    300 NENE01729A.txt
    300 NENE01729B.txt
    300 NENE01736A.txt
    300 NENE01751A.txt
    

This is was just a brief summary of how to use the command line. There is much, much more you can do. For more information check out the `Software Caprentry <https://software-carpentry.org/workshops/>`_ page. 



.. |shelllooklike| image:: ../img/cmd1.png
  :width: 750
  :height: 150

.. |TheFileSystem| image:: ../img/cmd2.png
  :width: 400
  :height: 250

.. |HomeDirectories| image::  ../img/cmd3.png
  :width: 400
  :height: 400

.. |nano| image:: ../img/cmd15.png
  :width: 750
  :height: 200

.. |nano>>| image:: ../img/cmd16.png
  :width: 750
  :height: 115













