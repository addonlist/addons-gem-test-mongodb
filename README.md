# Launchbox gem test w/ MongoDB

* `rails g new-project -0` to create a rails project without ActiveRecord

## Integrating with Launchbox is Simple

* add `gem 'addons', '~> 0.0.6'` to your Gemfile
* `bundle install` installs addons
* `rails generator launchbox:install`
* `bundle install` installs figaro
* SIGN UP FOR ADDONS LAUNCHBOX
* set `ENV['ADDONS_APP_ID']` and `ENV['ADDONS_APP_TOKEN']` environment variables
* `rails console` or `rails server` will have set all environment variables and create a config/application.yml
* HEROKU USERS ONLY: `rake figaro:heroku` will set all your heroku environment variables
* Add code to integrate with your services. All environment variables for those services are securely populated by the Launchbox gem

### MongoLab Integration #1

* add `gem 'mongoid'` to Gemfile
* `bundle install`
* add production configuration to `config/mongoid.yml`

````ruby
production:
  sessions:
    default:
      uri: <%= ENV['MONGOLAB_URI'] %>
      options:
        consistency: :strong
        max_retries: 30
        retry_interval: 1
        timeout: 30
````

### Mailgun Integration

```ruby
def send_simple_message(email)
  RestClient.post "https://api:#{ENV['MAILGUN_API_KEY']}"\
  "@api.mailgun.net/v2/sandbox28428.mailgun.org/messages",
  :from => email.from,
  :to => email.to,
  :subject => email.subject,
  :text => email.body
end
````
