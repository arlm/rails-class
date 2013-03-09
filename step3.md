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

