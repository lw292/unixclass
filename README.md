# The Very Basics of the Unix Command Line

<br/>

## Outline

* Accessing and navigating a Unix-based operating system with a terminal.
* Basics of running a Unix command.
* Essential command line tools for reading and editing files.
* Fundamentals of the Unix file system permissions.
* The basics of automating tasks with shell scripting.

<br/>

## Getting Basic System Information

You can get some basic **system information** by running the command `uname`:
```
uname
```

> [!TIP]
> **The Anatomy of a Command**. We can pass **options** (sometimes known as **flags**) to a command. The syntax usually looks like this:
> ```
> command_name [options]
> ```
> For example:
> ```
> uname -a # single dash + single letter
> uname --all # double dashes + full name
> uname -s -v # multiple single letter options
> uname --kernel-name --kernel-version # multiple full name options
> uname -sv # shorthand for multiple single letter options
> ```

To print your **user name** on the system, run:
```
whoami
```

To print the **current system date and time**, run:
```
date
```

<br/>

## Navigating the File System

To print the **present working directory**, run:
```
pwd
```

To **list** the contents of a directory, run:
```
ls [/path/to/directory]
```

> [!TIP]
> **The Anatomy of a Command**
> In addition to options or flags, most of the time we also need to pass **parameters** to a command. The syntax of a command therefore looks like this:
> ```
> command_name [options] [parameters]
> ```
> For example:
> ```
> ls data/sample
> ls -la data/sample
> ls -lah /workspace/unix/data/sample
> ls -lahr /workspace/unix/data/sample
> ```

> [!TIP]
> **Relative path** starts from the present working directory. For example, suppose we are currently in `/workspace/unixclass/data`:
> ```
> my_file.csv # => /workspace/unixclass/data/my_file.csv
> sample/my_file.csv # => /workspace/unixclass/data/sample/my_file.csv
> ```
> **Absolute path** starts from the root directory, so it always starts with `/`:
> ```
> /workspace/unixclass/my_file.csv
> /workspace/unixclass/data/my_file.csv
> ```

> [!TIP]
> **Special Characters**
> **Forward slash** `/` denotes the root directory at the beginning of a path, and is the element delimiter in the middle of a path:
> ```
> / # Root directory
> data/my_file.csv # Delimits the directory name "data" from the file name "my_file.csv"
> /workspace/unixclass/data/my_file.csv # The first slash denotes the root directory, and the subsequent ones delimit path elements
> ```
> A **single dot** `.` represents the present working directory, and **double dots** `..` represent the parent directory of the present working directory. Assume we are currently in `/workspace/unixclass/data`:
> ```
> ./my_file.csv # => my_file.csv => /workspace/unixclass/data/my_file.csv
> ../README.md # => /workspace/unixclass/README.md
> ```
> Sometimes you may also encounter the **tilde** character `~`, which in most Unix systems denote the user's "home directory".

> [!TIP]
> **Convenience Features in the Bash Shell**
> It can be tedious to always type in paths character by character, so there is a must-know convenience feature in the Bash shell (and many other shells). As you type path elements, pressing the **TAB** key will prompt the shell to attempt to auto-complete the path element.
> If you want to re-run a command you ran before, use the **ARROW** keys to cycle through your command history.
> If your terminal becomes too busy with command output, and you just want to start from a clean slate, use the `clear` command.

To **change directory**, run:
```
cd [/path/to/directory]
```
For example:
```
cd data
cd /workspaces/unixclass/data
cd ..
cd ~
cd # shorthand in most systems to go back to home directory
```

To **make directories**, run:
```
mkdir /path/to/directory
mkdir -p /path/to/directory_1 [/path/to/directory_2 ...]
```
For example:
```
mkdir data/sample_1
mkdir -p data/sample_2 data/sample_3
```

<br/>

## Copying, Moving, or Removing Files or Directories

To **copy files**, run:
```
cp [/path/to/source] [/path/to/destination]
```
For example:
```
cp data/my_file.csv data/sample_1/my_file.csv
cp data/my_file.csv data/sample_1/
cp data/my_file.csv data/sample_1/my_file_copy.csv # copy to new location with a new name
```

To **copy a directory** with its contents, use `cp` with the `-R` (recursive) flag:
```
cp -R data/sample_1 data/sample_4
```

To **move** files or directories, use:
```
mv [/path/to/source] [/path/to/destination]
```
For example:
```
mv data/my_file.csv data/sample_4/my_file.csv
mv data/my_file.csv data/sample_4/
mv data/my_file.csv data/sample_4/my_file_new.csv # move to new location with a new name
```
When using `mv` in the same location, it is effectively **renaming** the file or directory:
```
mv data/my_file.csv data/my_file_backup.csv
mv data/sample_1 data/sample_5
```

To **remove** files, use:
```
rm [/path/to/file]
```
For example:
```
rm data/sample/my_file.csv
```
To **remove** a directory together with its contents, use `rm` with the `-r` (recursive) flag:
```
rm -r data/sample_5
```

> [!CAUTION]
> Unlike in Windows or macOS, the Unix command line assumes that you know what you are doing. It DOES NOT ask you for confirmation when deleting or overwriting files or directories. Therefore when using commands like `cp`, `mv`, and `rm`, you should measure twice and cut once, and make sure you do not accidentally erase an existing file with the same name or delete a file with a similar name. There is no "trash can" or "recycle bin" for these commands.

> [!TIP]
> **Special Characters**
> The **question mark** `?` is a wildcard character that denotes one character when specifying file names:
> ```
> cp data/sample/my_file_?.csv data/sample_1/ # => my_file_1.csv, my_file_2.csv, ...
> ```
> The **asterisk** `*` is a wildcard character that denotes any number of characters when specifying file names:
> ```
> cp data/sample/*.csv data/sample_1/ # => my_file.csv, another_file.csv, yet_another_file.csv, ...
> ```

<br/>

## Creating or Editing Files

Most people use a dedicated GUI-based text editor or IDE (integrated development environment) to create or edit files, but if you do not have access to one in a terminal environment, there are a variety of terminal-based text editors. The most commonly pre-installed one is `nano`.
```
nano [/path/to/file]
```
For example:
```
nano sample/my_file.txt
```

> [!TIP]
> At the bottom of the `nano` screen, you will find a list of keyboard shortcuts to help you with common tasks. Most importantly, press `Ctrl+O` to save (write out) the file, and press `Ctrl+X` to exit the nano program.

> [!TIP]
> You system may have other text editors installed, such as `vi`, `vim`, etc. They all have their own keyboard shortcuts.

> [!TIP]
> To see if a command or program is available on your system, run:
> ```
> which [command_name]
> ```
> For example:
> ```
> which nano
> which vi
> which curl
> which wget
> ```

<br/>

## Downloading Files

Now let's get some sample data files on to our system, so that we can work with them. We can use the widely available `curl` command to download them from the internet.
```
curl -L -o shakespeare.txt https://bit.ly/cwml-shakespeare
curl -L -o covid.csv https://bit.ly/ct-covid-21-22
```
OR use the `wget` command if it's available:
```
wget https://bit.ly/cwml-shakespeare -O shakespeare.txt
wget https://bit.ly/ct-covid-21-22 -O covid.csv
```

<br/>

## Reading Files

Now we can take a look at those files! Before we look at the contents of the files, we can get some useful information about them. Of course, we can do a `ls -l` to find out its size:
```
ls -l shakespeare.txt # size in bytes
ls -lh shakespeare.txt # size in human-readable units
```
We can get the **character, word, and line counts** of the file:
```
wc [/path/to/file]
```
For example,
```
wc shakespeare.txt # character, word, line counts
wc -l covid.csv # line count only, useful for tabular data
```

Now let's try to **display the contents** of the file (**concatenate**) using the `cat` command:
```
cat [/path/to/file]
```
For example:
```
cat shakespeare.txt
```

We just "read" the complete works of Shakespeare in 5 seconds, but that's not helpful! Now let's try to read them page by page using the `more` command:
```
more [/path/to/file]
```
For example:
```
more shakespeare.txt
```

> [!TIP]
> With `more`, you can use the spacebar to **scroll** pages and type in `:q` to **quit** the interface.

For large tabular data files, we might just want to look at the **first a few rows** to get a sense of the data. We can use the `head` command to achieve that:
```
head [/path/to/file]
```
For example:
```
head covid.csv # show the first 10 lines of data
```

Sometimes it is more important to look at the **end of a file**, especially if the rows are ordered chronologically and you want to look at the most recent data. We can use the `tail` command for that:
```
tail [/path/to/file]
```
For example:
```
tail covid.txt
```

> [!TIP]
> For `head` and `tail`, we can specify the `-n` option for the number of lines to display:
> ```
> head -n 100 covid.csv # display the first 100 lines
> tail -n 50 covid.csv # display the last 50 lines
> ```

<br/>

## How to Get Help

We cannot possibly list all Unix commands in this tutorial, as there are so many of them, and they vary from system to system. However, you can learn how to use almost any command yourself. Arguably the most important command you should know is the `man` command. It prints the **manual** of a specified command, allowing you to find out exactly what a command does, what options are available, and what syntax you should follow.
```
man command_name
```
For example, if we want to read the manual of the `ls` command, we can run:
```
man ls
```
Here we can see a brief description of the command, the general syntax, and what each option does.

Sometimes (not always), commands may have the `--help` or `-h` option built in, which may give you more information on how to use these commands.

Of course, you can also use the good old search engine and a trusted site to find the answer to any questions you may have.

<br/>

## Directing Command Output

The `--output` flag
The `>` and `>>` signs
The `|` sign

<br/>

## Getting Started with Shell Scripting

Why don't we start with an exercise. What do these commands do?
```
cat shakespeare.txt | tr -sc [:alpha:] '\n' | sort -f | uniq -ci | sort -bnfr > results-shakespeare.txt

head -n 101 covid.csv | tail -n 100 | sort -r | cut -d , -f 2,3,4,5 > results-covid.txt
```

Now that we know what these commands do, let's put them in a file so that we never have to type in such a long command again! You can use commands like `nano`, or your favorite text editor to create a file with this content:
```
#! /bin/bash

date

read -p "Which file would you like to process?" file

echo "Now counting words used in $file ..."
cat $file | tr -sc [:alpha:] '\n' | sort -f | uniq -ci | sort -bnfr > results-${file}
echo "Done. Here are the top 10 frequently used words in $file:"
head results-${file}

date
```

If we want to run the same process for a batch of files, we can write a loop:
```
#! /bin/bash

date

for file in *.txt
do
echo "Now counting words used in $file ..."
cat $file | tr -sc [:alpha:] '\n' | sort -f | uniq -ci | sort -bnfr > results-${file}
echo "Done. Here are the top 10 frequently used words in $file:"
head results-${file}
done

date
```

<br/>

## File Permission

`ls -l` output

Octal Representation of File Permission

`chmod` command

`chown` command

`sudo` command

<br/>

## Running Your Shell Script

```
chmod +x file_name
./file_name
```

<br/>

## Summary

