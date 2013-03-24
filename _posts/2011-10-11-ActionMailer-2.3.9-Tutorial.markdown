---           
layout: post
title: Action Mailer 2.3.9
date: 2011-11-10 20:05:14 UTC
updated: 2011-11-10 20:05:14 UTC
comments: false
categories: ruby send email ruby email rails email gmail email in ruby emails email rails ruby gmail actionmailer html email in ror actionmailer email in ruby actionmailer 2.3.9
---


# Easy email delivery and testing

Action Mailer allows you to send email from your application using a mailer model and views.  
This tutorial is about how to send an email using gmail free service in Ruby on Rails 2.3.9, for versions higher than this refer rails guides .

### Creating Demo project
{% highlight ruby linenos %}
    rails mail_demo –d mysql        

{% endhighlight %}
### Creating a User model
{% highlight ruby linenos %}
    ruby script/generate scaffold User name:string email:string content:string

{% endhighlight %}
### Creating a Mailer model
{% highlight ruby linenos %}
    ruby script/generate mailer user_mailer

{% endhighlight %}
### Setting up the development.rb for configuring application settings to access mail smtp server

#### In development.rb
{% highlight ruby linenos %}

    config.action_mailer.delivery_method = :smtp
    config.action_mailer.raise_delivery_errors = true
    config.action_mailer.smtp_settings = {
     :enable_starttls_auto =true,
     :address ='smtp.gmail.com',
     :port =587,
     :domain ='your.domain.com',
     :authentication =:login,
     :content_type ="text/html",
     :user_name =your full username example xyz@gmail.com',
     :password ='password'
    }

{% endhighlight %}

 
Remember these are the basic settings needed to send mails from gmail ,other server may have different settings .

### Creating the mailer
 
Now we will write the method in user_mailer model to send the mail .Remember in the mailer model

{% highlight ruby linenos %}
    def send_email(user)
     recipients user.emailÏ
     from "webmaster@example.com"
     subject "Thank you for Registering"
     part :content_type ="text/html",
     :body =render_message("registration_confirmation", :user =user)
    end

{% endhighlight %}
The from field can be your own or your domains email address. Please check if the from for field has invalid email the user will not be able to reply .

### Creating Email Template

Now we will create a view which would form a the email template .It is named as same as the method in the model user_mailer ie. Send_email.html.erb

{% highlight ruby linenos %}
    "http://www.w3.org/TR/html4/loose.dtd"&gt;
    h3 { color: #f00; }
    ul { list-style: none; }
    Your account signup details are below
    Name:  
    Login: 
    Image: 
    Content: 

{% endhighlight %}
In the end add a line to the create method of the Users_controller

{% highlight ruby linenos %}
    UserMailer.deliver_send_email(@user)
        
{% endhighlight %}

The method is referred to as deliver_send_email because rails appends it to a mailer method.

Now run the server and try creating a new user. The email is sent to the address the user enters for the new record.  
