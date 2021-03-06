# Netsoul-Ruby [![Gem Version](https://badge.fury.io/rb/netsoul.svg)](http://badge.fury.io/rb/netsoul) [![Build Status](https://travis-ci.org/fenicks/netsoul-ruby.svg?branch=master)](https://travis-ci.org/fenicks/netsoul-ruby) [![Coverage Status](https://coveralls.io/repos/fenicks/netsoul-ruby/badge.svg?branch=master&service=github)](https://coveralls.io/github/fenicks/netsoul-ruby?branch=master)

* formerly __libnetsoul-rb__

This gem is a simple and efficient Netsoul client implementation written in Ruby.
You can use it as a Ruby gem in order to implement your own Netsoul client or just use the provided Netsoul client.

*__[History]__: 8 years after writing my first ruby lines of code, I decide to rewrite this old own with all my Ruby backgrounds. The old design was really bad.*

## Features

* __MD5__ authentication
* __Kerberos__ (my own Ruby native extension) authentication. Something is wrong with kerberos server or gssapi __[work in progress]__
* Data transfert is supported **only for the library part, not the provided client**, use it at your own. _My academic account was closed when I tryed files transfert at school_.
* Identification Netsoul client is provided
* Netsoul message library: all netsoul DSL is covered by the 'netsoul/message' module

## Installation

### On your desktop

```ruby
gem install netsoul
```

### In your project

#### Gemfile

```ruby
gem 'netsoul', '~> 2.3.5'
```

#### project.rb

```ruby
require 'netsoul'
```

## Use the client

After installing the gem **netsoul**, call the client as described bellow.

Define at least two environment variables : `NETSOUL_LOGIN` and `NETSOUL_SOCKS_PASSWORD` (see the config for the complete list: [https://github.com/fenicks/netsoul-ruby]()).

```bash
netsoul-ruby
```

or with a config file

```bash
netsoul-ruby -config netsoul-config.yml
```

### Example of _netsoul-config.yml_ file

#### Standard (MD5) authentication

```yaml
:login: 'kakesa_c'
:socks_password: 'my socks password'
# :unix_password: 'unix password needed for kerberos authentication' # :auth_method must be set to :krb5
# :auth_method: :std # :std, :krb5
# :server_host: 'ns-server.epita.fr'
# :server_port: 4242
# :state: :none # :actif, :away, :connection, :idle, :lock, :server, :none
# :location: 'Home'
# :user_group: 'ETNA_2008'
```

#### Kerberos authentication

```yaml
:login: 'kakesa_c'
:unix_password: 'unix password'
:auth_method: :krb5 # :std, :krb5
# :socks_password: 'my socks password'
# :server_host: 'ns-server.epita.fr'
# :server_port: 4242
# :state: :none # :actif, :away, :connection, :idle, :lock, :server, :none
# :location: 'Home'
# :user_group: 'ETNA_2008'
```

## Build your own Netsoul client with netsoul-ruby gem

Look at the client implementation in this gem: [https://github.com/fenicks/netsoul-ruby/blob/master/bin/netsoul-ruby]().
This client is implemented in less than 80 lines of code ; including option parser, client reconnection, ...

```ruby
# Install the gem first (Gemfile or 'gem install'), see the 'Installation' section
require 'netsoul/client'

c = Netsoul::Client.new options[:user_opts_hash]
c.connect
# ...
if c.started
  # ...
  c.send str
  # ...
  msg = c.get
  #...
end
# ...
c.disconnect
```

## Contributing

1. Fork it ( https://github.com/fenicks/netsoul-ruby/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
