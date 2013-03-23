---           
layout: post
title: Action Mailer
date: 2011-11-10 20:15:45 UTC
updated: 2011-11-10 20:15:45 UTC
comments: false
categories: gmail email in ruby emails email rails html email in ror actionmailer email in ruby
---

##  For rails 3

Action Mailer allows you to send email from your application using a mailer
model and views.

This tutorial is about how to send an email using gmail free service in Ruby on Rails 3 and above</div>

### Creating Demo project

<code> rails new mail_demo –d mysql </code>

### Creating a User model

<code>rails g scaffold User name:string email:string content:string </code>

### Creating a Mailer model

<code> rails g mailer user_mailer </code>

### Setting up the development.rb for configuring application settings to
access mail smtp server

#### In development.rb
<blockquote>
<pre>
<code>
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
 :enable_starttls_auto =&gt; true,
 :address =&gt; 'smtp.gmail.com',
 :port =&gt; 587,
 :domain =&gt; 'your.domain.com',
 :authentication =&gt; :login,
 :content_type =&gt; "text/html",
 :user_name =&gt; 'username',
 :password =&gt; 'password'
}

config.action_mailer.perform_deliveries = true
config.action_mailer.raise_delivery_errors = true
</code>
</pre>
</blockquote>

Remember
these are the basic settings needed to send mails from gmail ,other server may
have different settings.

### Creating the mailer

Now we will write the method in user_mailer model to send the mail .Remember in the mailer model  :

<blockquote>
<pre>
<code>

def send_email(user)
   recipients  user.email
   from        "webmaster@example.com"
   subject     "Thank you for Registering"
   part :content_type => "text/html",
    :body => render_message("registration_confirmation", :user => user)
end

</code>
</pre>
</blockquote>

### Creating Email Template

<blockquote><pre><code> 
"http://www.w3.org/TR/html4/loose.dtd"&gt;
h3 { color: #f00; }
ul { list-style: none; }
Your account signup details are below
Name:  
Login: 
Image: 
Content: 
</code></pre></blockquote>

The method is referred to as deliver_send_email because rails appends it to a mailer method.Now
run the server and try creating a new user . The email is sent to the address
the user enters for the new record.