# The Very Basics of the Unix Command Line

<br/>

## Outline

* Accessing and navigating a Unix-based operating system with a terminal.
* Basics of running a Unix command.
* Essential command line tools for reading and editing files.
* Fundamentals of the Unix file system permissions.
* The basics of automating tasks with shell scripting.

<br/>

## Getting System Information

You can get some basic **system information** by running the command `uname`:
```
uname
```
> [!TIP]
> **The Anatomy of a Command**. We can pass options (sometimes known as "flags") to a command. The syntax looks like this:
> ```
> command_name [options]
> ```
> For example:
> ```
> uname -a # single dash + single letter
> uname --all # double dashes + full name
> uname -s -v # multiple single letter flags
> uname --kernel-name --kernel-version # multiple full name flags
> uname -sv # shorthand for multiple single letter flags
> ```

To print your **user name** on the system, run:
```
whoami
```

To return the **current system date and time**, run:
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
ls
```

> [!TIP]
> **The Anatomy of a Command**. In addition to options or flags, most of the time we also need to pass **parameters** to a command. The syntax usually looks like one of these:
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
> **Relative path** vs **absolute path**. Relative path starts from the present working directory. For example, suppose we are currently in `/workspace/unixclass/data`:
> ```
> my_file.csv # Look for the file "my_file.csv" under present working directory
> sample/my_file.csv # Look for the file "data/my_file.csv" under present working directory
> ```
> Absolute path starts from the root directory, so it always starts with `/`:
> ```
> /workspace/unixclass/my_file.csv
> /workspace/unixclass/data/my_file.csv
> ```

> [!TIP]
> **Special characters in paths**. Pay attention to 4 special characters in paths. Forward slash `/` denotes the root directory at the beginning of a path, but is an element delimiter in the middle of a path:
> ```
> / # Root directory
> data/my_file.csv # Slash separates the directory "data" from the file "my_file.csv"
> /workspace/unixclass/data/my_file.csv # The first slash denotes the root directory, and the subsequent slashes separate path elements
> ```
> A single dot `.` represents the present working directory, and a double dot `..` represent the parent directory of the present working directory. Assume we are currently in `/workspace/unixclass/data`:
> ```
> ./my_file.csv # The same as simply "my_file.csv"
> ../README.md # Look for the file "README.md" in the parent directory
> ```
> Some you will also encounter the character `~`, which in most Unix systems denote the user's "home directory".

> [!TIP]
> **Convenience Features in Bash Shell**.
> The TAB key to autocomplete
> The ARROW keys to cycle through history
> The `clear` command to clear the terminal

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
cd # Shorthand in most systems to go back to home directory
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
To **copy** files, use:
```
cp [/path/to/source] [/path/to/destination]
```
For example:
```
cp data/my_file.csv data/sample_1/my_file.csv
cp data/my_file.csv data/sample_2/
```
To **copy** a directory with its contents, use `cp` with the `-R` (recursive) flag:
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
To **remove** an entire directory together with its contents, use `rm` with the `-r` (recursive) flag:
```
rm -r data/sample_5
```

> [!CAUTION]
> Unlike in Windows or macOS, the Unix command line assumes that you know what you are doing. It DOES NOT ask you for confirmation when deleting files or directories.

<br/>

## Creating or Editing Files

Most people use a dedicated GUI-based text editor or IDE (integrated development environment), but if you do not have access to one in a terminal only environment, there are a variety of terminal-based text editors. The most commonly pre-installed one is `nano`.
```
nano [/path/to/file]
```
For example:
```
nano sample/my_file.txt
```

> [!TIP]
> At the bottom of the `nano` screen, you will notice a guide of keyboard shortcuts to help you run common operations. For example, press `Ctrl+O` to save the file, and press `Ctrl+X` to exit the nano program.

> [!TIP]
> You system may have more advanced text editors than `nano`, such as `vi`, `vim`, `emac`, etc. They have their own keyboard shortcuts.

> [!TIP]
> To see if a command is available on your system, run:
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

Now let's get some data files to our system to work with. We can use the widely available `curl` command to download these files.
```
curl -L -o shakespeare.txt https://bit.ly/cwml-shakespeare
curl -L -o covid.csv https://bit.ly/ct-covid-21-22
```
OR use the `wget` command if available:
```
wget https://bit.ly/cwml-shakespeare -O shakespeare.txt
wget https://bit.ly/ct-covid-21-22 -O covid.csv
```

<br/>

## Reading Files

Now we can take a look at those files! First, we can get a character, word, or line count of the file:
```
wc [/path/to/file]
```
For example,
```
wc shakespeare.txt
wc -l covid.csv
```

Now let's try to read the contents of the file using the `cat` command:
```
cat [/path/to/file]
```
For example:
```
cat shakespeare.txt
```

We just "read" the complete works of Shakespeare in 5 seconds, but that's not helpful! Now let's try to read the file page by page using the `more` command:
```
more [/path/to/file]
```
For example:
```
more shakespeare.txt
```
Much better!

> [!TIP]
> You can use the spacebar to scroll pages and type in `:q` to quit the `more` interface.

For tabular data, it might be helpful to get a sense of what the data looks like. If the data file is large, we might just want to look at the first a few rows to get a sense. We can then use the `head` command:
```
head [/path/to/file]
```
For example:
```
head covid.csv
```
Sometimes it is more important to look at the end of a data file, especially if the data is chronological and you want to look at the most recent data. We can then use the `tail` command.
```
tail [/path/to/file]
```
For example:
```
tail covid.txt
```
For `head` and `tail`, we can specify the `-n` option for the number of rows to return:
```
head -n 100 covid.csv
tail -n 50 covid.csv
```

<br/>

## How to Get Help

We cannot possibly list all Unix commands in this tutorial, but you can learn how to become better yourself with a few very important tools. Arguably the most important command you should know is the `man` command. It's short for "manual", and it allows you find out exactly what a command does and what options are available and what syntax you should use:
```
man command_name
```

For example, if we want to check the manual of the `ls` command, we can run:
```
man ls
```
Here we can see a definition of the command, the general syntax, and what each option does.

Sometimes (not always) commands may have the `--help` or `-h` option built in, which may give you more information on how to use these commands.

Of course, you can also use the good old search engine and use a trusted site to find your answers.

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

