## Step 1 - Setup the environment

Install [ruby](http://www.ruby-lang.org/en/downloads/) and verify its version

```console
$ ruby -v
ruby 1.9.3p385 (2013-02-06 revision 39114)
```

Install [rails](http://rubyonrails.org/download) and verify its version

```console
$ rails -v
Rails 3.2.12
```

Create your application on the directory

```console
$ rails new rails_class
      create  
      create  README.rdoc
      create  Rakefile
      create  config.ru
      create  .gitignore
      create  Gemfile
      create  app
      create  app/assets/images/rails.png
      create  app/assets/javascripts/application.js
      create  app/assets/stylesheets/application.css
      create  app/controllers/application_controller.rb
      create  app/helpers/application_helper.rb
      create  app/views/layouts/application.html.erb
      create  app/mailers/.gitkeep
      create  app/models/.gitkeep
      create  config
      create  config/routes.rb
      create  config/application.rb
      create  config/environment.rb
      create  config/environments
      create  config/environments/development.rb
      create  config/environments/production.rb
      create  config/environments/test.rb
      create  config/initializers
      create  config/initializers/backtrace_silencers.rb
      create  config/initializers/inflections.rb
      create  config/initializers/mime_types.rb
      create  config/initializers/secret_token.rb
      create  config/initializers/session_store.rb
      create  config/initializers/wrap_parameters.rb
      create  config/locales
      create  config/locales/en.yml
      create  config/boot.rb
      create  config/database.yml
      create  db
      create  db/seeds.rb
      create  doc
      create  doc/README_FOR_APP
      create  lib
      create  lib/tasks
      create  lib/tasks/.gitkeep
      create  lib/assets
      create  lib/assets/.gitkeep
      create  log
      create  log/.gitkeep
      create  public
      create  public/404.html
      create  public/422.html
      create  public/500.html
      create  public/favicon.ico
      create  public/index.html
      create  public/robots.txt
      create  script
      create  script/rails
      create  test/fixtures
      create  test/fixtures/.gitkeep
      create  test/functional
      create  test/functional/.gitkeep
      create  test/integration
      create  test/integration/.gitkeep
      create  test/unit
      create  test/unit/.gitkeep
      create  test/performance/browsing_test.rb
      create  test/test_helper.rb
      create  tmp/cache
      create  tmp/cache/assets
      create  vendor/assets/javascripts
      create  vendor/assets/javascripts/.gitkeep
      create  vendor/assets/stylesheets
      create  vendor/assets/stylesheets/.gitkeep
      create  vendor/plugins
      create  vendor/plugins/.gitkeep
         run  bundle install
Enter your password to install the bundled RubyGems to your system: 
Fetching gem metadata from https://rubygems.org/...........
Fetching gem metadata from https://rubygems.org/..
Using rake (10.0.3) 
Installing i18n (0.6.4) 
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
Installing tilt (1.3.4) 
Using sprockets (2.2.2) 
Using actionpack (3.2.12) 
Using mime-types (1.21) 
Using polyglot (0.3.3) 
Using treetop (1.4.12) 
Using mail (2.4.4) 
Using actionmailer (3.2.12) 
Using arel (3.0.2) 
Installing tzinfo (0.3.36) 
Using activerecord (3.2.12) 
Using activeresource (3.2.12) 
Using bundler (1.2.3) 
Installing coffee-script-source (1.6.1)
Using execjs (1.4.0) 
Using coffee-script (2.2.0) 
Using rack-ssl (1.3.3) 
Using json (1.7.7) 
Using rdoc (3.12.2) 
Using thor (0.17.0) 
Using railties (3.2.12) 
Using coffee-rails (3.2.2) 
Using jquery-rails (2.2.1) 
Using rails (3.2.12) 
Installing sass (3.2.7) 
Using sass-rails (3.2.6) 
Using sqlite3 (1.3.7) 
Using uglifier (1.3.0) 
Your bundle is complete! Use `bundle show [gemname]` to see where a bundled gem is installed.
```
On `Gemfile`, change

We’ve also changed

```ruby
gem 'sqlite3'
```

to

```ruby
group :development do
  gem 'sqlite3'
end

group :production do
  gem 'pg'
end
```

and run the bundler again

```console
$ bundle update
Fetching gem metadata from https://rubygems.org/...........
Fetching gem metadata from https://rubygems.org/..
Enter your password to install the bundled RubyGems to your system: 
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
Using coffee-script-source (1.6.1) 
Using execjs (1.4.0) 
Using coffee-script (2.2.0) 
Using rack-ssl (1.3.3) 
Using json (1.7.7) 
Using rdoc (3.12.2) 
Using thor (0.17.0) 
Using railties (3.2.12) 
Using coffee-rails (3.2.2) 
Using jquery-rails (2.2.1) 
Using rails (3.2.12) 
Using sass (3.2.7) 
Using sass-rails (3.2.6) 
Using sqlite3 (1.3.7) 
Using uglifier (1.3.0) 
Your bundle is updated! Use `bundle show [gemname]` to see where a bundled gem is installed.
```

Run your application on the rails server

```console
$ rails server
=> Booting WEBrick
=> Rails application starting on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2013-03-09 00:35:21] INFO  WEBrick 1.3.1
[2013-03-09 00:35:21] INFO  ruby 1.9.3 (2013-02-06) [x86_64-darwin12.2.1]
[2013-03-09 00:35:21] INFO  WEBrick::HTTPServer#start: pid=11197 port=3000
```