---
layout: post
title: "Essential GIT Commands"
date: 2019-01-30
tags: [git]
---

## 1. git config

This command used to get and set configuration variables that control all aspects of how Git looks and operates. Use `--list` to get all configuration as following command:

```bash
git config --list
```

Use the following two commands to set name and email in global level:

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
See also:<br />
[Getting Started - First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)<br />
[Bitbucket Tutorial](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config)

## 2. git init

This command is used to create an empty Git repository. Simply run the following command to initialize Git repository:

```bash
git init
```

To start a new Git repository for an existing code base, run the following commands in the main folder of our code base:

```bash
git init
git add .
git commit
```

See also:<br />
[git init docs](https://git-scm.com/docs/git-init)

## 4. git status

## 5. git add

## 6. git commit

## 7. git clone

This command is used to grab a complete copy of another user's repository. In GitHub, use pattern `https://github.com/USERNAME/REPOSITORY.git` as target repository. 

For instance, if we want to clone `https://github.com/WisnuAnggoro/hello-world`  to our active local directory, simply run following command:

```bash
git clone https://github.com/WisnuAnggoro/hello-world.git
```

See also:<br />
[Fetching a remote](https://help.github.com/articles/fetching-a-remote/)<br />
[git clone docs](https://git-scm.com/docs/git-clone)<br />
[How do you clone a Git repository into a specific folder?](https://stackoverflow.com/questions/651038/how-do-you-clone-a-git-repository-into-a-specific-folder)

## 8. git fetch

This command is used to grab all the new remote-tracking branches and tags **without merging** those changes into our own branches.

To fetch remote repository, we need to specify `remote-name` as the target. `origin` is common remote name. Run the following command to fetch all branches from remote repository:

```bash
git fetch origin
```

We can also fetch spesific remote branch to local repository.

See also:<br />
[]()

## 9. git remote

## 10. git merge

## 11. git branch

This command is used to list, create, or delete branches. To list local branches only, simply run the following command:

```bash
git branch
```

To list all branchss in both local and remote, run the following command:

```bash
git branch -a
```

When listing all branches in both local and remote repositories, press `d` to continue to next list and press `q` to quit the list.

To delete local branch, we can run the following command:

```bash
git branch -d [branch_name]

```

The `-d` argument stands for `--delete` which will delete the local branch only if we have already pushed and merged it to remote branches.

Another delete branch command is as follow:

```bash
git branch -D [branch_name]
```

The `-D` argument stands for `--delete --force`. The preceding command will delete `branch_name` branch regardless of its push and merge status.

For **SAFETY REASON**, please use only `-d` argument when deleting local branch.

See also:<br />
[git branch docs](https://git-scm.com/docs/git-branch)<br />
[How to get the current branch name in Git?](https://stackoverflow.com/a/6245587)<br />
[Delete a local and a remote GIT branch](https://koukia.ca/delete-a-local-and-a-remote-git-branch-61df0b10d323)

## 12. git show-branch

This command is used to show branches and their commits. Just simply run the following command to show all branches and their commits:

```bash
git show-branch
```

See also:<br />
[git show-branch docs](https://git-scm.com/docs/git-show-branch)

## 13. git checkout