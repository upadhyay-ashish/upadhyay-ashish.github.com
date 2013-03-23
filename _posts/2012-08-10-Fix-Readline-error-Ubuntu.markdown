---           
layout: post
title: Fix Readline error Ubuntu
date: 2012-08-10 19:18:12 UTC
updated: 2012-08-10 19:18:12 UTC
comments: false
categories: rvm readline readline error readline ubuntu readline heroku readline
---

		sudo apt-get install libreadline-dev

		cd ~/.rvm/src/ruby-1.8.7-p249/ext/readline

		ruby extconf.rb && make && make install