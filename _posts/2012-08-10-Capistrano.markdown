---
layout: post
title: Capistrano 
category: posts
---

## Too many arguments while deployment

**Issue : shell command failed with return code 33024**

It's a <code>ruby + git clone + windows</code> issue.

__ If we chain commands with while calling system(cmd) from ruby, chaining <code>git clone</code> with other commands is not fine. Git clone perceives the chained commands as its own continuation, i.e. as a destination directory, unless I run it from the command line. 
__ 

As we couldn't find any references or solutions to this problem on the internet, I put a hack to capistrano code, so <code>git clone</code> is executed separately.

In  
<code>
ruby-directory\lib\ruby\gems\1.8\gems\capistrano-2.5.18\lib\capistrano\recipes\deploy\strategy\base.rb 
</code>

** after the line 53 (cmd = cmd.split...) **
add the following lines:
<blockquote>
<pre>
<code>
if cmd =~ /\s\&\&\s/ && cmd =~ /^git\s+clone/
   cmd1, cmd = cmd.split(" && ", 2)
   super(cmd1)
end
</code>
</pre>
</blockquote>

it checks if it's a chained command and the first command is "git clone", and if such it executes it separately. It may not work for all possible cases.

### Also you can try using ubuntu from your local.

---