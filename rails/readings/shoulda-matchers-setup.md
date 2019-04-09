## Setting up Shoulda-Matchers

First, make sure that your Gemfile includes the `shoulda-matchers` gem:

```rb
group :test do
  gem 'shoulda-matchers'
  gem 'rspec-rails'
end
```

Next, we need to specify some configuration options in the `rails_helper.rb` file. We want to configure shoulda-matchers to use rspec as the testing framework, and to use the rails library (ActiveRecord, ActiveModel, and ActionController):

```rb
Shoulda::Matchers.configure do |config|
    config.integrate do |with|
      with.test_framework :rspec
      with.library :rails
    end
  end
```

You'll also need to `require 'shoulda-matchers'` at the top of your `rails_helper.rb` file.

Check out the [shoulda-matchers docs][shoulda-matchers-docs] for more details. 

[shoulda-matchers-docs]:https://github.com/thoughtbot/shoulda-matchers#rspec
