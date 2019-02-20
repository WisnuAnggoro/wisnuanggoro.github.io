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

## 3. git status

This command is used to display the state of the working directory and the staging area, including which changes have been staged, which haven’t, and which files aren’t being tracked by Git.

Run the following command to see the state of our repository:

```bash
git status
```

See also:<br />
[Git Status: Inspecting a repository](https://www.atlassian.com/git/tutorials/inspecting-a-repository)

## 4. git add

This command is used to move modified files to `staging index` which is area where Git stores files that is ready to commit.

Run the following command if we want to move all modified files into staging index:

```bash
git add .
```

Or run the following command to add specified files, for instance we want to add `index.html` and `css/site.css` files:

```bash
git add index.html css/site.css
```

To unstage files in staging index, run the following command:

```bash
git reset HEAD index.html
```

The preceding command will unstage `index.html` from staging index since `HEAD` is the last commit of the current branch.

See also:<br />
[git add docs](https://git-scm.com/docs/git-add)<br />
[Unstage Git](https://docs.gitlab.com/ee/university/training/topics/unstage.html)

## 5. git commit

This command is used to commit all files in staging index. We must provide a descriptive message when committing the staging index, for instance `add unit test for GetUser() function`

Run the following command to commit staging index in Git:

```bash
git commit -m "<descriptive message>"
```

See also:<br />
[git commit docs](https://git-scm.com/docs/git-commit)

## 6. git clone

This command is used to grab a complete copy of another user's repository. In GitHub, use pattern `https://github.com/USERNAME/REPOSITORY.git` as target repository. 

For instance, if we want to clone `https://github.com/WisnuAnggoro/hello-world`  to our active local directory, simply run following command:

```bash
git clone https://github.com/WisnuAnggoro/hello-world.git
```

See also:<br />
[Fetching a remote](https://help.github.com/articles/fetching-a-remote/)<br />
[git clone docs](https://git-scm.com/docs/git-clone)<br />
[How do you clone a Git repository into a specific folder?](https://stackoverflow.com/questions/651038/how-do-you-clone-a-git-repository-into-a-specific-folder)

## 7. git fetch

This command is used to grab all the new remote-tracking branches and tags **without merging** those changes into our own branches.

To fetch remote repository, we need to specify `remote-name` as the target. `origin` is common remote name.
Run the following command to fetch all branches from remote repository (`origin`):

```bash
git fetch origin
```

We can also fetch spesific remote branch to local repository. For instance, the following command will only fetch `master` branch in `origin`:

```bash
git fetch origin/master
```

See also:<br />
[Git Basics - Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

## 8. git remote

This command is used to add a new remote. Run the following command to create `origin` remote name:

```bash
git remote add origin https://github.com/user/repo.git
```

To find out our remote name, use this command: 

```bash
git remote -v
```

See also:<br />
[git remote docs](https://git-scm.com/docs/git-remote)

## 9. git merge

This command is used to combine our local changes with changes made by others.

Run this command to merge `remotename/branchname` to our active local branch:

```bash
git merge remotename/branchname
```

See also:<br />
[git merge docs](https://git-scm.com/docs/git-merge)

## 10. git pull

## 11. git push

## 12. git branch

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

## 13. git show-branch

This command is used to show branches and their commits. Just simply run the following command to show all branches and their commits:

```bash
git show-branch
```

See also:<br />
[git show-branch docs](https://git-scm.com/docs/git-show-branch)

## 14. git checkout

This command is used to switch to different local branches. Run the following command to switch to `other-branch`:

```bash
git branch other-branch
```

To create and switch to a `new-branch`, run the following command:

```bash
git branch -b new-branch
```

See also:<br />
[git checkout docs](https://git-scm.com/docs/git-checkout)

---

Source links:<br />
[Essential git commands every developer should know](https://medium.com/@nendhruv/essential-git-commands-every-developer-should-know-1249d4d597b5)<br />
[Git for beginners: 12 commands you need to know](https://blog.prototypr.io/git-for-beginners-12-commands-you-need-to-know-e084cce9cc94)<br />
[Most Basic Git Commands with Examples – a Welcome Introduction to Git](https://rubygarage.org/blog/most-basic-git-commands-with-examples)