[![Gem Version](https://badge.fury.io/rb/kitchen-rackspace.png)](http://badge.fury.io/rb/kitchen-rackspace)
[![Build Status](https://travis-ci.org/test-kitchen/kitchen-rackspace.png?branch=master)](https://travis-ci.org/test-kitchen/kitchen-rackspace)
[![Code Climate](https://codeclimate.com/github/test-kitchen/kitchen-rackspace.png)](https://codeclimate.com/github/test-kitchen/kitchen-rackspace)
[![Coverage Status](https://coveralls.io/repos/test-kitchen/kitchen-rackspace/badge.png)](https://coveralls.io/r/test-kitchen/kitchen-rackspace)
[![Dependency Status](https://gemnasium.com/test-kitchen/kitchen-rackspace.png)](https://gemnasium.com/test-kitchen/kitchen-rackspace)

# Kitchen::Rackspace

A Rackspace Cloud Servers driver for Test Kitchen!

Shamelessly copied from [Fletcher Nichol](https://github.com/fnichol)'s
awesome work on an [EC2 driver](https://github.com/opscode/kitchen-ec2).

## Installation

Add this line to your application's Gemfile:

    gem 'kitchen-rackspace'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install kitchen-rackspace

## Usage

Provide, at a minimum, the required driver options in your `.kitchen.yml` file:

    driver:
      name: rackspace
      rackspace_username: [YOUR RACKSPACE CLOUD USERNAME]
      rackspace_api_key: [YOUR RACKSPACE CLOUD API KEY]
      require_chef_omnibus: [e.g. 'true' or a version number if you need Chef]
    platforms:
      - name: [A PLATFORM NAME, e.g. 'centos-6']

By default, the driver will spawn a 1GB Performance server on the base image
for your specified platform. Additional, optional overrides can be provided:

    image_id: [SERVER IMAGE ID]
    flavor_id: [SERVER FLAVOR ID]
    server_name: [A FRIENDLY SERVER NAME]
    public_key_path: [PATH TO YOUR PUBLIC SSH KEY]
    rackspace_region: [A VALID RACKSPACE DC/REGION]
    wait_for: [NUM OF SECONDS TO WAIT BEFORE TIMING OUT, DEFAULT 600]
    no_ssh_tcp_check: [DEFAULTS TO false, SKIPS TCP CHECK WHEN true]
    no_ssh_tcp_check_sleep: [NUM OF SECONDS TO SLEEP IF no_ssh_tcp_check IS SET]
    networks: [LIST OF RACKSPACE NETWORK UUIDS, DEFAULT PUBLICNET AND SERVICE NET]
    rackconnect_wait: ['true' IF USING RACKCONNECT TO WAIT FOR IT TO COMPLETE]
    servicenet: ['true' IF USING THE SERVICENET IP ADDRESS TO CONNECT]

You also have the option of providing some configs via environment variables:

    export RACKSPACE_USERNAME="user"   # (or OS_USERNAME)
    export RACKSPACE_API_KEY="api_key" # (or OS_PASSWORD)

Some configs are also derived based on your .ssh directory, specifically the
`public_key_path` setting is derived by searching for:
- `~/.ssh/id_rsa.pub`
- `~/.ssh/id_dsa.pub`
- `~/.ssh/identity.pub`
- `~/.ssh/id_ecdsa.pub`

## Contributing

1. Fork it
2. `bundle install`
3. Create your feature branch (`git checkout -b my-new-feature`)
4. `bundle exec rake` must pass
5. Commit your changes (`git commit -am 'Add some feature'`)
6. Push to the branch (`git push origin my-new-feature`)
7. Create new Pull Request
