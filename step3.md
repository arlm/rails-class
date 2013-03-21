## Step 3 - Static pages

Add testing libraries by editing `Gemfile`

```ruby
group :development, :test do
  gem 'sqlite3'
  gem 'rspec-rails', '2.11.0'
end

group :test do
  gem 'capybara', '1.1.2'
end
```

Install the gem install

```console
$ bundle update
Fetching gem metadata from https://rubygems.org/.........
Fetching gem metadata from https://rubygems.org/..
Using rake (10.0.3) 
Using i18n (0.6.4) 
Using multi_json (1.6.1) 
Using activesupport (3.2.12) 
Using builder (3.0.4) 
Using activemodel (3.2.12) 
Using erubis (2.7.0) 
Using journey (1.0.4) 
Using rack (1.4.5) 
Using rack-cache (1.2) 
Using rack-test (0.6.2) 
Using hike (1.2.1) 
Using tilt (1.3.4) 
Using sprockets (2.2.2) 
Using actionpack (3.2.12) 
Using mime-types (1.21) 
Using polyglot (0.3.3) 
Using treetop (1.4.12) 
Using mail (2.4.4) 
Using actionmailer (3.2.12) 
Using arel (3.0.2) 
Using tzinfo (0.3.36) 
Using activerecord (3.2.12) 
Using activeresource (3.2.12) 
Using bundler (1.2.3) 
Installing nokogiri (1.5.6) with native extensions 
Installing ffi (1.4.0) with native extensions 
Installing childprocess (0.3.9) 
Using rubyzip (0.9.9) 
Installing websocket (1.0.7) 
Installing selenium-webdriver (2.31.0) 
Installing xpath (0.1.4) 
Installing capybara (1.1.2) 
Using coffee-script-source (1.6.1) 
Using execjs (1.4.0) 
Using coffee-script (2.2.0) 
Using rack-ssl (1.3.3) 
Using json (1.7.7) 
Using rdoc (3.12.2) 
Using thor (0.17.0) 
Using railties (3.2.12) 
Using coffee-rails (3.2.2) 
Installing diff-lcs (1.1.3) 
Using jquery-rails (2.2.1) 
Using rails (3.2.12) 
Installing rspec-core (2.11.1) 
Installing rspec-expectations (2.11.3) 
Installing rspec-mocks (2.11.3) 
Installing rspec (2.11.0) 
Installing rspec-rails (2.11.0) 
Using sass (3.2.7) 
Using sass-rails (3.2.6) 
Using sqlite3 (1.3.7) 
Using uglifier (1.3.0) 
Your bundle is updated! Use `bundle show [gemname]` to see where a bundled gem is installed.
```

Install RSpec

```console
$ rails generate rspec:install
      create  .rspec
      create  spec
      create  spec/spec_helper.rb
```

Create a static page

`public/hello.html`
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Greeting</title>
  </head>
  <body>
    <p>Hello, world!</p>
  </body>
</html>
```

Create a controller to handle static pages

```console
$ rails generate controller StaticPages home help --no-test-framework
      create  app/controllers/static_pages_controller.rb
       route  get "static_pages/help"
       route  get "static_pages/home"
      invoke  erb
      create    app/views/static_pages
      create    app/views/static_pages/home.html.erb
      create    app/views/static_pages/help.html.erb
      invoke  helper
      create    app/helpers/static_pages_helper.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/static_pages.js.coffee
      invoke    scss
       create      app/assets/stylesheets/static_pages.css.scss
```

Generate the failing tests

```console
$ rails generate integration_test static_pages
      invoke  rspec
      create    spec/requests/static_pages_spec.rb
```

Describe the test `spec/requests/static_pages_spec.rb`

```ruby
describe "Home page" do

  it "should have the content 'Sample App'" do
    visit '/static_pages/home'
    page.should have_content('Sample App')
  end
end
```

Run the test

```console
$ bundle exec rspec spec/requests/static_pages_spec.rb
Rack::File headers parameter replaces cache_control after Rack 1.5.
F

Failures:
     
  1) Static pages Home page should have the content 'Sample App'
     Failure/Error: page.should have_content('Sample App')
       expected there to be content "Sample App" in "RailsClass\n\nStaticPages#home\nFind me in app/views/static_pages/home.html.erb\n\n\n"
     # ./spec/requests/static_pages_spec.rb:9:in `block (3 levels) in <top (required)>'

Finished in 0.2724 seconds
1 example, 1 failure

Failed examples:

rspec ./spec/requests/static_pages_spec.rb:7 # Static pages Home page should have the content 'Sample App'

Randomized with seed 2144
```

To make the test pass edit `app/views/static_pages/home.html.erb`

```html
<h1>Sample App</h1>
<p>
  This is the home page for the
  <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
  sample application.
</p>
```

Run the test again

```console
$ bundle exec rspec spec/requests/static_pages_spec.rb
Rack::File headers parameter replaces cache_control after Rack 1.5.
.

Finished in 0.16103 seconds
1 example, 0 failures

Randomized with seed 29743
```

Add tests for the help page on `spec/requests/static_pages_spec.rb`

```ruby
require 'spec_helper'

describe "Static pages" do

  describe "Home page" do

    it "should have the content 'Sample App'" do
      visit '/static_pages/home'
      page.should have_content('Sample App')
    end
  end

  describe "Help page" do

    it "should have the content 'Help'" do
      visit '/static_pages/help'
      page.should have_content('Help')
    end
  end
end
```

Make it pass editing `app/views/static_pages/help.html.erb`

```html
<h1>Help</h1>
<p>
  Get help on the Ruby on Rails Tutorial at the
  <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
  To get help on this sample app, see the
  <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
</p>
```

Add tests from the About page on `spec/requests/static_pages_spec.rb`

```ruby
  describe "About page" do

    it "should have the content 'About Us'" do
      visit '/static_pages/about'
      page.should have_content('About Us')
    end
  end
```

Add the new route on `config/routes.rb` 

```ruby
get "static_pages/about"
```

Add an About handler on the controller: `app/controllers/static_pages_controller.rb`

```ruby
  def about
  end
```

Create a template for the About page: `app/views/static_pages/about.html.erb`

```html
<h1>About Us</h1>
<p>
  The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
  is a project to make a book and screencasts to teach web development
  with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
  is the sample application for the tutorial.
</p>
```

Run your tests


Add tests to validate the page titles on `spec/requests/static_pages_spec.rb`. It should be like:

```ruby
require 'spec_helper'

describe "Static pages" do

  describe "Home page" do

    it "should have the content 'Sample App'" do
      visit '/static_pages/home'
      page.should have_content('Sample App')
    end
	
    it "should have the right title 'Home'" do
      visit '/static_pages/home'
      page.should have_selector('title', :text => " | Home")
    end
  end
  
  describe "Help page" do
  
    it "should have the content 'Help'" do
      visit '/static_pages/help'
      page.should have_content('Help')
    end
	
    it "should have the right title 'Help'" do
      visit '/static_pages/home'
      page.should have_selector('title', :text => " | Help")
    end
  end
  
  describe "About page" do
  
    it "should have the content 'About Us'" do
      visit '/static_pages/about'
      page.should have_content('About Us')
    end
	
    it "should have the right title 'About Us'" do
      visit '/static_pages/home'
      page.should have_selector('title', :text => " | About Us")
    end
  end
  
end
```

Run your tests:

```console
$ bundle exec rspec spec/requests/static_pages_spec.rb
Rack::File headers parameter replaces cache_control after Rack 1.5.
F.F.F.

Failures:

  1) Static pages About page should have the right title 'About Us'
     Failure/Error: page.should have_selector('title', :text => " | About Us")
       expected css "title" with text " | About Us" to return something
     # ./spec/requests/static_pages_spec.rb:42:in `block (3 levels) in <top (required)>'

  2) Static pages Home page should have the right title 'Home'
     Failure/Error: page.should have_selector('title', :text => " | Home")
       expected css "title" with text " | Home" to return something
     # ./spec/requests/static_pages_spec.rb:14:in `block (3 levels) in <top (required)>'

  3) Static pages Help page should have the right title 'Help'
     Failure/Error: page.should have_selector('title', :text => " | Help")
       expected css "title" with text " | Help" to return something
     # ./spec/requests/static_pages_spec.rb:29:in `block (3 levels) in <top (required)>'

Finished in 2.14 seconds
6 examples, 3 failures

Failed examples:

rspec ./spec/requests/static_pages_spec.rb:40 # Static pages About page should have the right title 'About Us'
rspec ./spec/requests/static_pages_spec.rb:12 # Static pages Home page should have the right title 'Home'
rspec ./spec/requests/static_pages_spec.rb:27 # Static pages Help page should have the right title 'Help'

Randomized with seed 22673
```

Make the application layout use a dynamic title by editing `app/views/layouts/application.html.erb`

```html
<!DOCTYPE html>
<html>
<head>
  <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
  <%= stylesheet_link_tag    "application", :media => "all" %>
  <%= javascript_include_tag "application" %>
  <%= csrf_meta_tags %>
</head>
<body>

<%= yield %>

</body>
</html>
```

Provide Home title on `app/views/static_pages/home.html.erb` by adding this as first line:

```ruby
<% provide(:title, 'Home') %>
```

Provide Home title on `app/views/static_pages/help.html.erb` by adding this as first line:

```ruby
<% provide(:title, 'Help') %>
```

Provide Home title on `app/views/static_pages/about.html.erb` by adding this as first line:

```ruby
<% provide(:title, 'About') %>
```

Run your tests

```console
$ bundle exec rspec spec/requests/static_pages_spec.rb
Rack::File headers parameter replaces cache_control after Rack 1.5.
......

Finished in 2.09 seconds
6 examples, 0 failures

Randomized with seed 36738
```

Add tests for the contact page on `spec/requests/static_pages_spec.rb`

```ruby
  describe "Contact page" do

    it "should have the h1 'Contact'" do
      visit '/static_pages/contact'
      page.should have_selector('h1', :text => 'Contact')
    end

    it "should have the title 'Contact'" do
      visit '/static_pages/contact'
      page.should have_selector('title',
                        :text => " | Contact")
    end
  end
```

Create a contact page `app/views/static_pages/contact.html.erb`

```html
<% provide(:title, 'Contact') %>
<h1>Contact</h1>
<p>
  Contact Ruby on Rails Tutorial about the sample app at the
  <a href="http://railstutorial.org/contact">contact page</a>.
</p>
```

Add a route for the new page on `config/routes.rb` 

```ruby
get "static_pages/contact"
```

### Let's have automated tests


On `Gemfile` add:

```ruby
group :development, :test do
  gem 'sqlite3'
  gem 'rspec-rails', '2.11.0'
  gem 'guard-rspec', '1.2.1'
end

group :test do
  gem 'capybara', '1.1.2'
  gem 'minitest'
  
  # Test gems on Macintosh OS X
  #gem 'rb-fsevent', '0.9.1', :require => false
  #gem 'growl', '1.0.3'
  
  # Test gems on Linux
  #gem 'rb-inotify', '0.8.8'
  #gem 'libnotify', '0.5.9'
  
  # Test gems on Windows
  gem 'rb-fchange', '0.0.5'
  gem 'rb-notifu', '0.0.4'
  gem 'win32console', '1.3.0'
  
end
```
Update your bundle

```console
$ bundle install
Fetching gem metadata from https://rubygems.org/.........
Fetching gem metadata from https://rubygems.org/..
Using rake (10.0.3)
Using i18n (0.6.4)
Using multi_json (1.6.1)
Using activesupport (3.2.12)
Using builder (3.0.4)
Using activemodel (3.2.12)
Using erubis (2.7.0)
Using journey (1.0.4)
Using rack (1.4.5)
Using rack-cache (1.2)
Using rack-test (0.6.2)
Using hike (1.2.1)
Using tilt (1.3.5)
Using sprockets (2.2.2)
Using actionpack (3.2.12)
Using mime-types (1.21)
Using polyglot (0.3.3)
Using treetop (1.4.12)
Using mail (2.4.4)
Using actionmailer (3.2.12)
Using arel (3.0.2)
Using tzinfo (0.3.37)
Using activerecord (3.2.12)
Using activeresource (3.2.12)
Using bundler (1.2.3)
Using nokogiri (1.5.6)
Using ffi (1.4.0)
Using childprocess (0.3.9)
Using rubyzip (0.9.9)
Using websocket (1.0.7)
Using selenium-webdriver (2.31.0)
Using xpath (0.1.4)
Using capybara (1.1.2)
Installing coderay (1.0.9)
Using coffee-script-source (1.6.1)
Using execjs (1.4.0)
Using coffee-script (2.2.0)
Using rack-ssl (1.3.3)
Using json (1.7.7)
Using rdoc (3.12.2)
Using thor (0.17.0)
Using railties (3.2.12)
Using coffee-rails (3.2.2)
Using diff-lcs (1.1.3)
Installing listen (0.7.3)
Installing lumberjack (1.0.2)
Installing method_source (0.8.1)
Installing slop (3.4.4)
Installing pry (0.9.12)
Installing terminal-table (1.4.5)
Installing guard (1.6.2)
Installing guard-rspec (1.2.1)
Using jquery-rails (2.2.1)
Using minitest (4.6.2)
Using pg (0.14.1)
Using rails (3.2.12)
Installing rb-fchange (0.0.5)
Installing rb-notifu (0.0.4)
Using rspec-core (2.11.1)
Using rspec-expectations (2.11.3)
Using rspec-mocks (2.11.3)
Using rspec (2.11.0)
Using rspec-rails (2.11.0)
Using sass (3.2.7)
Using sass-rails (3.2.6)
Using sqlite3 (1.3.7)
Using uglifier (1.3.0)
Installing win32console (1.3.0) with native extensions

Your bundle is complete! Use `bundle show [gemname]` to see where a bundled gem is installed.
```
Create Guard files

```console
$ bundle exec guard init rspec
13:32:53 - INFO - Writing new Guardfile to /cygdrive/c/Users/Alexandre/dev/projects/rails-class/rails_class/Guardfile
13:32:53 - INFO - rspec guard added to Guardfile, feel free to edit it

```

Add our tests to `Guardfile` and make it stop on errors

```ruby
require 'active_support/core_ext'

guard 'rspec', :version => 2, :all_after_pass => false do
.
.
.
watch(%r{^app/controllers/(.+)_(controller)\.rb$})  { |m| ["spec/routing/#{m[1]}_routing_spec.rb", "spec/#{m[2]}s/#{m[1]}_#{m[2]}_spec.rb", "spec/acceptance/#{m[1]}_spec.rb", (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" :  "spec/requests/#{m[1].singularize}_pages_spec.rb")] }
.
.
.
# Capybara request specs
  watch(%r{^app/views/(.+)/.*\.(erb|haml)$})          { |m| (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" :  "spec/requests/#{m[1].singularize}_pages_spec.rb") }
  
.
.
.
end
```

The line

```ruby
guard 'rspec', :version => 2, :all_after_pass => false do
```

ensures that Guard doesn't run all the tests after a failing test

Make a new directory called `spec/routing`

```console
mkdir spec/routing
```

Now run guard and type `quit` to exit

```console
$ bundle exec guard
10:12:33 - INFO - Guard uses TerminalTitle to send notifications.
10:12:33 - INFO - Guard::RSpec is running, with RSpec 2!
10:12:33 - INFO - Running all specs
Rack::File headers parameter replaces cache_control after Rack 1.5.
........

Finished in 3.23 seconds
8 examples, 0 failures


Randomized with seed 5067

10:14:05 - INFO - Guard is now watching at '/cygdrive/c/Users/Alexandre/dev/projects/rails-class/rails_class'
[Listen warning]:
  Listen will be polling changes. Learn more at https://github.com/guard/listen#polling-fallback.

[1] guard(main)> quit
10:15:58 - INFO - Bye bye...
```