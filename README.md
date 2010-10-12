RailsTinyMCE,i find it can not be used in rails3,so i changed it for rails3.
----------------------------------------------------------------------
cheng it
it's author is http://github.com/sandipransing/rails_tiny_mce

i have found another Rich Text Editor kindeditor and make a gem in http://github.com/doabit/kindeditor


# RailsTinyMCE - A Rich Text Editor for ruby on rails

TinyMCE is a javascript rich text editor. It is easy to integrate with blogs, cms, messages and mailers.

Plugin uses jquery paperclip plugin for upload support.

Features
--------------

- Provides rich text editor 
- Customisable TinyMCE plugins
- Easy to integrate
- Supports Image upload & insert
- Supports Media upload & Youtube embed 
- TODO: Document upload plugin

1. Install rails_tiny_mce plugin using
--------------------- 
   	rails plugin install git://github.com/doabit/rails_tiny_mce.git
 
    rails g rails_tiny_mce_migration
    
    rake db:migrate
 
2. Install jqeury rails.js using
----------------
  http://github.com/rails/jquery-ujs/blob/master/src/rails.js 
download jqeuery.js ,put it in javascripts/
 
3. Install dependent plugins(if you didn\'t)
---------------------
    rake rails_tiny_mce:plugins
 
Above command will copy *paperclip, responds_to_parent, will_paginate* plugins to vendor/plugins directory.
 
- **paperclip** git://github.com/thoughtbot/paperclip.git(rails 3 :gem "paperclip")
- **responds_to_parent** http://responds-to-parent.googlecode.com/svn/trunk
- **will_paginate** git://github.com/mislav/will_paginate.git (rails 3 gem "will_paginate","3.0.pre")
 
4. In your layout add following lines
-----------------------
    <%= javascript_include_tag "jquery","rails"%>
    <%= javascript_include_tiny_mce_if_used %>
    <%= tiny_mce if using_tiny_mce? %>
 
5. Inside controller class on top add following lines
-------------------------------------
    uses_tiny_mce(:options => AppConfig.default_mce_options, :only => [:new, :edit])
 
This AppConfig.default_mce_options is in *config/initializers/tiny_mce_plus_config.rb*, you could change the setting there
 
6. In your view add class mceEditor to text_area
-----------------------------
Then append the following to the text area you want to transform into a TinyMCE editor.
 
    :class => "mceEditor"
 
7. Install file lists!
-------------------------
    rake rails_tiny_mce:install
 
will Install following files:
 
    app
      |-- controller
        |-- attachments_controller.rb
      |-- helpers
        |-- remote_link_renderer.rb
      |-- models
        |-- print.rb
        |-- video.rb
      |-- views
        |-- attachments
           |-- _show_attachment_list.html.erb
		   |-- manage.js.erb
		   |-- create.js.erb
    config
      |-- initializers
        |-- tiny_mce_plus_config.rb
    public
      |-- images
        |-- tiny_mce
      |-- javascripts
        |-- tiny_mce
 
You may custom the config in tiny_mce_plus_config.rb.
 
## Attention Note:
* Do not put *\<p> \</p>* around the textarea.
* If you are using *old will_paginate plugin*, change the *url_for* to *url_option* in *remote_link_renderer.rb*
 
## Example use:

- Create CRUD for post
    
    rails generate scaffold post title:string description:text
 
- Run Migrations
    
    rake db:migrate
 
- Add following line to *posts_controller.rb*
    
    uses_tiny_mce(:options => AppConfig.default_mce_options, :only => [:new, :edit])
 
- Open */views/posts/new.html.erb* and */views/posts/edit.html.erb*

- Modifiy following line
    
    <%= f.text_area :description %>
to
    <%= f.text_area :description, :class => "mceEditor" %>
 
## Contributors

1. Sandip Ransing, Josh Software Private Limited
2. ilake

thats, all

any sugestions? **san2821 at gmail.com** or **sandip at joshsoftware.com** released under the MIT license
