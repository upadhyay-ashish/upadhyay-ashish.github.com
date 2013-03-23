--- 
layout: post
title: Installing RMagick with Imagemagic on Windows 7/Vista
date: 2012-08-09 08:30:18 UTC
updated: 2012-08-09 08:30:18 UTC
comments: false
categories: rails rmagic imagemagick rmagick
---

Working with Windows 7 64bit and Ruby 1.9.3.

+ Install Ghostscript  
		<code>http://downloads.sourceforge.net/project/ghostscript/GPL%20Ghostscript/9.05/gs905w32.exe</code>

+ Install Imagemagick  
Use the 32 bit version, 64bit is not working.  
[Imagemagick](http://www.imagemagick.org/download/binaries/ImageMagick-6.7.6-1-Q16-windows-dll.exe)

		Install dev headers (Check!)
		Install into C:\opt\

+ Restart the console/cmd prompt/IDE/.. or just restart windows to make Imagemagick commands available

+ Install rmagick
<blockquote><pre><code></code>
	gem install rmagick --platform=ruby -- --with-opt-lib=C:/opt/ImageMagick-6.7.6-Q16/lib 
	--with-opt-include=c:/opt/ImageMagick-6.7.6-Q16/include
</pre></blockquote>