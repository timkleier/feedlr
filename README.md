# Feedlr

A Ruby interface to Feedly's [API](http://developer.feedly.com/).

## Installation

Add this line to your application's Gemfile:

    gem 'feedlr'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install feedlr

## Usage

### Baisc usage

```ruby
require 'feedlr'
client = Feedlr::Client.new(oauth_access_token: 'oauth access token')
# Fetch user categories
p client.user_categories
# Fetch user subscriptions
p client.user_subscriptions
```

### Detailed API

You can easily inspect the available client methods:

```ruby
require 'feedlr'
client = Feedlr::Client.new
p client.methods.sort - Object.methods
```

Also, the gem is fairly documented. Browse the YARD [documentaion](http://rubydoc.info/gems/feedlr/) for more information.

### Global configuration

You can have a global configuration that instances can use. For example,  you can have the following in some initializer's code:

```ruby
Feedlr.configure do |config|
  config.oauth_access_token = 'oauth access token'
  config.sandbox = true
  config.logger = SomeCustomLogger.new
end
```
And elsewhere you can do:
```ruby
client = Feedlr::Client.new
```

### Instance initialization

You can set the oauth access token, a custom logger(if needed) and whether or not to use the client on sandbox(develpment) mode:

```ruby
require 'feedlr'
require 'logger'
client = Feedlr::Client.new(
  oauth_access_token: 'oauth access token',
  sandbox: true,
  logger: Logger.new(STDOUT)
)
```

### Rate limiting

The client deals with a variaty of [errors](http://rubydoc.info/gems/feedlr/Error). The errors have a corresponding [rate_limit]((http://rubydoc.info/gems/feedlr/RateLimit)) object that maps to the returned rate limiting [headers](http://developer.feedly.com/v3/#rate-limiting) if any.


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request