## Step 2 - The application

Create the User elements

![image](http://ruby.railstutorial.org/images/figures/demo_user_model.png)

```console
$ rails generate scaffold User name:string email:string
      invoke  active_record
      create    db/migrate/20130309034754_create_users.rb
      create    app/models/user.rb
      invoke    test_unit
      create      test/unit/user_test.rb
      create      test/fixtures/users.yml
      invoke  resource_route
       route    resources :users
      invoke  scaffold_controller
      create    app/controllers/users_controller.rb
      invoke    erb
      create      app/views/users
      create      app/views/users/index.html.erb
      create      app/views/users/edit.html.erb
      create      app/views/users/show.html.erb
      create      app/views/users/new.html.erb
      create      app/views/users/_form.html.erb
      invoke    test_unit
      create      test/functional/users_controller_test.rb
      invoke    helper
      create      app/helpers/users_helper.rb
      invoke      test_unit
      create        test/unit/helpers/users_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/users.js.coffee
      invoke    scss
      create      app/assets/stylesheets/users.css.scss
      invoke  scss
      create    app/assets/stylesheets/scaffolds.css.scss
```

Create the User database support

```console
$ bundle exec rake db:migrate
==  CreateUsers: migrating ====================================================
-- create_table(:users)
   -> 0.0014s
==  CreateUsers: migrated (0.0016s) ===========================================
```

It created the following pages:

|URI	        | Action |	Purpose                       |
|:-------------:|:------:|:-----------------------------:|
|/users         | index	  | page to list all users        |
|/users/1	    | show	  | page to show user with id 1   |
|/users/new	    | new	  | page to make a new user       |
|/users/1/edit	| edit	  | page to edit user with id 1   |

And the following RESTFUL endpoints:


|HTTP request | URI	           | Action | Purpose                       |
|----------------------------------------------------------------------|
|GET	      | /users	       | index	 | page to list all users       |
|GET	      | /users/1      | show	 | page to show user with id 1  |
|GET	      | /users/new	   | new	 | page to make a new user      |
|POST	      | /users	       | create	 | create a new user            |
|GET	      | /users/1/edit |	 edit    | page to edit user with id 1  |
|PUT	      | /users/1	   | update  | update user with id 1        |
|DELETE	      | /users/1	   | destroy |	delete user with id 1       |

Create the Microposts element

![image](http://ruby.railstutorial.org/images/figures/demo_micropost_model.png)

```console
$ rails generate scaffold Micropost content:string user_id:integer
      invoke  active_record
      create    db/migrate/20130309114438_create_microposts.rb
      create    app/models/micropost.rb
      invoke    test_unit
      create      test/unit/micropost_test.rb
      create      test/fixtures/microposts.yml
      invoke  resource_route
       route    resources :microposts
      invoke  scaffold_controller
      create    app/controllers/microposts_controller.rb
      invoke    erb
      create      app/views/microposts
      create      app/views/microposts/index.html.erb
      create      app/views/microposts/edit.html.erb
      create      app/views/microposts/show.html.erb
      create      app/views/microposts/new.html.erb
      create      app/views/microposts/_form.html.erb
      invoke    test_unit
      create      test/functional/microposts_controller_test.rb
      invoke    helper
      create      app/helpers/microposts_helper.rb
      invoke      test_unit
      create        test/unit/helpers/microposts_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/microposts.js.coffee
      invoke    scss
      create      app/assets/stylesheets/microposts.css.scss
      invoke  scss
   identical    app/assets/stylesheets/scaffolds.css.scss
```

Create the Microposts database support

```console
$ bundle exec rake db:migrate
==  CreateMicroposts: migrating ===============================================
-- create_table(:microposts)
   -> 0.0123s
==  CreateMicroposts: migrated (0.0124s) ======================================
```

It created the following RESTFUL endpoints:

|HTTP request | URI	               | Action  | Purpose                           |
|-------------------------------------------------------------------------------|
|GET	      | /microposts        | index	  | page to list all microposts       |
|GET	      | /microposts/1      | show	  | page to show micropost with id 1  |
|GET	      | /microposts/new	    | new     | page to make a new micropost      |
|POST	      | /microposts	        | create  | create a new micropost            |
|GET	      | /microposts/1/edit | edit    | page to edit micropost with id 1  |
|PUT	      | /microposts/1	    | update  | update micropost with id 1        |
|DELETE	      | /microposts/1	    | destroy |	delete micropost with id 1        |

Add size validation to Microposts editing `app/models/micropost.rb`

```ruby
class Micropost < ActiveRecord::Base
  attr_accessible :content, :user_id
  validates :content, :length => { :maximum => 140 }
end
```

Add associations between Users and Microposts by editing its model files:

![image](http://ruby.railstutorial.org/images/figures/micropost_user_association.png)

`app/models/user.rb`

```ruby
class User < ActiveRecord::Base
  attr_accessible :email, :name
  has_many :microposts
end
```

`app/models/micropost.rb`

```ruby
class Micropost < ActiveRecord::Base
  attr_accessible :content, :user_id

  belongs_to :user

  validates :content, :length => { :maximum => 140 }
end
```