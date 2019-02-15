---
layout: post
title: "Untracking Files After Modifying gitignore"
date: 2019-02-12
tags: [git, gitignore]
---

We have tracked some files but then we need to ignore them. Here the steps to untrack them all:

## 1. Commit all changes

Run `commit` command to commit all changes including `.gitignore` file

```bash
git commit -m "update .gitignore"
```

> Note: `-m` is paramater to add message to our commit

## 2. Clear all tracking

Run the following command to clear the cache. The command will only clear the tracking, not the files themself.

```bash
git rm -r --cached .
```

## 3. Re-track all files

Run the following command to stage all files and implements `.gitignore` file.

```bash
git add .
```

## 4. Commit all staged files

Commit all staged files by running the following command:

```bash
git commit -m ".gitignore fix"
```

Now, our repository is clean.

---

Source links:<br />
[Untrack files already added to git repository based on .gitignore](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)