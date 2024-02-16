# The Very Basics of the Unix Command Line

## Outline
This class will introduce you to:
* Accessing and navigating a Unix-based operating system with a terminal.
* Basics of running a Unix command.
* Essential command line tools for reading and editing files.
* Fundamentals of the Unix file system permissions.
* The basics of automating tasks with shell scripting.

## Getting System Information

You can get some basic system information by running:
```
uname -a
```
The system returns your user name on the system if you run:
```
whoami
```
To return the current system date and time, run:
```
date
```
## Navigating the File System
To print the **present working directory**, run:
```
pwd
```
To **list** the contents of a directory, run:
```
ls (/path/to/directory)
ls -l (/path/to/directory)
ls -la (/path/to/directory)
ls -lah (/path/to/directory)
ls -lahr (/path/to/directory)
```
To **change directory**, run:
```
cd (/path/to/directory)
```
To **make directories**, run:
```
mkdir /path/to/directory
mkdir -p /path/to/directory_1 (/path/to/directory_2 ...)
```
To **copy** files or directories, use:
```
cp
```
To **move** or **rename** files or directories, use:
```
mv
```
To **remove** files or directories, use:
```
rm
```

## Reading and Editing Files

> [!TIP]
> To see if a command is available on your system, run:
> ```
> which [command_name]
> ```
> For example:
> ```
> which curl
> which wget
> ```

Now let's get some data files to our system to work with. We can use the widely available `curl` command:
```
curl -L -o shakespeare.txt https://bit.ly/cwml-shakespeare
curl -L -o ct-covid-21-22.csv https://bit.ly/ct-covid-21-22
```
OR use the `wget` command:
```
wget https://bit.ly/cwml-shakespeare -O shakespeare.txt
wget https://bit.ly/ct-covid-21-22 -O ct-covid-21-22.csv
```
Now we can take a look at those files! First, we can get a character, word, or line count of the file:
```
wc [/path/to/file]
```
For example,
```
wc ./shakespeare.txt
wc -l ./ct-covid-21-22.csv
```
Now let's try to read the contents of the file using the `cat` command:
```
cat [/path/to/file]
```
For example:
```
cat ./shakespeare.txt
```
We just "read" the complete works of Shakespeare in 5 seconds, but that's not helpful! Now let's try to read the file page by page using the `more` command:
```
more [/path/to/file]
```
For example:
```
more ./shakespeare.txt
```
Much better! You can use the spacebar to scroll pages and type in `:q` to quit the `more` interface.

For tabular data, it might be helpful to get a sense of what the data looks like. If the data file is large, we might just want to look at the first a few rows to get a sense. We can then use the `head` command:
```
head [/path/to/file]
```
For example:
```
head ./ct-covid-21-22.csv
```
Sometimes it is more important to look at the end of a data file, especially if the data is chronological and you want to look at the most recent data. We can then use the `tail` command.
```
tail [/path/to/file]
```
For example:
```
tail ./ct-covid-21-22.txt
```
For `head` and `tail`, we can specify the `-n` option for the number of rows to return:
```
head -n 100 ./ct-covid-21-22.csv
tail -n 50 ./ct-covid-21-22.csv
```

