---
layout: post
title: Using Rubymotion for iOS application development
category: posts
---
## TCS RSS Feed Reader  123

[TCS RSS Feed](https://github.com/upadhyay-ashish/TCSRssReader)

This is an iOS application build using 

+ [Rubymotion](http://rubymotion.com/)
+ [Bundler](http://gembundler.com/)
+ [CocoaPods](http://cocoapods.org/)
+ [NanoStoreInMotion](https://github.com/siuying/NanoStoreInMotion)
+ [Pixate iOS Styling Framework](www.pixate.com)

### Running on Simulator/Device

You will need Rubymotion installed on your Mac.

  1. Clone repo <code> git clone git@github.com:upadhyay-ashish/TCSRssReader.git</code>
  2. Bundle gems <code> bundle install </code>
  3. Setup cocoapods <code> pod setup </code>
  4. Setup Developer license reference in the Rakefile 
  5. To run on simulator <code> rake </code> else to run on a Device <code> rake device </code>
  6. To create a distribution IPA <code> rake archive:distribution </code>
  

### Screenshots 

  ![Alt Icon](/images/March-23-2013/icon.png)  ![Alt Icon](/images/March-23-2013/menu.png)  
  ![Alt Icon](/images/March-23-2013/events.png)  ![Alt Icon](/images/March-23-2013/news.png)   
  ![Alt Icon](/images/March-23-2013/press_releases.png)  


###Suggestions ?

Please log an issue [here](https://github.com/upadhyay-ashish/TCSRssReader/issues)

[ashish.upadhyaye@gmail.com](ashish.upadhyaye@gmail.com)


---