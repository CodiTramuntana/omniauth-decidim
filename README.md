# OmniAuth::Decidim

This is the [Decidim](https://github.com/decidim/decim) strategy for OmniAuth. It should be used when using a Decidim application as an OAuth provider.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'omniauth-decidim', git: 'https://github.com/decidim/omniauth-decidim'
```

And then execute:

    $ bundle

## Usage

First you need to [create an OAuth application](https://github.com/decidim/decidim/blob/master/docs/customization/oauth.md) at your Decidim installation in order to get the Client ID, Client Secret and Site parameters.

Next, tell OmniAuth about this strategy. In a Decidim application using Devise you would create a file like `config/initializers/omniauth_decidim.rb` with this code:

```ruby
Devise.setup do |config|
  config.omniauth :decidim,
                  ENV["DECIDIM_CLIENT_ID"],
                  ENV["DECIDIM_CLIENT_SECRET"],
                  ENV["DECIDIM_SITE_URL"],
                  scope: :public
end

Decidim::User.omniauth_providers << :decidim
```

You should set the environment variables with the values you got from your Decidim installation.

## Authentication Hash

An example auth hash available in `request.env['omniauth.auth']`:

```ruby
{
  :provider => "decidim",
  :uid => "123456",
  :info => {
    :nickname => "foobar",
    :name => "Foo Bar",
    :email => "foo@bar.com",
    :image => "http://www.example.org/avatar.jpeg",
  },
  :credentials => {
    :token => "a1b2c3d4...", # The OAuth 2.0 access token
    :secret => "abcdef1234"
  }
}
```

## Following our license

If you plan to release your application you'll need to publish it using the same license: GPL Affero 3. We recommend doing that on GitHub before publishing, you can read more on "[Being Open Source From Day One is Especially Important for Government Projects](http://producingoss.com/en/governments-and-open-source.html#starting-open-for-govs)". If you have any trouble you can contact us on [Gitter](https://gitter.im/decidim/decidim).
