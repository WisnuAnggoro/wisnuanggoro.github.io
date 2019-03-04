---
layout: post
title: "Essential Bash Commands"
date: 2019-03-04
tags: [bash, linux, ubuntu, terminal]
---

I personally prefer terminal instead of GUI to do simple and complex job. The first time I learned how to use Ubuntu, I also learned how to use the bash terminal. I found the following bash commands saved me to do various simple job.

## ls

`ls` stands for `list` and is used to display the list of folders and files in the current working directory. There are two flags we are going to use regularly: `-a` (to list all files including hidden files) and `-l` (to use long format display).

The following command will display all folder and files in current working directory:

```bash
ls -al
```

If we want to display other directory instead of current working directory, we can specify the path in the `ls` command.

The following will display all folders and files in `$HOME` directory:

```bash
ls -al ~
```

If we only need to display a spesific file, here's command that we can use to display only files with `html` extension:

```bash
ls -al ~ *.html
```

## cd

`cd` stands for `change directory`. Suppose we don't know the folder structure, we can list all folders by using `ls` command. The following command will move us to `/usr/bin`:

```bash
cd /usr/bin
```

There are two arguments that contains only `dot`, they are:

- `.` refers to current directory
- `..` is used to move up one folder

Suppose we are now in `$ROOT` folder and need to move to `/usr/bin` folder. We can run the following command to achive the need:

```bash
cd ./usr/bin
```

Now, we are in `/bin/usr` folder. To move up to `/bin` folder, we can simply run the following command:

```bash
cd ..
```

The `..` can be used to as many as we need it. If we are in `/bin/usr` folder and want to move to `/` folder, just run the following command:

```bash
cd ../..
```

If we are in `/bin/usr` folder and want to move to `/etc/apt` folder, the following command can be run to achieve the need:

```bash
cd ../../etc/apt
```

## mkdir

`mkdir` stands for `make directory`. A useful flag that can be used is `p` to ensure it creates parents folders as well if they don't exist already. The following command will create `page1` folder and will also create `docs` folder if it doesn't exist as `page1` folder's parents:

```bash
mkdir -p $HOME/docs/page1
```

## touch

We have successfully create a new directory using `mkdir` command. To create an empty file, we can use `touch` command. Run the following command to create an empty file named `go.sh` in current working directory:

```bash
touch go.sh
```

The `touch` command is actually used to update the access and or modification date of a file or directory without opening, saving or closing the file.

## cat

`cat` is a command to concatenate and display files' content to `stdout`. To add a bunch of line of text at the end of file, run the following command:

```bash
cat >> filename
```

After run the preceding command, we can write the text line to the console. Press `Ctrl+D` to insert inputed text in the end of `filename` file.

To create a new file instead of inserting text, we can run the following command to create a new file named `filename`:

```bash
cat > filename
```

## mv

`mv` stands for `move`and is used to move files or folders. It need at least two arguments: `SOURCE` and `DESTINATION`. For instance, the following is command to move `$HOME/app` to `/usr/bin`:

```bash
mv ~/app /usr/bin
```

After successfully running the preceding command, we will have `/usr/bin/app` folder.

## cp

`cp` stands for `copy` and is used to copy selected files or folders to another folder. Similar to `mv` command, it needs `SOURCE` and `DESTINATION` arguments too. The difference with `mv` command is `SOURCE` in `cp` command will still be there. The following command will copy file named `file.sh` in `$HOME` to `$HOME/doc2` folder:

```bash
cp ~/file1.sh ~/doc2
```

To copy a folder, we need to add `-r` flag which means `recursively`. The following command will copy `doc2` folder and all its content in `$HOME` directory to `$HOME/doc` folder:

```bash
cp -r ~/doc2 ~/doc
```

## rm

`rm` stands for `remove` and is used to delete files or folders. The following command will delete `file.sh` in current active directory:

```bash
rm file1.sh
```

To delete a directory, similar to `cp` command, we have to specify `-r` flags as well. The following will delete `doc1` folder in `$HOME` directory:

```bash
rm -r ~/doc1
```

NOTE: `rm -r /` will remove all folders and file inside `/` folder which means it will delete all contents in our computer.

## chmod

`chmod` stands for `change mode` and is used to set file or folder permission for `read`, `write`, and `execute` for the `user`, `members of current group` and `others`. It denote by three octal digit representing binary value.

## man

`man` stands for `manuals` and is used to print out the instruction of specified command.

---

Source links:<br />
[Top 10 Bash file system commands you can’t live without](https://medium.com/the-code-review/top-10-bash-file-system-commands-you-cant-live-without-4cd937bd7df1)<br />
[Bash scripting cheatsheet](https://devhints.io/bash)<br />
[13 Basic Cat Command Examples in Linux](https://www.tecmint.com/13-basic-cat-command-examples-in-linux/)<br />
[Linux chmod command](https://www.computerhope.com/unix/uchmod.htm)