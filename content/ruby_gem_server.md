+++
title = "Chef's Ruby gem server"

[menu.chef_gem_server]
title = "Chef's Ruby gem server"
+++

This page is going to be used for the context of our Customers.

# How to add a Gem Source

In order for customers to use the [https://rubygems.chef.io/](https://rubygems.chef.io/), they need:

- A valid license
  - you can obtain your license by visiting: [Add a Chef License Key](https://docs.chef.io/licensing/license_key/)
- Server that has ruby setup on it

To add commercial rubygems source from chef, they need to first add a valid license key into their gem source like this:

```sh
gem source --add https://v1:<license-key>@rubygems.chef.io
```

Expected output:

```sh
gem source --add https://v1:11111111-2222-3333-4444-55555555555@rubygems.chef.io
https://v1:11111111-2222-3333-4444-55555555555@rubygems.chef.io added to sources
```

Downloading a RubyGem

- Verify you have your gem source added
  - `gem source -a` - expected output:

```sh
*** CURRENT SOURCES ***

https://rubygems.org/
https://v1:11111111-2222-3333-4444-55555555555@rubygems.chef.io
```

- to install our gems now:

```sh
gem install chef-testing-ssimmons-simple-gem
Fetching chef-testing-ssimmons-simple-gem-0.1.4.gem
Successfully installed chef-testing-ssimmons-simple-gem-0.1.4
1 gem installed
```
