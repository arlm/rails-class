## Step 4 - A little Ruby on Rails

Create an application helper on `app/helpers/application_helper.rb`

```ruby
module ApplicationHelper

  # Returns the full title on a per-page basis.
  def full_title(page_title)
    base_title = "Ruby on Rails Tutorial Sample App"
    if page_title.empty?
      base_title
    else
      "#{base_title} | #{page_title}"
    end
  end
end
```

Modify `app/views/layouts/application.html.erb` replacing

```ruby
<title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
```

with

```ruby
<title><%= full_title(yield(:title)) %></title>
```

And update RSpec tests on `spec/requests/static_pages_spec.rb`

```ruby
require 'spec_helper'

describe "Static pages" do

  describe "Home page" do

    it "should have the h1 'Sample App'" do
      visit '/static_pages/home'
      page.should have_selector('h1', :text => 'Sample App')
    end

    it "should have the base title" do
      visit '/static_pages/home'
      page.should have_selector('title',
                        :text => "Ruby on Rails Tutorial Sample App")
    end

    it "should not have a custom page title" do
      visit '/static_pages/home'
      page.should_not have_selector('title', :text => '| Home')
    end
  end
  .
  .
  .
end
```

Now remove the provide line on `app/views/static_pages/home.html.erb`