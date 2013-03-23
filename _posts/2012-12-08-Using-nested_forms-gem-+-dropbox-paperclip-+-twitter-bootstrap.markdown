---           
layout: post
title: Using nested_forms gem + dropbox-paperclip + twitter-bootstrap
date: 2012-12-08 08:25:52 UTC
updated: 2012-12-08 08:25:52 UTC
comments: false
categories: photo-upload multi-model-forms dropbox-rails rails-nested-forms bootstrap rails-paperclip paperclip-dropbox paperclip file-storage-rails accepts_nested_attributes_for nested_form nested-forms
---

#### This is a tutorial about using nested_forms gem with dropbox-paperclip plugin on Heroku to create a multiple photo upload albums interface with twitter bootstrap

[Demo application](http://ashish-albums.herokuapp.com)
   
+ Create a new rails app and add the gems to Gemfile.**  
   
        paperclip
        paperclip-dropbox
        nested_form 

+ Create 3 models**  
   
        rails g model User name:string  
        rails g model Album name:string user_id:integer
        rails g model Photo tags_name:string album_id:integer

+ Adding relationships among models
#### in app/models/user.rb

        has_many :albums, :dependent =:destroy  
        accepts_nested_attributes_for :albums  
        attr_accessible :name, :albums_attributes  
        validates_presence_of :name    
        belongs_to :user   
        has_many :photos, :dependent =:destroy  
        accepts_nested_attributes_for :photos, :allow_destroy =true  
        attr_accessible :name, :photos_attributes  
        validates_presence_of :name   
        belongs_to :album  
        attr_accessible :avatar, :tags_name  
        has_attached_file :avatar,  
        :storage =:dropbox,  
        :dropbox_credentials ="#{Rails.root}/config/dropbox.yml",  
        :styles ={ :thumb ="100x100" },  
        :dropbox_options ={  
        :path =proc { |style| "#{style}/#{id}_#{avatar.original_filename}"}  
        }  
        validates_presence_of :avatar   
   
+ Adding a controller and a few actions**  
   
        rails g controller Users 
        add following code to the controller 
        def index  
         @users = User.all  
        end  
          
        def new  
         @user = User.new  
        end  
          
        def create  
         @user = User.new(params[:user])  
         if @user.save  
          redirect_to root_url  
          else  
           redirect_to root_url  
         end  
        end  
          
        def show_albums  
         @albums = Album.find(params[:id])  
        end  
          
        def destroy  
         @user = User.find(params[:id])  
         @user.destroy  
         redirect_to root_url  
        end 

  
+ Adding routes to routes.rb

        resources :users do  
         member do  
         get 'show_albums'  
         end  
        end  
        root :to ='users#index'  

+ Creating views for forms and data show  

        index.html.erb
        new.html.erb
        show_albums.html.erb
        _album_fields.html.erb
        _photo_fields.html.erb

  
 + Adding form html to views**  
  #### in index.html.erb :**  
        <%= link_to 'New User', new_user_path , :class => 'btn btn-medium btn-primary pull-right'%>
        <table class="table table-striped">
        <tr>
        <th>Name</th>
        <th>Album Names</th>
        <!--th>Tags</th-->
        <th>Destroy</th>
        </tr>
        <% @users.each do |user| %>
        <tr>
        <td><%= user.name %></td>
        <td>
          <% (user_albums_link user).each do |album_link| %>
            <%= album_link.html_safe %>
          <% end %>
         <% thumbnails = show_photo_thumbnails(user.albums) if user.albums %>
         <% if thumbnails %>
            <% thumbnails.each do |thumb| %>
              <%= thumb.html_safe  %>
            <% end %>
         <% end %>
        </td>
        <!--td>
          <%#= tags user.albums %>
        </td-->
        <td>
            <%= link_to t('.destroy', :default => t("helpers.links.destroy")),
              user_path(user),
              :method => :delete,
              :data => { :confirm => t('.confirm', 
              :default => t("helpers.links.confirm", :default => 'Are you sure?')) },
              :class => 'btn btn-mini btn-danger' %>
        </td>
        </tr>
        <% end %>
        </table>
        <br />
  
  
 
+ in new.html.erb
  
        <%= nested_form_for @user, :html => { :multipart => true } do |f| %>
        <div class="controls">
          Username :
          <%= f.text_field :name, :class => 'text_field' %>
        </div>
        <%= f.fields_for :albums %>
        <%= f.link_to_add "Add an album", :albums %>
        <br />
        <br />
        <div class="controls">
          <%= f.submit nil, :class => 'btn btn-primary' %>
        </div>
        <% end %>

+ in _album_fields.html.erb
  
        <div class="controls">
          Album Name :
          <%= f.text_field :name, :class => 'text_field' %>
          <%= f.link_to_remove "Remove this album" %>
          <%= f.fields_for :photos %>
            <p>
            <%= f.link_to_add "Add a photo", :photos %>
            </p>
        </div>

+ in _photo_fields.html.erb
  
        <div class="controls offset1">
          File :
          <%= f.text_field :tags_name %>
          <%= f.file_field :avatar %>
          <%= f.link_to_remove "Remove this photo" %>
        </div>

+ in show_albums.html.erb
  
        <% thumbnails = get_photos(@albums) if @albums %>
         <% if thumbnails %>
            <% thumbnails.each do |thumb| %>
              <%= thumb.html_safe  %>
            <% end %>
         <% end %>
         <%= show_tags @albums %>

+ Add dropbox.yml in config folder with following data :**    
   
        app_key:    
        app_secret:    
        access_token:    
        access_token_secret:    
        user_id:
    
+ These variables are Environment variables in environments files.  
  
+ For detailed setup for paperclip-dropbox gem [paperclip-dropbox](https://github.com/janko-m/paperclip-dropbox)  
  
+ Setup Twitter Bootstrap **  

        rails generate bootstrap:install less  
        rails g bootstrap:layout application fixed**Step 10 : Run the application :**  
        bundle  
        rake db:create  
        rake db:migrate  
        rails s  
   
   
   
  
   
   
   
   
  
  