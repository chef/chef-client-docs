+++
title = "Chef Infra Client RC2 release notes"

[menu.release_notes]
title = "Release notes"
+++

## Chef Workstation

### chef CLI

The `chef` command is deprecated. Use the `chef-cli` command to execute all commands that ran with the `chef` command.

For example, replace:

```sh
chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

with:

```sh
chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

For the RC2 release, the `chef report` command isn't available.

For information on available commands, see the [`chef` CLI documentation](https://docs.chef.io/workstation/ctl_chef/).

### chef-workstation CLI

This release introduces the new `chef-workstation` CLI. This release only supports the `--version` (`-v`) option.

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