## Step 5 - Filling in the layout

Update `app/views/layouts/application.html.erb` to include more elaborate elements

```ruby
<!DOCTYPE html>
<html>
  <head>
    <title><%= full_title(yield(:title)) %></title>
    <%= stylesheet_link_tag    "application", media: "all" %>
    <%= javascript_include_tag "application" %>
    <%= csrf_meta_tags %>
    <!--[if lt IE 9]>
    <script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
    <![endif]-->
  </head>
  <body>
    <header class="navbar navbar-fixed-top navbar-inverse">
      <div class="navbar-inner">
        <div class="container">
          <%= link_to "sample app", '#', id: "logo" %>
          <nav>
            <ul class="nav pull-right">
              <li><%= link_to "Home",    '#' %></li>
              <li><%= link_to "Help",    '#' %></li>
              <li><%= link_to "Sign in", '#' %></li>
            </ul>
          </nav>
        </div>
      </div>
    </header>
    <div class="container">
      <%= yield %>
    </div>
  </body>
</html>
```

Now update `app/views/static_pages/home.html.erb` contents

```ruby
<div class="center hero-unit">
  <h1>Welcome to the Sample App</h1>

  <h2>
    This is the home page for the
    <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
    sample application.
  </h2>

  <%= link_to "Sign up now!", '#', class: "btn btn-large btn-primary" %>
</div>

<%= link_to image_tag("rails.png", alt: "Rails"), 'http://rubyonrails.org/' %>
```

Install [Bootstrap-saas gem](http://) on your `Gemfile`

```ruby
source 'https://rubygems.org'

gem 'rails', '3.2.13'
gem 'bootstrap-sass', '~> 2.3.2.0'
```
Install the bundle

```console
$ bundle install
Fetching gem metadata from https://rubygems.org/.........
Fetching gem metadata from https://rubygems.org/..
Installing rake (10.1.0) 
Using i18n (0.6.4) 
Installing multi_json (1.7.7) 
Using activesupport (3.2.12) 
Using builder (3.0.4) 
Using activemodel (3.2.12) 
Using erubis (2.7.0) 
Using journey (1.0.4) 
Using rack (1.4.5) 
Using rack-cache (1.2) 
Using rack-test (0.6.2) 
Installing hike (1.2.3) 
Installing tilt (1.4.1) 
Using sprockets (2.2.2) 
Using actionpack (3.2.12) 
Installing mime-types (1.23) 
Using polyglot (0.3.3) 
Installing treetop (1.4.14) 
Using mail (2.4.4) 
Using actionmailer (3.2.12) 
Using arel (3.0.2) 
Using tzinfo (0.3.37) 
Using activerecord (3.2.12) 
Using activeresource (3.2.12) 
Installing sass (3.2.9) 
Installing bootstrap-sass (2.3.2.0) 
Using bundler (1.2.3) 
Installing mini_portile (0.5.0)
Installing nokogiri (1.6.0) with native extensions 
Using ffi (1.9.0) 
Using childprocess (0.3.6) 
Using rubyzip (0.9.9) 
Using websocket (1.0.7) 
Installing selenium-webdriver (2.33.0) 
Using xpath (0.1.4) 
Using capybara (1.1.2) 
Using coderay (1.0.9) 
Installing coffee-script-source (1.6.2) 
Using execjs (1.4.0) 
Using coffee-script (2.2.0) 
Using rack-ssl (1.3.3) 
Installing json (1.8.0) with native extensions 
Using rdoc (3.12.2) 
Installing thor (0.18.1) 
Using railties (3.2.12) 
Using coffee-rails (3.2.2) 
Using diff-lcs (1.1.3) 
Installing formatador (0.2.4) 
Using growl (1.0.3) 
Using listen (0.7.3) 
Installing lumberjack (1.0.4) 
Using method_source (0.8.1) 
Installing slop (3.4.5) 
Installing pry (0.9.12.2) 
Installing guard (1.7.0) 
Using guard-rspec (1.2.1) 
Using spork (0.9.2) 
Using sys-proctable (0.9.3) 
Using guard-spork (1.2.0) 
Installing jquery-rails (3.0.1) 
Installing minitest (5.0.6) 
Using rails (3.2.12) 
Using rb-fsevent (0.9.1) 
Using rspec-core (2.11.1) 
Using rspec-expectations (2.11.3) 
Using rspec-mocks (2.11.3) 
Using rspec (2.11.0) 
Using rspec-rails (2.11.0) 
Using sass-rails (3.2.6) 
Using sqlite3 (1.3.7) 
Installing uglifier (2.1.1) 
Your bundle is updated! Use `bundle show [gemname]` to see where a bundled gem is installed.
```

Create a custom CSS file to your project as `app/assets/stylesheets/custom.css.scss` and import bootstrap on it

```css
@import "bootstrap";
```

Add some styling on the same file

```css
@import "bootstrap";

/* mixins, variables, etc. */

$grayMediumLight: #eaeaea;

/* universal */

html {
  overflow-y: scroll;
}

body {
  padding-top: 60px;
}

section {
  overflow: auto;
}

textarea {
  resize: vertical;
}

.center {
  text-align: center;
}

.center h1 {
  margin-bottom: 10px;
}

/* typography */

h1, h2, h3, h4, h5, h6 {
  line-height: 1;
}

h1 {
  font-size: 3em;
  letter-spacing: -2px;
  margin-bottom: 30px;
  text-align: center;
}

h2 {
  font-size: 1.7em;
  letter-spacing: -1px;
  margin-bottom: 30px;
  text-align: center;
  font-weight: normal;
  color: $grayLight;
}

p {
  font-size: 1.1em;
  line-height: 1.7em;
}

/* header */

#logo {
  float: left;
  margin-right: 10px;
  font-size: 1.7em;
  color: white;
  text-transform: uppercase;
  letter-spacing: -1px;
  padding-top: 9px;
  font-weight: bold;
  line-height: 1;
  &:hover {
    color: white;
    text-decoration: none;
  }
}

/* footer */

footer {
  margin-top: 45px;
  padding-top: 5px;
  border-top: 1px solid $grayMediumLight;
  color: $grayLight;
  a {
    color: $gray;
    &:hover { 
      color: $grayDarker;
    }
  }  
  small { 
    float: left; 
  }
  ul {
    float: right;
    list-style: none;
    li {
      float: left;
      margin-left: 10px;
    }
  }
}
```

Let's add some partials to clean-up the `app/views/layouts/application.html.erb` layout code

```ruby
<!DOCTYPE html>
<html>
  <head>
    <title><%= full_title(yield(:title)) %></title>
    <%= stylesheet_link_tag    "application", media: "all" %>
    <%= javascript_include_tag "application" %>
    <%= csrf_meta_tags %>
    <%= render 'layouts/shim' %>    
  </head>
  <body>
    <%= render 'layouts/header' %>
    <div class="container">
      <%= yield %>
    </div>
    <%= render 'layouts/footer' %>
  </body>
</html>
```

Create the shim partial as `app/views/layouts/_shim.html.erb`

```ruby
<!--[if lt IE 9]>
<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
```

Create the header partial as `app/views/layouts/_header.html.erb`

```ruby
<header class="navbar navbar-fixed-top navbar-inverse">
  <div class="navbar-inner">
    <div class="container">
      <%= link_to "sample app", '#', id: "logo" %>
      <nav>
        <ul class="nav pull-right">
          <li><%= link_to "Home",    '#' %></li>
          <li><%= link_to "Help",    '#' %></li>
          <li><%= link_to "Sign in", '#' %></li>
        </ul>
      </nav>
    </div>
  </div>
</header>
```

Create a footer partial as `app/views/layouts/_footer.html.erb`

```ruby
<footer class="footer">
  <small>
    <a href="http://railstutorial.org/">Rails Tutorial</a>
    by Michael Hartl
  </small>
  <nav>
    <ul>
      <li><%= link_to "About",   '#' %></li>
      <li><%= link_to "Contact", '#' %></li>
      <li><a href="http://news.railstutorial.org/">News</a></li>
    </ul>
  </nav>
</footer>
```

### Add a Contact page

Add tests for it on `spec/requests/static_pages_spec.rb`

```ruby
require 'spec_helper'

describe "Static pages" do
  .
  .
  .
  describe "Contact page" do

    it "should have the h1 'Contact'" do
      visit '/static_pages/contact'
      page.should have_selector('h1', text: 'Contact')
    end

    it "should have the title 'Contact'" do
      visit '/static_pages/contact'
      page.should have_selector('title',
                    text: "Ruby on Rails Tutorial Sample App | Contact")
    end
  end
end
```

### Styling links

Change links from

```ruby
<a href="/static_pages/about">About</a>
```
to

```ruby
<%= link_to "About", about_path %>
```

As is shown here:

|Page    | URI       | Named route  |
|--------|-----------|--------------|
|Home    |	/	     | root_path    |
|About   |	/about   | about_path   |
|Help    |	/help    | help_path    |
|Contact |	/contact | contact_path |
|Sign up |	/signup  | signup_path  |
|Sign in |	/signin  | signin_path  |

Update the RSpec tests on `spec/requests/static_pages_spec.rb`

```ruby
require 'spec_helper'

describe "Static pages" do
  
    describe "Home page" do
  
      it "should have the h1 'Sample App'" do
        visit root_path
        page.should have_selector('h1', text: 'Sample App')
      end
  
      it "should have the base title" do
        visit root_path
        page.should have_selector('title', text: "Ruby on Rails Tutorial Sample App")
      end
  
      it "should not have a custom page title" do
        visit root_path
        page.should_not have_selector('title', text: '| Home')
      end
    end
  
  describe "Help page" do
  
    it "should have the content 'Help'" do
      visit help_path
      page.should have_content('Help')
    end
	
    it "should have the right title 'Help'" do
      visit help_path
      page.should have_selector('title', text: " | Help")
    end
  end
  
  describe "About page" do
  
    it "should have the content 'About Us'" do
      visit about_path
      page.should have_content('About Us')
    end
	
    it "should have the right title 'About Us'" do
      visit about_path
      page.should have_selector('title', text: " | About Us")
    end
  end
  
  describe "Contact page" do

    it "should have the h1 'Contact'" do
      visit contact_path
      page.should have_selector('h1', text: 'Contact')
    end

    it "should have the title 'Contact'" do
      visit contact_path
      page.should have_selector('title', text: " | Contact")
    end 
  end
  
end
```

Update the routes map on ``

```ruby
RailsClass::Application.routes.draw do
  root to: 'static_pages#home'
  
  match '/signup',  to: 'users#new'
  match '/signin',  to: 'users#new'
  match '/signout',  to: 'users#new'
  
  match '/help',    to: 'static_pages#help'
  match '/about',   to: 'static_pages#about'
  match '/contact', to: 'static_pages#contact'
  
  .
  .
  .
end
```

### Pretify RSpec


Simplify the RSpec file `spec/support/static_pages_spec.rb`

```ruby
 require 'spec_helper'

describe "Static pages" do
	subject { page }

   describe "Home page" do
      before { visit root_path }
  
      it { should have_selector('h1', text: 'Sample App') }
      it { should have_selector('title', text: full_title('')) }
    end
  
  describe "Help page" do
	before { visit help_path }
	
    it { should have_selector('h1', text: 'Help') }
    it { should have_selector('title', text: full_title('Help')) }
  end
  
  describe "About page" do
	before { visit about_path }
  
    it { should have_selector('h1', text: 'About Us') }
    it { should have_selector('title', text: full_title('About Us')) }
  end
  
  describe "Contact page" do
	before { visit contact_path }
	
    it { should have_selector('h1', text: 'Contact') }
    it { should have_selector('title', text: full_title('Contact')) }
  end
end
```

Create a RSpec help on `spec/support/utilities.rb`

```ruby
def full_title(page_title)
  base_title = "Ruby on Rails Tutorial Sample App"
  if page_title.empty?
    base_title
  else
    "#{base_title} | #{page_title}"
  end
end
```

### User Signup

Generate a Users Controller

```console
$ rails generate controller Users new --no-test-framework
      create  app/controllers/users_controller.rb
       route  get "users/new"
      invoke  erb
      create    app/views/users
      create    app/views/users/new.html.erb
      invoke  helper
      create    app/helpers/users_helper.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/users.js.coffee
      invoke    scss
      create      app/assets/stylesheets/users.css.scss
```

Create User tests

```console
$ rails generate integration_test user_pages
      invoke  rspec
      create    spec/requests/user_pages_spec.rb
```

Update the tests on `spec/requests/user_pages_spec.rb`

```ruby
require 'spec_helper'

describe "User pages" do

  subject { page }

  describe "signup page" do
    before { visit signup_path }

    it { should have_selector('h1',    text: 'Sign up') }
    it { should have_selector('title', text: full_title('Sign up')) }
  end
end
```

Change the signup button on `app/views/static_pages/home.html.erb` from

```ruby
<%= link_to "Sign up now!", '#, class: "btn btn-large btn-primary" %>
```

to

```ruby
<%= link_to "Sign up now!", signup_path, class: "btn btn-large btn-primary" %>
```

