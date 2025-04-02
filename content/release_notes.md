+++
title = "Chef Infra Client RC2 release notes"

[menu.release_notes]
title = "Release notes"
+++

## Chef Workstation

### Workstation tools

To improve the user experience and simplify interactions with its components, we've modularized Chef Workstation. This restructuring divides Chef Workstation into independent components, allowing users to install, upgrade, and manage specific parts individually using Chef Habitat. This modular design reduces the complexity of maintaining the entire package.

### Test Kitchen Enterprise

Test Kitchen Enterprise, initially available for testing during the Chef Infra Client 19 RC1 release, is now fully integrated into the Chef Workstation package. This integration ensures users can access the latest features and security updates without waiting for full workstation releases, improving productivity and minimizing downtime.

### chef and chef-cli CLIs

The `chef` CLI is deprecated and replaced by the `chef-cli` command. Use `chef-cli` to execute all commands that ran with the `chef` command.

For example, replace:

```sh
chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

with:

```sh
chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

{{< note >}}

For this release, the chef-cli `--help` option returns usage instructions for the chef CLI.

For example:

```sh
$ chef-cli generate --help

Usage: chef generate GENERATOR [options]
```

{{< /note >}}

#### Supported commands

For the RC2 release, the following commands aren't available:

- `chef-cli capture`
- `chef-cli report`
- `chef-cli supermarket`

In addition, the `chef {-v|--version}` is replaced by `chef-workstation {-v|--version}`.

For information on command syntax and usage, see the [`chef` CLI reference documentation](https://docs.chef.io/workstation/ctl_chef/).

### chef-workstation CLI

This release introduces the new `chef-workstation` CLI, which only supports the `--version` (`-v`) option.

```sh
$ chef-workstation -v

Product Name: Chef Workstation
Product Version: 0.1.4

Default Installed Components:

Chef Infra Client Version: 19.0.85
Chef CLI Version: 5.6.17
Chef Test Kitchen Enterprise Version: 1.0.14
Berkshelf Version: 8.0.17
Ohai Version: 19.0.7
Fauxhai Version: 9.3.22
Chef Vault Version: 4.1.15
Cookstyle Version: 7.32.13
```
