---
layout: post
title: Git Hooks: No Large Files!
date: 2014-08-22 12:00:00
categories: git bash
author: Nick Jacob
---

One of the version control mistakes I really worry about, especially when working in repos with a chance of very large files (e.g., trained neural nets, data sets, log files), is the checking in of relatively large data that is heavily modified by scripts (not by users). While it can be useful to have version control on something like neural net parameters, I think this is better accomplished by versioned keys in s3 corresponding to git tags, or to a `CHANGES.txt` file or equivalent. 

To avoid accidentally adding these files for all users of a repo, I like using [git hooks](http://git-scm.com/book/en/Customizing-Git-Git-Hooks) to check the staging area before a commit. Here's a simple pre-commit hook that checks for large files:

{% gist 5a0c56ba451a6892ff14 %}

It would be nice to turn this script into a system that offers some kind of versioning for the large files (like s3 upload or renaming/gzipping as with logrotate), although at that point maybe you should just work more towards having your team involved more in maintaining a good repo/use of VCS.
