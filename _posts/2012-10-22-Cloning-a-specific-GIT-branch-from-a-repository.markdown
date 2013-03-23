---           
layout: post
title: Cloning a specific GIT branch from a repository
date: 2012-10-22 08:15:13 UTC
updated: 2012-10-22 08:15:13 UTC
comments: false
categories: git clone git git clone branch clone git branch cloning a branch git
---

+ Clone the master branch

    	git clone <repo master>

+ Clone the specific GIT branch

    	git fetch origin +branchname:branchname

+ Switch to the branch

	    git checkout branchname

+ Check the file difference between the master and the branch 

		git diff --name-status master..sibos