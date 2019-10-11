title: Linux basics
author:
  name: Michael Robinson
  email: laxdog@gmail.com
output: basics.html
theme: sjaakvandenberg/cleaver-dark

--

# Linux basics
## A quick look at some common linux commands

--

### Contents

 * Why?
 * Directory structure, file paths and files
 * Text manipulation
 * Advanced text manipulation
 * Connectivity
 * Advanced structure / file etc.
 * Process / user control / information
 * Help / recall
 * Environments
 * System

--

### Why?

There are many reasons that you might need to use the linux command line. The main one being that most of the servers that you will be interacting with do not have any other means of input. They run in a 'headless' state, where they normally don't have a keyboard, mouse or monitor plugged into them and the only way to interact is via 'ssh'. 

This means we only have a text interface to them. But that's ok. We can do everything (and more) with just this interface. 

--


### Directory structure, file paths and files

To help demonstrate this, we will look at the commands being executed on the command line alongside a file explore showing a visual representation of what's happening. 

So, start up a terminal on your local machine and also start up a file explorer on your local machine. Your terminal should start in your home directory. 

By the end of these slides, you should be able to navigate around your home directory in the terminal and see the same locations/files in your file explorer.

--
### Directory structure, file paths and files
#### In this section:
* `ls`
* `pwd`
* `cd`
* understanding paths
* `cp`
* `mv`
* `touch`
* `rmdir`
* `rm`
* `mkdir`
* `file`
* understanding wild cards

--

### Directory structure, file paths and files : `ls` - [L]i[s]t

This is used to list the contents of a directory. You should have started in your home directory, so this should show you the contents of this. Any files will be listed by name here and should match those shown in your file explorer. The -l swtich will give extra info.

```bash
> ls
master.zip
mefffix_m3_test.actual
build_codes.log
```
```bash
> ls -l
-rw-rw-r--. 1 michaelr michaelr    402 Mar 27 19:51 build_codes.log
-rw-rw-r--. 1 michaelr michaelr 143335 Feb 16 11:45 master.zip
-rw-r--r--. 1 michaelr michaelr 176120 Dec 11  2014 mefffix_m3_test.actual

```
--

### Directory structure, file paths and files : `pwd` - [P]rint [W]orking [D]irectory

Shows the directory you are currently executing commands in.

```bash
> pwd
/home/mrobinson/git/training/linux/basics
```
--

### Directory structure, file paths and files : `cd` - [C]hange [D]irectory

Changes to another directory 
```bash
> cd /home/mrobinson/git/training/
> pwd
/home/mrobinson/git/training
```

--

### Directory structure, file paths and files : Paths

There are two types of paths. Relative and absolute. Relative paths are relative to the directory you are in.
```bash
> pwd
/home/mrobinson
cd git/training/
> pwd
/home/mrobinson/git/training
```

Absolute paths are full paths from the very root of the file system and can be used no matter which directory you are in. 
```bash
> pwd
/home/mrobinson/
cd /home/mrobinson/git/training/
> pwd
/home/mrobinson/git/training
```
Lastly a "." indicates the current directory. Try `ls .` for example.

--

### Directory structure, file paths and files : `cp` - [C]o[p]y

Copy a file from one place to another. Full or relative paths can be used. 
```bash
> cp /home/mrobinson/git/training/linux/README /home/mrobinson/git/training/DONTREADME
> ls
DONTREADME  linux
```

```bash
> cp DONTREADME ICANTEVENREAD
> ls
DONTREADME  ICANTEVENREAD  linux
```
--

### Directory structure, file paths and files : `mv` - [M]o[v]e

This is used to move a file from one place to another. It is also used to rename files (as this is the same as moving the file to a different name, but keeping it's location the same). 

```bash
mv DONTREADME /tmp/
> ls
ICANTEVENREAD  linux
> ls /tmp/
basics.html
DONTREADME
tmux-947
```

```bash
> mv ICANTEVENREAD WoopWoopItsTheSoundOfThePolice
> ls
linux  WoopWoopItsTheSoundOfThePolice
```

--

### Directory structure, file paths and files : `mkdir` - [M]a[k]e [D]irectory

This creates a new directory. If we use the -l swtich for ls, we can see it's directory by looking at the first character, which is a d. If you have colours enabled for your terminal you should also noticed that it's a different colour. 

```bash
> mkdir SleepIsForTheWeak
> ls -l 
total 16
drwxrwxr-x. 7 michaelr michaelr 1024 Jul 10 09:05 linux
drwxrwxr-x. 2 michaelr michaelr   80 Jul 10 10:40 SleepIsForTheWeak
-rw-rw-r--. 1 michaelr michaelr 1003 Jul 10 10:25 WoopWoopItsTheSoundOfThePolice
```

--

### Directory structure, file paths and files : `rm` - [R]e[m]ove

This deletes files. Be careful, they can't be recovered. If you need to remove a directory you can use the -r (recursive) switch. Again, be careful, this will delete everything in the directory supplied. 

```bash
> rm WoopWoopItsTheSoundOfThePolice 
> ls
linux  SleepIsForTheWeak
> rm SleepIsForTheWeak/
rm: cannot remove ‘SleepIsForTheWeak/’: Is a directory
> rm -r SleepIsForTheWeak/
> ls
linux

```

--

### Directory structure, file paths and files : `file` - Return the type of file

This can be useful if you're not sure what a file is. It can identify many different file types and show some extra information on them. Files may not always have extensions you recognise or have an extension at all, this command ignores that. 
```bash
> file linux/
linux/: directory
> file linux/basics.html 
linux/basics.html: HTML document, UTF-8 Unicode text, with very long lines
> file linux/basics/basics.md 
linux/basics/basics.md: UTF-8 Unicode text, with very long lines
> file /usr/bin/bash
/usr/bin/bash: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=0x7e60e3500525487556361588a7e2818807f5815a, stripped
```

--

### Directory structure, file paths and files : Wild cards

A wildcard is a symbol used to replace or represent one or more characters. Wildcards are typically either an asterisk (\*), which represents one or more characters or question mark (?), which represents a single character. This means the same command can be executed on many files at the same time. 

```bash
> ls Q*
QuoteHandler.cc QuotePublisher.cc QuoteQualifier.cc QuoteSource.cc QuoteUpdate.cc
QuoteHandler.h  QuotePublisher.h  QuoteQualifier.h  QuoteSource.h  QuoteUpdate.h
```
```bash
> ls Q*.?
QuoteHandler.h QuotePublisher.h QuoteQualifier.h QuoteSource.h QuoteUpdate.h
```
```bash
> ls Q*.??
QuoteHandler.cc QuotePublisher.cc QuoteQualifier.cc QuoteSource.cc QuoteUpdate.cc
```

--

### Text manipulation

This section will go into some basics on display, storing and redirecting output streams from programs. This allows you to 'pipe' or chain various commands together. 

It will then show some examples of common commands that are used to manipulate this data, allowing you to ignore parts of it, search for specific things, subsitute text for other text or maybe split it all up into columns. 

--

### Text manipulation
#### In this section

* Input and output
* Redirection
* stdout, stdin and stderr
* `echo`
* `cat`
* `head`
* `tail`
* `less`
* `cut`
* `grep`

--

### Text manipulation : Input and output 

There are a few different places that programs can get and print data. The standard ones for communication between a keyboard, a program and a display are below, the reasons for the file descriptors will become apparent later:

* stdin - file descriptor 0
  * Standard input, Unless redirected, standard input is expected from the keyboard which started the program.
* stdout - file descriptor 1
  * Standard output, Unless redirected, standard output is the text terminal which initiated the program.
* stderr - file descriptor 2
  * Standard error, The usual destination is the text terminal which started the program. It is acceptable, and normal, for standard output and standard error to be directed to the same destination. 

--

### Text manipulation : Redirection

Text can be redirected from a command to a file using the `>` character, or into a command using `<` and lastly append to a file using `>>`. This can be used to redirect all the inputs and outputs from the last slide (this is where the file descriptor is used)

The next few slides will show examples of each

--

### Text manipulation : Redirection
#### stdout to file

This will cause the ouput of a program to be written to a file.
```bash
ls -l > ls-l.txt
```
        
Here, a file called `ls-l.txt` will be created and it will contain what you would see on the screen if you type the command `ls -l` and execute it.

#### stderr to file

This will cause the stderr ouput of a program to be written to a file.

```bash
grep da * 2> grep-errors.txt
```
        
Here, a file called `grep-errors.txt` will be created and it will contain what you would see the stderr portion of the output of the `grep da *` command.

--
### Text manipulation : Redirection
#### stdout to stderr

This will cause the stderr ouput of a program to be written to the same filedescriptor than stdout.

```bash
grep da * 1>&2 
```
        
Here, the stdout portion of the command is sent to stderr, you may notice that in different ways.

#### stderr to stdout

This will cause the stderr ouput of a program to be written to the same filedescriptor than stdout.
```bash
grep * 2>&1
```

Here, the stderr portion of the command is sent to stdout, if you pipe to less, you'll see that lines that normally 'dissapear' (as they are written to stderr) are being kept now (because they're on stdout).

--

### Text manipulation : Redirection
#### stderr and stdout to file

This will place every output of a program to a file. This is suitable sometimes for cron entries, if you want a command to pass in absolute silence. There are two ways, the first is the full version (note where the redirection is) and the second is the shorthand. 
```bash
grep * > /dev/null 2>&1
```
```bash
grep * &> /dev/null 
```

#### stdin from file

This is less common and I include it for completeness, though there are scenarios where it's useful. This will take the the contents of a file and use it in place of standard input. 

```bash
cat < grep-errors.txt
```
--


### Text manipulation : Pipes

Pipes let you use the output of a program as the input of another one

```bash
ls -l | grep error
```
        
Here, the following happens: first the command ls -l is executed, and it's output, instead of being printed, is sent (piped) to the grep program, which in turn, prints what it has to. In this example we would be better using wild cards `ls -l *error*`, but you will see as we go on what other commands can be chained together in this way. 


--

### Text manipulation : `echo`
Echo will take a string and output it back to standard out. This isn't particularly useful on command line alone, but can be when you start to write scripts. 

```bash
> echo "Work is the curse of the drinking classes"
Work is the curse of the drinking classes
```
This can be redirected though if you wanted to create a file
```bash
echo "Work is the curse of the drinking classes" > quotes.txt
```
And appended to if required
```bash
> echo "I love deadlines. I love the whooshing noise they make as they go by." >> quotes.txt
```

--

### Text manipulation : `cat` - con[cat]enate

Cat, as you have already see, can be used to display the output of a file.
```bash
> cat quotes.txt
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```
Multiple files can be passed to it to display several files one after another
```bash
cat grep-errors.txt quotes.txt
```

--

### Text manipulation : `head`

This is similar to cat in that it will display a file, however it will only display the first X lines. The default is 10, but can be changed with -X
```bash
> head -5 /etc/nsswitch.conf
#
# /etc/nsswitch.conf
#
# An example Name Service Switch config file. This file should be
# sorted with the most-used services at the beginning.
```

### Text manipulation : `tail`

Unsurprisingly tail does the opposite of head. 

--

### Text manipulation : `less`

Less allows you to view the contents of a file and page through at will. Although this could be achieved with cat, less will allow you to scroll, search and page through the file. This could also be acheived with vim or another editor, though less will only load the part of the file you are currently viewing. This is useful if you are looking at a file that is very large as it takes a long time to load the whole thing into memory. 

There are many commands beyond the standard invocation of it, if you want to view them all you can do `less --help`, otherwise the main useful ones are:
* Up arrow and down arrow - Scroll up and down a line
* Page up and page down - Scroll up and down a full screen
* / and ? - Search forwards and backwards in the file
* q - quit

--

### Text manipulation : `cut`
Cut allows you to extract portion of text from a file by selecting columns. There are a number of useful things you can do with it, though if you get too advanced you should probably be using awk instead. Here are two useful examples:

#### Select Column of Characters using Range

```bash
> cut -c21-35 quotes.txt
the drinking c
love the whoosh
```

#### Select Multiple Fields from a File

The -d switch can be used to specify a delimiter, unlike awk, this must be a single character
```
> cut -d ' ' -f4,7,10 quotes.txt
curse drinking
I whooshing make
```

--

### Text manipulation : `grep`
In it's simplist form, grep is used to search for a string in text that it is given. This may be via another command or from a file. 

#### Piped output
```bash
> cat quotes.txt | grep the
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```

#### From a file
```
> grep the quotes.txt
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```

--

### Connectivity

This is just a quick intro on connecting to other machines and verifying that there's nothing wrong with the network. 

#### What's covered

* `ssh`
* `ping`
* `scp`
* `telnet`

--

### Connectivity : `ssh` - secure shell

This is your main method of connecting to another machine via the command line. This (once connected) will allow you to execute commands on the remote machine much like you are in the terminal of your own machine. Basic syntax is as follows:

```
ssh user@remote_machine
```

Where `remote_machine` can be an IP or hostname. There are many different things that can be done with SSH, too many for me to go into now. However one of the most useful is passwordless ssh. This allows you to connect to machines without supplying your password everytime. This can also be accomplished via some GUI utilities, however this may not work when you are already in a terminal or you wish to automate a task. Again, I'll not go into the details here. This [link](http://www.linuxproblem.org/art_9.html) has a good example. 

--

### Connectivity : `ping`

If for some reason you can't connect to a machine over SSH then this is probably your next command. Although not definitive (some machines do not respond to ping) this should tell you whether there is a problem on the network or if the machine is down.

```
> ping 10.119.18.150
PING 10.119.18.150 (10.119.18.150) 56(84) bytes of data.
64 bytes from 10.119.18.150: icmp_seq=1 ttl=64 time=0.056 ms
64 bytes from 10.119.18.150: icmp_seq=2 ttl=64 time=0.099 ms
64 bytes from 10.119.18.150: icmp_seq=3 ttl=64 time=0.086 ms
```

If you see output like that above then you can connect to the machine and something else is wrong. 

--

### Connectivity : `scp` - Secure Copy

This is a method for copying files from one machine to another. It uses the ssh protocol, so anything you can ssh to, you can scp to (and from). The syntax is similar to ssh, but it has files names in the command too. 

```
> scp michaelr@10.119.18.150:/tmp/CareBearStare /home/mrobinson/
Password:
CareBearStare
```
--

### Connectivity : `telnet`

This is another tool that can be useful from time to time. It is normally used to actually connect to a remote terminal and execute commands. However more frequently now I use it to connect to a specific port on a machine to see if it's open. This can be useful to try the ssh port (22) or the http port (80) or various others depending on what you are doing. 

```
> telnet 10.119.18.150 22
Trying 10.119.18.150...
Connected to 10.119.18.150.
Escape character is '^]'.
SSH-2.0-OpenSSH_6.6.1
```

--

### Advanced text manipulation 
#### What's covered
* advanced `grep`
* `regex`
* `sed`
* `awk`
* `strings`
* `diff`

--

### Advanced text manipulation : grep

I use grep every day in multiple different ways. There are loads of things you can do with it, I find these most useful:

#### Search the output of the last command
```
> cat quotes.txt | cut -c1-11 | grep -i WORK
Work is the
```
The `-i` makes it case insensitive.
#### Search a file for the given string
```
> grep -i WORK quotes.txt
Work is the curse of the drinking classes
```


#### Search for everything that doesn't match the given string

```
> grep -i -v WORK quotes.txt
I love deadlines. I love the whooshing noise they make as they go by.
```

--

### Advanced text manipulation : grep
#### Show the X lines after the matching line

```
> grep -i -A 1 WORK quotes.txt
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```

#### Show the X lines before the matching line
```
> grep -i -B 1 LOVE quotes.txt
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```

#### Search for multiple strings
```
> grep -i -e LOVE -e WORK quotes.txt
Work is the curse of the drinking classes
I love deadlines. I love the whooshing noise they make as they go by.
```

--

### Advanced text manipulation : grep
#### Search recursively - This is really handy

```
> mkdir test
> cp quotes.txt test/
> grep -i -r WORK .
quotes.txt:Work is the curse of the drinking classes
test/quotes.txt:Work is the curse of the drinking classes
```

There are lots of other things it can do, and there's not much point in me going into all of them. Suffice to say, you can have a read at the man page or some web pages for other interesting uses for it. 

--

### Advanced text manipulation : Regex

A regular expression is a pattern that describes a set of strings. Regular expressions are constructed analogously to arithmetic expressions by using various operators to combine smaller expressions.

The fundamental building blocks are the regular expressions that match a single character. Most characters, including all letters and digits, are regular expressions that match themselves. Any metacharacter with special meaning may be quoted by preceding it with a backslash.

I could go into a whole day on this alone... These are the basics just so you are aware of what's possible. It would be a good idea to have a look about and see what else you can do knowing the type of thing that can be accomplised. 

--

### Advanced text manipulation : Regex operators

| Operator  | Effect  |
|-----------|---------|
| .         | Matches any single character. |
| ?         | The preceding item is optional and will be matched, at most, once. |
| *         | The preceding item will be matched zero or more times.|
| +         | The preceding item will be matched one or more times.|
| {N}       | The preceding item is matched exactly N times.|
| {N,}      | The preceding item is matched N or more times.|
| {N,M}     | The preceding item is matched at least N times, but not more than M times.|
| -         | represents the range if it's not first or last in a list or the ending point of a range in a list.|
| ^         | Matches the empty string at the beginning of a line; also represents the characters not in the range of a list.|
| $         | Matches the empty string at the end of a line.|

There's a better list [here](http://www.rexegg.com/regex-quickstart.html)

--

### Advanced text manipulation : Regex - examples

#### Search for the start of the line then a word

```
> grep ^root /etc/passwd
root:x:0:0:root:/root:/bin/bash
```
#### Search for a word and the end of the line
```
> grep shutdown$ /etc/passwd
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
```

#### Search for a range of characters
```
> grep [yf] /etc/group
sys:x:3:
tty:x:5:
mail:x:12:postfix,exim
floppy:x:19:
ftp:x:50:
nobody:x:99:
ssh_keys:x:999:
systemd-journal:x:190:
postfix:x:89:
nfsnobody:x:65534:
```

--
### Advanced text manipulation : Regex - examples
#### This lists all files starting with "a", "b", "c", ",q","x", "y" or "z".
```
> ls -ld [a-c,q,x-z]*
-rw-rw-r--. 1 michaelr michaelr 1526 Oct 24  2014 boxes
-rw-rw-r--. 1 michaelr michaelr  402 Mar 27 19:51 build_codes.log
drwxrwxr-x. 6 michaelr michaelr 1024 Jun  8 15:21 builds
-rwxrwxr-x. 1 michaelr michaelr 2691 Oct 24  2014 checkPorts_bak.py
-rwxrwxrwx. 1 michaelr michaelr 3161 Oct 24  2014 checkPorts.py
drwxrwxr-x. 2 michaelr michaelr   80 Mar 28  2014 cntlm
-rwxrwxr-x. 1 michaelr michaelr  757 Jul 13 11:19 colour.sh
-rw-rw-r--. 1 michaelr michaelr  112 Jul 13 11:48 quotes.txt
```

#### List all files starting with an upper case letter
```
> ls -ld [[:upper:]]*
-rw-rw-r--.  1 michaelr michaelr        0 Jul 14 10:29 CareBearStare
drwx------. 14 michaelr michaelr     2048 Jul 15 13:23 Dropbox
-rw-rw-r--.  1 michaelr michaelr  5674868 Oct 28  2014 Master_Field_Definitions.xml
-rw-rw-r--.  1 michaelr michaelr 26097970 Sep 11  2013 RH5-x86-64_wombat_papaframework_2.17.261_lbt323_wapi40_xml.tgz
```
--

### Advanced text manipulation : Regex - summary

Regular expressions are powerful tools for selecting particular lines from files or output. A lot of UNIX commands use regular expressions: vim, perl, the PostgreSQL database and so on. They can be made available in any language or application using external libraries, and they even found their way to non-UNIX systems. For instance, regular expressions are used in the Excell spreadsheet that comes with the MicroSoft Windows Office suite. In this chapter we got the feel of the grep command, which is indispensable in any UNIX environment.

Note    

The grep command can do much more than the few tasks we discussed here; we only used it as an example for regular expressions. The GNU grep version comes with plenty of documentation, which you are strongly advised to read!

Bash has built-in features for matching patterns and can recognize character classes and ranges.

--

### Advanced text manipulation : `sed`

As with everything today, these will only be a short intro to the commands and the type of things they can do. Sed is a stream editor. That means usually you will be piping data into and or out of it. There are not that many main commands. The most used is the subsitution and will be the focus of the next few slides. 

*Substitute a simple string*
```
> tail -1 quotes.txt | sed s/deadlines/jokes/                                                                           
I love jokes. I love the whooshing noise they make as they go by.
```
*Substitute all matches of a simple string (global)*

```
> tail -1 quotes.txt | sed s/love/eat/
I eat deadlines. I love the whooshing noise they make as they go by.
> tail -1 quotes.txt | sed s/love/eat/g
I eat deadlines. I eat the whooshing noise they make as they go by.
```
*Substitute all regex matches*

```
> sed s/[abcdef]/X/g quotes.txt                                                                                         
Work is thX XursX oX thX Xrinking XlXssXs
I lovX XXXXlinXs. I lovX thX whooshing noisX thXy mXkX Xs thXy go Xy.
```

--

### Advanced text manipulation : `sed`
*The slash as a delimiter*

The character after the s is the delimiter. It is conventionally a slash, because this is what ed, more, and vi use. It can be anything you want, however. If you want to change a pathname that contains a slash - say /usr/local/bin to /common/bin - you could use the backslash to quote the slash:

```
> ls -ld /usr/local/bin/ > old
drwxr-xr-x. 2 root root 4096 Jul 15 13:42 /usr/local/bin/
> sed 's/\/usr\/local\/bin/\/common\/bin/' old
drwxr-xr-x. 2 root root 4096 Jul 15 13:42 /common/bin/
```
Gulp. Some call this a 'Picket Fence' and it's ugly. It is easier to read if you use an underline instead of a slash as a delimiter:
```
sed 's_/usr/local/bin_/common/bin_' old
```
--

### Advanced text manipulation : `awk`

This can get VERY complicated as it's essentially a scripting language on to it's own. I don't intend to go in to any of that. Following are just a few examples of things it's useful for.

*Print the second field separated by white space*
```
> # awk by default will split using white space for fields
> awk '{print $2}' quotes.txt 
is
love
```
*Print the second field separated by a word*
```
> # awk by default will split using white space for fields* diff
> awk -F 'the' '{print $2}' quotes.txt                                                                                  
curse of 
whooshing noise 

```
--

### Advanced text manipulation : `awk`

*Sum the input from another process*
```
> cat count.txt 
1
2
3
4
5
> cat count.txt | awk '{ sum+=$1} END {print sum}'
15
```

*Average the input from another process*
```
> cat count.txt 
1
2
3
4
5
> cat count.txt | awk '{ sum += $1 } END { if (NR > 0) print sum / NR }'
3
```
--

### Advanced text manipulation : strings
There are not that many use cases for this command, the first here is an arbitrary example and the second one you might actually use.

#### Arbitrary example

```
> strings /lib64/ld-linux-x86-64.so.2 | grep version
versions
display version dependencies
la_version
ELF file ABI version invalid
 (no version symbols)
, version 
unsupported version 
weak version `
version lookup error
file you run.  This is mostly of use for maintainers to test new versions
FATAL: cannot determine kernel version
ELF file version does not match current one
ELF file version ident does not match current one
checking for version `%s' in file %s [%lu] required by file %s [%lu]
no version information available (required by 
cannot allocate version reference table
```
--

### Advanced text manipulation : `strings`
#### Useful example
```
>strings /usr/bin/strings | grep -- --
  -a - --all                Scan the entire file, not just the data section [default]
  -d --data                 Only scan the data sections in the file
  -f --print-file-name      Print the name of the file before each string
  -n --bytes=[number]       Locate & print any NUL-terminated sequence of at
  -t --radix={o,d,x}        Print the location of the string in base 8, 10 or 16
  -w --include-all-whitespace Include all whitespace as valid string characters
  -o                        An alias for --radix=o
  -T --target=<BFDNAME>     Specify the binary file format
  -e --encoding={s,S,b,l,B,L} Select character size and endianness:
  -s --output-separator=<string> String used to separate strings in output.
  -h --help                 Display this information
  -v -V --version           Print the program's version number```
--

### Advanced text manipulation : `diff`
This shows you the differences between two files or directories. It has a lot of different options which you can look, here's basic usage however


 Let's say we have two files, file1.txt and file2.txt.

If file1.txt contains the following four lines of text:
```
I need to buy apples.
I need to run the laundry.
I need to wash the dog.
I need to get the car detailed.
```
...and file2.txt contains these four lines:
```
I need to buy apples.
I need to do the laundry.
I need to wash the car.
I need to get the dog detailed.
```
--

### Advanced text manipulation : `diff`

...then we can use diff to automatically display for us which lines differ between the two files with this command:
```
diff file1.txt file2.txt
```

...and the output will be:

```diff
 2,4c2,4
 < I need to run the laundry.
 < I need to wash the dog.
 < I need to get the car detailed.
 ---
 > I need to do the laundry.
 > I need to wash the car.
 > I need to get the dog detailed.
```

*vimdiff is nicer...*

`vimdiff file1.txt file2.txt`

--

### Advanced Dir, paths and files
#### What's covered
* `which`
* `find`
* `locate / updatedb`
* `permissions`
* `chown`
* `chmod`
* `unzip`
* `gzip`
* `tar`

--

### Advanced Dir, paths and files : `which`
This command basically tells you the full path of the file that you pass to it. This may not seem useful, but sometimes you may have many different binaries in a test or dev environment. Especially if you are sourcing wombat.profile or similar to setup your `$PATH` variable. Running  `which bash` in this case would tell you exactly which one you are executing. 
``` 
> which bash
/usr/bin/bash
```
Another sometimes useful case is when using virtual environments in python. You can make sure that the python version you are executing your program with is the one you expect. 
```
> which python
/usr/bin/python
> source virtual_envs/venv/bin/activate                                                                            
> which python
~/virtual_envs/venv/bin/python
```

--

### Advanced Dir, paths and files : `find`

The clue is in the name. It will search directories recursively to find files that you have specified via filename regex and other means. There are many powerful features in this tool, so it's worth having a look at the man pages. Here are a few examples I use frequently
#### Find a file underneath the current directory with the given file name (regex)
```
> find . -name "*quo*"
```

A useful additonal note around that is you can make it **ignore case** by using `-iname` instead of name.
If you remember from before the `.` is used to represent the current working directory. The command could also be written as 
```
> find /home/michaelr -name "*quo*"
```
--

### Advanced Dir, paths and files : `find` - mindepth / maxdepth
While not immediately appparent why these would be useful, there are often cases where they are needed. Supplying maxdepth 1 in the previous example for instance would only search the current working directory:
```
> find . -name \*md | head
./bash-scripting/bash_scripting_intro.md
./bash-scripting/README.md
./python/06-testing/testing_example/.pytest_cache/README.md
./python/README.md
./python/python_exercises/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/rubberband/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/scroll_down/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/hinterland/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/snippets/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/toggle_all_line_numbers/readme.md```
```
> find . -mindepth 9 -name \*md | head
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/rubberband/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/scroll_down/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/hinterland/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/snippets/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/toggle_all_line_numbers/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/notify/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/runtools/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/tree-filter/readme.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/table_beautifier/README.md
./python/venv/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/freeze/readme.md```
Notice how each time a regex is used, this is because find expects the parameter to name to be the exact match of the file you are looking for. 

--

### Advanced Dir, paths and files : find - `mtime`

There are several different times that can be used for file matching. This one is the modify time, i.e. the last time the file changed. This is the most commonly used. This command can be useful to find out which file it was you were modifying today and have forgotten about, or to find old files that could maybe be removed to clear up space on a disk. 
#### All files in the current directory that have been modified today
```
> find . -maxdepth 1 -mtime -1                                                                                          
.
./.bash_history
./old
./.Xauthority
./test
./.vim
./.viminfo
./.cache
./.vimrc
./.bashrc
./quotes.txt
./count.txt
./pika
./test.tar.gz
```

--

### Advanced Dir, paths and files : find - `exec`
This is where things get interesting. The exec parameter will allow you to execute a command on every match that it finds. So for example, if we wanted to find every file that was in the /etc directory, that had conf in the title and then print the first line of that file. We could do this:
```
> find /etc -iname "*conf*" -exec head -1 {} \;
#
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
<?xml version="1.0"?>
```
The `{}` in the example will be replaced by the file name. One important thing to note here is that you **must** have a space between the `{}` and the `\;` otherwise you will see this error:
```
> find /etc -iname "*conf*" -exec head -1 {}\;                                                                          
                                              
find: missing argument to `-exec'
```

As I mentioned, there are many other uses for find and you can have a look at the help for more examples. 

--

### Advanced Dir, paths and files : `locate`
This is another very useful tool that will find files on a disk. However, unlike find, it will search the entire disk by default. However, there's a catch. It comes along with another tool called updatedb. 

The updatedb tool is the one that actually finds the files on the disk and allows locate to tell you where they are. 

So, normally not an issue, just run updatedb and then you can view the files. Well updatedb requires root permissions to run, so unless you have root or sudo on the box then the information you will get back from locate could be out of date. However, it's still worth a try as it's much faster than find if you just want to know the location of a file. 


```
> locate OfFun
/var/userspace/autobuild/WelcomeToTheHouseOfFun
```

--

### Advanced Dir, paths and files : permissions

```
> ls -l
total 270048
-rw-rw-r--.  1 michaelr michaelr     18667 Jan 23 10:01 1
drwxrwxr-x.  5 michaelr michaelr      1024 Feb 25  2014 217-trunk
-rw-rw-r--.  1 michaelr michaelr      1526 Oct 24  2014 boxes
-rw-rw-r--.  1 michaelr michaelr       402 Mar 27 19:51 build_codes.log
drwxrwxr-x.  6 michaelr michaelr      1024 Jun  8 15:21 builds
-rw-rw-r--.  1 michaelr michaelr         0 Jul 14 10:29 CareBearStare
```
These are who has access to files and what access they have. 

You can see the permissions on files by using `ls -l`. You can see the user who owns the file `michaelr` and the group `michaelr` that the file belongs to.  

The first column is the permissions for each user and group (see next slide)

--

### Advanced Dir, paths and files : permissions

```
> ls -l
total 270048
-rw-rw-r--.  1 michaelr michaelr     18667 Jan 23 10:01 1
drwxrwxr-x.  5 michaelr michaelr      1024 Feb 25  2014 217-trunk
-rw-rw-r--.  1 michaelr michaelr      1526 Oct 24  2014 boxes
-rw-rw-r--.  1 michaelr michaelr       402 Mar 27 19:51 build_codes.log
drwxrwxr-x.  6 michaelr michaelr      1024 Jun  8 15:21 builds
-rw-rw-r--.  1 michaelr michaelr         0 Jul 14 10:29 CareBearStare
```

The first block of data is made up of 10 characters. They're broken down like so:

|Position | Meaning |
|---------|---------|
|1        |File type (There lots, the most common are "d" directory, "l" symbolic link and "-" regular file) |
|2-4      |Permissions for the **owner** of the file|
|5-7      |Permissions for people in the same **group** as the file|
|8-10     |Permissions of **other** people (not the owner or group|

|Character | Meaning |
|----------|---------|
| r | read |
| w | write |
| x | execute |

--

### Advanced Dir, paths and files : permissions
#### `chmod`
This allows you to change the permissions on a file allowing others to read / write / excute. There are two ways to specify the permissions. I like this way
```
> ls -l quotes.txt                                                                                                      
-rw-rw-r--. 1 michaelr michaelr 112 Jul 13 11:48 quotes.txt
> chmod ugo+x quotes.txt                                                                                                
> ls -l quotes.txt                                                                                                      
-rwxrwxr-x. 1 michaelr michaelr 112 Jul 13 11:48 quotes.txt
```

|Character | Meaning |
|----------|---------|
| u | user |
| g | group |
| o | other |

--

### Advanced Dir, paths and files : permissions
#### `chmod`

Lots of people use this way

```
> chmod 600 quotes.txt
> ls -l quotes.txt                                                                                                      
-rw-------. 1 michaelr michaelr 112 Jul 13 11:48 quotes.txt
```
The second uses a bit mask, which is explained [here](http://www.cyberciti.biz/faq/unix-linux-bsd-chmod-numeric-permissions-notation-command/) if you're interested in using it. 

#### `chown`
This will change the owner of a file. In most cases you probably don't want to do this. Normally you just want to allow others to read the file, not own it. 

--

### Advanced Dir, paths and files : zips

#### `unzip`
This will unzip a file that comes in the standard windows format, files that end in `.zip` for example. You can zip files as well, but just use gzip or tar with gzip instead. 
Zipping is basically a method for compressing files. This means they take up less disk space and should be easier to upload to places, leave more free space for others to use and take less time to copy place to place. 
```
> unzip file.zip -d destination_folder
```

#### `gzip`
This is more widely used on linux and files generally come with the extension `.gz`. 
```
# To zip up a file
> gzip quotes.txt

# Original replace by the zipped version
> ls -l quotes*

# To unzip a file
> gunzip quotes.txt.gz

```

--

### Advanced Dir, paths and files : `tar`

This command does a few things. By itself (without compression) it will add all the given files to one large file (called a tarball). The first variable after the options is the file to create ***Make sure you add this or you'll overwrite a file***.
The options do [c]reate, [v]erbose, [f]ilename
#### create a new tarball
```
> tar cvf test.tar quotes.txt test/
quotes.txt
test/
test/quotes.txt
```

#### view what's in the tarball
```
> tar tvf test.tar 
-rw-rw-r-- michaelr/michaelr 112 2015-07-16 11:51 quotes.txt
drwxrwxr-x michaelr/michaelr   0 2015-07-16 11:51 test/
-rw-rw-r-- michaelr/michaelr 112 2015-07-15 20:20 test/quotes.txt
```

#### extract from a tarball
```
> tar xvf test.tar                                                                                                      
quotes.txt
test/
test/quotes.txt
```
--

### Advanced Dir, paths and files : `tar`

That in itself is quite useful. If you are copying a lot of small files across the network, especially via SCP or FTP, it can take a long time to look up each individual file on the disk. So by using tar, it will only have to do one lookup, increasing your transfer rate. This will become immediately obvious if you are transferring a lot of source files. 

Though, it becomes a lot more useful when you combine it with a zip function. You can do this after you have created the tar if you wish, though tar has functionality built in for this. 

```
> tar zcvf test.tgz quotes.txt test/                                                                                    
quotes.txt
test/
test/quotes.txt

```
Files created with this normally use the extension `.tgz` or `.tar.gz`. 

--

### Process / user control / information - Why?
The reason for knowing what other users is doing is mainly to stop them doing it! Well, not always, but it's useful. If you have information about who is logging into the machine and doing what then you can maybe track down what problems you are seeing. 

Remember that a lot of the machines that you'll be using are also being used by multiple other people at the same time. So it's easy for someone to use up all the disk space, or hog a CPU running their applications running at full rate. 

These commands should help in finding some of that out. 

-- 

### Process / user control / information - What?
#### What's covered
* `last`
* `whoami` / `id`
* `who`
* `top`
* `ps`
* `kill`
* `pkill`
* `fg`
* `bg`
* Ctrl-z
* Ctrl-c
* `jobs`
* `kill %1`
* `sudo`

--

### Process / user control / information - `last`
Usually combined with `head` because the output is quite large, `last` will show you the last time users logged on to the box. 
```
> last | head
paul pts/52       10.193.2.37      Thu Jul 16 09:24   still logged in   
paul pts/101      10.193.2.37      Thu Jul 16 09:18   still logged in   
lloyd pts/100      10.193.2.10      Thu Jul 16 09:18   still logged in   
david  pts/99       10.193.2.128     Thu Jul 16 09:18   still logged in   
paul pts/98       10.193.2.37      Thu Jul 16 09:17   still logged in   
paul pts/97       10.193.2.37      Thu Jul 16 09:08 - 09:35  (00:26)    
thomas pts/94       10.193.2.176     Thu Jul 16 09:07   still logged in   
glenn pts/63       10.193.2.180     Thu Jul 16 08:57   still logged in   
sarah  pts/29       10.193.2.186     Thu Jul 16 08:14 - 09:51  (01:37)    
michaelr pts/36       10.193.2.14      Wed Jul 15 20:03   still logged in   
```
--

### Process / user control / information - `whoami` / `id`

`whoami` will simply print out the username that you are logged in as. id will give similar information, just more. It can also be used to query other users on the system. This is useful to find out what groups you are part of. 
Although most of the time you clearly know which user you are logged in as, sometimes you are using a shared user or you have sudo-ed to root. 

```
> whoami 
michaelr
> id
uid=947(michaelr) gid=800(michaelr) groups=800(michaelr),807(es),810(swx),812(builders),818(AX-build)
> id bob
uid=123(bob) gid=1899495625937(domain^users) groups=1899446795937(domain^users)
```

--
### Process / user control / information - `who` / `w`
This will tell you who is currently logged into the system (and for w, what they are doing). This is useful if you're on a machine and want to make sure that you are not going to ruin anyone else's day by using all the CPU / Memory / whatever for yourself. 

Or, if someone is already ruining your day...

The default options for w give more information than who, but who has more options that can be configured. 
```
> w
 10:34:44 up 22 days, 16:30, 13 users,  load average: 0.00, 0.02, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1                      24Jun15 22days  0.04s  0.04s -bash
mmulhern pts/29   10.193.3.101     10:29   20.00s  0.08s  0.08s -bash
paul pts/52   10.193.2.37      09:24   55:32   0.03s  0.03s -bash
glenn pts/63   10.193.2.180     08:57   52:12   0.04s  0.00s tmux
lloyd pts/78   10.193.3.98      10:29    2:12   0.03s  0.03s -bash
michaelr pts/35   10.193.2.14      Wed20    4.00s  0.03s  0.01s tmux a
michaelr pts/36   10.193.2.14      Wed20   14:30m  0.02s  0.02s -bash
thomas pts/94   10.193.2.176     09:07    1:11m  0.01s  0.00s tmux a
lloyd pts/147  10.193.2.10      Wed11   17:17m  0.54s  0.17s vim cccccc
paul pts/98   10.193.2.37      09:17   55:24   0.03s  0.03s -bash
david  pts/99   10.193.2.128     09:18   43:32   0.11s  0.11s -bash
lloyd pts/100  10.193.2.10      09:18   53:24   0.12s  0.12s -bash
paul pts/101  10.193.2.37      09:18   55:32   0.59s  0.57s vim -p .py common.py 
```

--

### Process / user control / information - `who` / `w`

```
> who
root     tty1         2015-06-24 08:44
mmulhern pts/29       2015-07-16 10:29 (10.193.3.101)
paul pts/52       2015-07-16 09:24 (10.193.2.37)
glennont pts/63       2015-07-16 08:57 (10.193.2.180)
lloydar pts/78       2015-07-16 10:29 (10.193.3.98)
michaelr pts/35       2015-07-15 20:02 (10.193.2.14)
michaelr pts/36       2015-07-15 20:03 (10.193.2.14)
tom pts/94       2015-07-16 09:07 (10.193.2.176)
lloydar pts/147      2015-07-15 11:48 (10.193.2.10)
paul pts/98       2015-07-16 09:17 (10.193.2.37)
david  pts/99       2015-07-16 09:18 (10.193.2.128)
lloydar pts/100      2015-07-16 09:18 (10.193.2.10)
paul pts/101      2015-07-16 09:18 (10.193.2.37)
```

--

### Process / user control / information - `top`

Another useful one to see who or what is using all the resources on the machine. 
```
> top
top - 10:36:35 up 22 days, 16:32, 13 users,  load average: 0.00, 0.01, 0.05
Tasks: 388 total,   1 running, 385 sleeping,   2 stopped,   0 zombie
%Cpu(s):  0.9 us,  0.2 sy,  0.0 ni, 98.6 id,  0.1 wa,  0.0 hi,  0.0 si,  0.2 st
KiB Mem :  3881168 total,   585060 free,  1253436 used,  2042672 buff/cache
KiB Swap:  4095996 total,  3637504 free,   458492 used.  2269420 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
 2154 michaelr  20   0  144208   3224   2028 R   5.6  0.1   0:00.01 top
    1 root      20   0  141660   5440   2848 S   0.0  0.1   0:29.40 systemd
    2 root      20   0       0      0      0 S   0.0  0.0   0:00.18 kthreadd
    3 root      20   0       0      0      0 S   0.0  0.0   1:20.05 ksoftirqd/0
    5 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0H
    7 root      rt   0       0      0      0 S   0.0  0.0   0:06.01 migration/0
    8 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcu_bh
    9 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcuob/0
```
There are a lot of switches on command line, but I normally just use the ones in the interface. Press `?` to see them. Some of the more useful ones are 

| Key | Action |
|-----|-------|
| M   | Sort by memory usage |
| H   | Show threads |
| V   | Show forest view |
| 1   | Show all CPU stats | 
| <   | Sort by the column left of this one |
| >   | Sort by the column right of this one |

--

### Process / user control / information - `ps`

Everyone has their own way to run this command. Basically it gives information on processes running on the system. Normally I'm running this to get the PID to kill a program or to check that something is actually running, or if it's still running. 

Much of this information is similar to that of top, this however will show more than just the top X processes running.

I use these flags `-ef` Check the man / help pages for others.
```
> ps -ef | tail
mrobins+  1866  1694  0 07:43 ?        00:00:00 [hp-upgrade] <defunct>
mrobins+  1868  1695  0 07:43 ?        00:00:00 st
mrobins+  1869  1868  0 07:43 pts/1    00:00:00 /bin/bash
mrobins+  2126  1869  0 07:45 pts/1    00:00:00 tmux
mrobins+  2128     1  0 07:45 ?        00:00:00 tmux
mrobins+  2129  2128  0 07:45 pts/0    00:00:00 -bash
mrobins+  2175  2128  0 07:45 pts/2    00:00:00 -bash
mrobins+  2240  2129  0 07:46 pts/0    00:00:00 vim basics.md
mrobins+  2323  2175  0 07:48 pts/2    00:00:00 ps -ef
mrobins+  2324  2175  0 07:48 pts/2    00:00:00 tail
```

--

### Process / user control / information - `kill`

This is used to kill a user. It spins their hard disk fast enough to set fire to the machine and burn their house to the ground. 

_editor's note: apologies for the bad humor_

In reality it kills processes. You need to give it a PID to do that, which you can get from the last command `ps` that we ran.

```
> ps -ef | grep top
mrobins+  1524  1512  0 07:43 ?        00:00:00 xfdesktop --display :0.0 --sm-client-id 240340fb0-eaab-43e2-9268-c142a097170e
mrobins+  2413  2175  0 07:52 pts/2    00:00:00 top
mrobins+  2415  2367  0 07:52 pts/3    00:00:00 grep --color=auto top
:) Fri Jul 17 07:52:54 mrobinson@localhost:~/Dropbox/source/work/training/linux/basics (2 files, 62k total)(0)
>
:) Fri Jul 17 07:52:59 mrobinson@localhost:~/Dropbox/source/work/training/linux/basics (2 files, 62k total)(0)
> kill 2413
:) Fri Jul 17 07:53:09 mrobinson@localhost:~/Dropbox/source/work/training/linux/basics (2 files, 62k total)(0)
> ps -ef | grep top
mrobins+  1524  1512  0 07:43 ?        00:00:00 xfdesktop --display :0.0 --sm-client-id 240340fb0-eaab-43e2-9268-c142a097170e
mrobins+  2457  2367  0 07:53 pts/3    00:00:00 grep --color=auto top
```

### Process / user control / information - `pkill`

Also used to kill processes, though for this you only need to supply the name of the program you wish to kill. For this reason however you should be careful. It will try to kill **any** process that has the supplied argument in it's name.

--

### Process / user control / information - signals

So, if you've already heard of signals, great. I'm not going to go into a lot of detail on them. Suffice to say, if a process won't die with a normal kill command (which by default sends a 15 signal), then you can try to send `kill -9` or `pkill -9`.

The main reason I wrote this part is because you shouldn't just send a `kill -9` as your default / go to behaviour. I see a lot of people doing this and it's bad practice. The reason being most of the time the process doesn't clean up. This can lead to unexpected / unwanted behaviour. So only use -9 if a normal kill doesn't work. 

--

### Process / user control / information - Ctrl-c

These are actually signals too. You may have used this already. If a program is running you can use the key combination `Ctrl-c` to stop it running. If this doesn't work, you can kill it with the method mentioned previously. This is just handier as you're normally in the same terminal as the program. 

--

### Process / user control / information - Ctrl-z

This is another signal, and is useful for a number of reasons, my main use case is actually whin I'm inside vim. It will stop the process but not kill it. So it's in a kind of paused state. It's handy in vim becuase it will drop you to a bash prompt where you can execute the thing you are writing in vim for example. 

You could just `:wq` to write quit in vim, but this is quicker for getting a prompt and reloading vim and more importantly you don't loose the current state that vim is in. Meaning you still have your full undo history, split panes, tabs, whatever else you have opened.

To get the program back you need to use the `fg` (as in \[f]ore\[g]round) command.

--

### Process / user control / information - `bg` / `fg`

Normally used in conjuction with the last command (Ctrl-z), `bg` will put the task that you were running (and paused) into the background. This means that it will start to run again, but this will happnen in the background. 

It will still output to stdout, so you might not always want to use this as can make your terminal confusing. Though it is useful if you've kicked off something that's logging to file and you know is going to take a while. 

You can get the same behaviour using the `&` character at the end of a command. 

Running `fg` is what you use to bring the last job that you backgrounded. This is also true for commands that you used Ctrl-z to pause.


### Process / user control / information - `jobs`

This command will be useful with the previous

--

### Process / user control / information - `sudo`
As hinted at beofore, `sudo` is used to escalate your permissions.

Because it allows you to do things which are possibly dangerous, we're not going to cover it here, but it's good to understand what it's for, even if you're not going to use it!
```
>head /var/log/hessages
head: cannot open '/var/log/hessages' for reading: No such file or directory
>sudo head /var/log/messages
[sudo] password for matt:
Oct  6 03:11:02 hex rsyslogd[16650]: [origin software="rsyslogd" swVersion="8.1907.0" x-pid="16650" x-info="https://www.rsyslog.com"] rsyslogd was HUPed
Oct  6 03:11:03 hex audit[32246]: AVC avc:  denied  { connectto } for  pid=32246 comm="docker-gen" path="/run/Oct  6 03:11:03 hex audit[17907]: VIRT_CONTROL pid=17907 uid=0 auid=4294967295 ses=4294967295 Oct  6 03:11:07 hex audit[646]: AVC avc:  denied  { open } for  pid=646 comm=54687265616420506F6F6C20576F72 path="/config/logs/sonarr.trace.txt" dev="dm-0" ino=2097228 scontext=system_u:system_r:container_t:s0:c117,c671 tcontext=system_u:object_r:default_t:s0 tclass=file permissive=1
```