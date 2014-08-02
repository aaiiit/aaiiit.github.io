---
layout: post
title:  "Rails 4 engines test"
date:   2014-06-23
categories: rails dev engines test
---

Testing is broken out of the box!
This is how you fix it :


test/test_helper.rb

{% highlight ruby %}
# Configure Rails Environment
ENV["RAILS_ENV"] = "test"

require File.expand_path("../dummy/config/environment.rb",  __FILE__)
require "rails/test_help"

Rails.backtrace_cleaner.remove_silencers!

# Load support files
Dir["#{File.dirname(__FILE__)}/support/**/*.rb"].each { |f| require f }

# Load fixtures from the engine
ActiveSupport::TestCase.fixture_path = File.expand_path("../fixtures", __FILE__)

class ActiveSupport::TestCase
  fixtures :all
end

#fixes other problems with controller tests (url helpers)
class ActionController::TestCase
  setup do
    @routes = Users::Engine.routes
  end
end
{% endhighlight %}

