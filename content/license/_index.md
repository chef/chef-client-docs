+++
title = "Apply a license in Chef Infra Client"
linkTitle = "Apply a license"

[menu.licensing]
title = "Apply a license"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

This document outlines the licensing requirements and enforcement policies for Chef Infra Client.

Depending on the distribution you download and install, you may have to add a license key to run Chef Infra Client.
You must also [accept the Chef End User License Agreement (Chef EULA)](#accept-the-end-user-license-agreement) when you first run Chef Infra Client.

## Licensing requirements

Chef Infra Client has different licensing requirements depending on the distribution you download.

### License required

License key requirements are enforced:

- At the point of download for the binaries from Progress Chef Download Portal or through Habitat package distribution.
- At first run when using runtime installations and workflows, if the binaries are from the Chef API.
- For Chef software from any other sources not listed above, such as public Ruby gems or channels outside of the official Habitat distribution and download portal.

### No license key requirement

Chef Infra Client doesn't require a license key to:

- Use runtime installations and workflows when using your own source to download binaries.
- Execute any non-download commands using software obtained from an official source.

## Add a license

Chef Infra Client has three ways to set a license:

- An environment variable
- A command line option
- The command line interactive dialog

After setting a license key, Chef Infra Client validates it with Progress Chef's licensing service.

### Environment variable

- You can set the license key by setting the `CHEF_LICENSE_KEY` environment variable:

  ```sh
  export CHEF_LICENSE_KEY=<LICENSE_KEY>
  ```

### Command line option

- You can set the license key using the `--chef-license-key` CLI option:

  ```sh
  chef-client --chef-license-key=<LICENSE_KEY>
  ```

### Interactive license dialog

If you run a `chef-client` command and a license key isn't already set, Chef Infra Client starts an interactive licensing dialog.

To set a license key with the CLI interactive dialog, follow these steps:

1. Verify the version of Chef Infra Client you have installed:

    ```sh
    chef-client --version
    ```

    It should return version 19.0.54 or greater for Infra Client RC 1.

1. Run `chef-client` in local mode and `why-run` mode:

    ```sh
    chef-client --local-mode --why-run
    ```

    Local mode runs Chef Infra Client on your local machine as if it were running against Chef Infra Server.
    `why-run` mode shows you what Chef Infra Client would configure during a Chef Infra Client run.

1. At the first prompt, select **I already have a license ID**.

    ```text
    Please choose one of the options below (Press ↑/↓ arrow to move and Enter to select)
    ‣ I already have a license ID
      I don't have a license ID and would like to generate a new license ID
      Skip
    ```

1. Enter your license key at the second prompt.

    ```text
    Please enter your license ID:  <LICENSE_KEY>
    ✔ [Success] License validated successfully.
    ```

    After entering the license key, Chef Infra Client verifies your license and the run completes.

## Accept the End User License Agreement

When you first run Chef Infra Client, you must accept the End User License Agreement (EULA).

Chef Infra Client accepts a license using a command line option, environment variable, or config file.

### Options

Chef Infra Client accepts the following license acceptance options:

`accept`
: Accept the license and attempts to persist a marker file locally. Persisting these marker files means future invocations don't require accepting the license again.

`accept-silent`
: Similar to `accept`, but no messaging is sent to STDOUT.

`accept-no-persist`
: Similar to `accept-silent`, but no marker file is persisted. Future invocations will require accepting the license again.

### Command line option

To accept the Chef License, run `chef-client` with the `--chef-license` option:

```sh
chef-client --chef-license <LICENSE_OPTION>
```

### Environment variable

To accept the Chef License, set the `CHEF_LICENSE` environment variable:

```sh
export CHEF_LICENSE="<LICENSE_OPTION>"
chef-client OPTION VALUE
```

### Config file

You can accept the Chef License in the Chef Infra Client or Knife config files.

On a workstation, set this in the [`~/.chef/config.rb` or `~/.chef/knife.rb` files](https://docs.chef.io/workstation/config_rb/).
On a node, set this in the [`/etc/chef/client.rb`]({{< relref "/install/config_rb_client" >}}) file.

```ruby
chef_license "<LICENSE_OPTION>"
```
