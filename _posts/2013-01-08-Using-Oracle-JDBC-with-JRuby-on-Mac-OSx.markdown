---           
layout: post
title: Using Oracle JDBC with JRuby on Mac OSx
date: 2013-01-08 15:32:14 UTC
updated: 2013-01-08 15:32:14 UTC
comments: false
categories: jdbc ruby jdbc mac
---

### Please follow the below steps to create a jruby library to connect to any oracle database on Mac OS x using Java ODBC drivers.


+ Create the Library folder and the Ruby file. eg `Sample.rb`
+ Add Gemfile to enable using jruby to connect to the database
+ Add the following gems to the Gemfile  

      gem 'activerecord'
      gem "activerecord-jdbc-adapter"


+ In the ruby file Sample.rb here please use the following lines and then write appropriate  code to access the data.

      class Person < ActiveRecord::Base
          establish_connection(
            :adapter  => 'jdbc',
            :driver   => 'oracle.jdbc.driver.OracleDriver',
            :url      => 'jdbc:oracle:thin:@server:port/sid',
            :username => 'ors',
            :password => 'ors'
            )
            self.table_name = :table_name_here
              def self.all
                connection.select_all <<-SQL
                        select * from table_name_here
                   SQL
              end
       end

+ Go to terminal ,run  

      bundle install 
      jruby Sample.rb


+ If there is a driver not found error please download the driver from oracle site here 
and place it in `/Library/Java/Extensions/` on your mac.
