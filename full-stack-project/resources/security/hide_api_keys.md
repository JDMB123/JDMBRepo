# How to hide your API key

If you're using Google Maps or any other API that requires an API key, you need to be careful not to push that API key to GitHub. There are crawlers that search through GitHub for API keys.

Fortunately, Rails 5.2+ makes it really easy to use API keys on Heroku without pushing them to GitHub. Note, however, that if you use your API keys in the frontend, they will still be exposed. They're just less likely to be picked up by crawlers.

# Master key

As of Rails 5.2, every Rails project automatically comes with a `master.key` file in `/config/`. This file contains a randomly generated master key that is used to encrypt and decrypt your API keys. The `master.key` file is automatically gitignored and it should never be pushed to GitHub. Because this file is gitignored, it also won't be pushed to Heroku when we `git push heroku master`.

To tell Heroku about your master key, run:

```bash
heroku config:set RAILS_MASTER_KEY=<your-master-key-here>
```

where `<your-master-key-here>` should be replaced with the contents of the `master.key` file.

Note that you must store your master key somewhere so that you can pick up your project from a new computer if you have to. For example, you can email the file to yourself. Then, to continue working on your project on a new computer, simply clone your project from GitHub and paste the `master.key` file into `/config/`.

# Encrypting API keys

Now that Heroku knows what your master key is, you can add your API key (for example your Google Maps key) to an encrypted `credentials.yml` file which will be what you push to GitHub and Heroku. To edit this file, run `bundle exec rails credentials:edit`. This will open a `yml` file. To add a Google API key, add the following:

```yml
google:
  api_key: 123456
```

 For `yml` files, white space matters, so be careful to exactly match this syntax. After making the edits, save and close the file and Rails will take care of encrypting it.

 # Using API keys

 Now that we've stored our Google API key, it is accessible like this:

 ```ruby
Rails.application.credentials.google[:api_key]
 ```

That means that in an `html.erb` file, we can access the key like this:

```html
<h1>My secret key: <%= Rails.application.credentials.google[:api_key] %></h1>
```

To use the API key in React, we can put it on the window. In your `application.html.erb`, put this:

```html
<script type="text/javascript">
  window.googleAPIKey = "<%= Rails.application.credentials.google[:api_key] %>"
</script>
```

Then in your React app, use the key like this:

```javascript
{window.googleAPIKey}
```