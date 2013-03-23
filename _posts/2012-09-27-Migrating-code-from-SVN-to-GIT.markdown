---           
layout: post
title: Migrating code from SVN to GIT
date: 2012-09-27 19:03:52 UTC
updated: 2012-09-27 19:03:52 UTC
comments: false
categories: migrating repositories svn git repo migration push to git from svn svn git migration move svn to git svn to git git svn clone git repo from svn migrate svn repo
---

+ Install <code>git-svn</code> on ubuntu or linux

		git-svn clone <svn repo link>  my_project  

+ You need to do a bit of post-import cleanup. For one thing, you should clean up the weird references that git svn set up. First you’ll move the tags so they’re actual tags rather than strange remote branches, and then you’ll move the rest of the branches so they’re local.  
To move the tags to be proper Git tags, run

		cp -Rf .git/refs/remotes/tags/* .git/refs/tags/  
		rm -Rf .git/refs/remotes/tags  

+ This takes the references that were remote branches that started with tag/ and makes them real (lightweight) tags.
Next, move the rest of the references under refs/remotes to be local branches:

		cp -Rf .git/refs/remotes/* .git/refs/heads/  
		rm -Rf .git/refs/remotes  

+ Now all the old branches are real Git branches and all the old tags are real Git tags. The last thing to do is add your new Git server as a remote and push to it. Here is an example of adding your server as a remote:
 
		git remote add origin git@my-git-server:myrepository.git  
+ Because you want all your branches and tags to go up, you can now run this  

		git push origin --all  