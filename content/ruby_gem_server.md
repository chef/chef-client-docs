+++
title = "Chef's Ruby gem server"
draft = true

[menu.chef_gem_server]
title = "Chef's Ruby gem server"
+++

Chef's Ruby gem server distributes Chef's commercial and licensed Ruby gems. The server is hosted at <https://rubygems.chef.io/>.

## Add Chef's gem server as a source

Before you begin, you will need your valid [Progress Chef license key](https://docs.chef.io/licensing/license_key/).

- Add Chef's Ruby gem server using `gem source --add`:

  ```sh
  gem sources --add https://v1:<LICENSE_KEY>@rubygems.chef.io
  ```

  It returns a message that `rubygems.chef.io` has been added as a gem source.

## Install a Ruby gem

1. Optional: Verify that you've added Chef's Ruby gem server as a source:

    ```sh
    gem sources -l
    ```

    This returns a list of Ruby gem servers that should include `rubygems.chef.io`:

    ```sh
    *** CURRENT SOURCES ***

    https://rubygems.org/
    https://v1:<LICENSE_KEY>@rubygems.chef.io
    ```

1. Install a gem:

    ```sh
    gem install <GEM>
    ```

    This installs the gem and displays a success message.

    For testing purposes, you can try installing `chef-test` or 'inspec-test' gem to verify that you can install from Chef's gem server:

    ```sh
    gem install chef-test-0.1.0.gem
    ```
