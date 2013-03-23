---           
layout: post
title: Replacing master with a branch GIT
date: 2013-02-25 11:49:27 UTC
updated: 2013-02-25 11:49:27 UTC
comments: false
categories: merge master rename a branch git. git branch
---

### This will help us to overwrite the master branch with a new branch incase the new branch is in a better state than the master  

        git checkout seotweaks
        git merge -s ours master
        git checkout master
        git merge seotweaks  

