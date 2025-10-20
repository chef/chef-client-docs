+++
title = "Chef Workstation 26 RC3"
linkTitle = "Chef Workstation"

[menu.workstation]
title = "Overview"
identifier = "workstation/overview"
parent = "workstation"
weight = 10
+++

Start automating your infrastructure with Chef Workstation. It provides everything you need to get started with Chef, including ad hoc remote execution, remote scanning, configuration tasks, cookbook creation tools, and robust dependency and testing software---all in one easy-to-install package.

## Chef Workstation components

{{< readfile file="/content/reusable/md/workstation_modularize.md" >}}

Chef Workstation includes the following tools:

- Berkshelf
- `chef-cli` CLI
- Chef Infra Client 19
- Chef Test Kitchen Enterprise
- Chef Vault
- Cookstyle
- Fauxhai
- Ohai

These tools come bundled with Chef Workstation, however you can install and manage them separately.
To install and manage Chef Workstation and it's components, see the [Workstation install documentation](/workstation/install/workstation) and the [Workstation component install documentation](/workstation/install/tools).

{{< note >}}

We aren't including the Knife and InSpec applications in Chef Workstation for the RC3 release.

{{< /note >}}

### chef-workstation CLI

This release introduces the new `chef-workstation` CLI, which has the `--version` (`-v`) option.

```sh
chef-workstation -v
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

### Berkshelf

Berkshelf is a dependency manager for Chef cookbooks. With it, you can depend on community cookbooks and include them in your workflow. You can also ensure that your CI systems reproducibly select the same cookbook versions, and can upload and bundle cookbook dependencies without needing a locally maintained copy. Berkshelf is included in Chef Workstation.

For more information, see the [Berkshelf documentation](https://docs.chef.io/workstation/berkshelf/).

### chef-cli CLI

The `chef-cli` CLI replaces the `chef` CLI, which is deprecated with this release.
You can use the `chef-cli` command to execute all commands that were executed with the `chef` command.

For example, replace:

```sh
chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

with:

```sh
chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

The following commands are unavailable in this release:

- `chef-cli capture`
- `chef-cli report`
- `chef-cli supermarket`

Additionally, the `chef {-v|--version}` command is replaced by `chef-workstation {-v|--version}`.

For command syntax and usage, see the [`chef` reference documentation](https://docs.chef.io/workstation/ctl_chef/).

### Chef Infra Client

See the [Chef Infra Client documentation](/).

### Chef Test Kitchen Enterprise

Use Chef Test Kitchen Enterprise to automatically test cookbooks across any combination of platforms and test suites.

For more information, see the [Test Kitchen Enterprise documentation](kitchen).

### Chef Vault

Chef Vault lets you encrypt a data bag item using asymmetric keys. When you provide Chef Vault with a list of public keys from your nodes, only the nodes with public keys entered on this list can decrypt the data bag item contents. Chef Vault is included in Chef Workstation and Chef Infra Client by way of the chef-vault Ruby Gem. chef-vault uses the knife vault subcommand.

For more information, see the [Chef Vault documentation](https://docs.chef.io/workstation/chef_vault/).

### Cookstyle

Cookstyle is a code linting tool that helps you write better Chef Infra cookbooks by detecting and automatically correcting style, syntax, and logic mistakes in your code.

For more information, see the [Cookstyle documentation](https://docs.chef.io/workstation/cookstyle/).

### Fauxhai

Fauxhai allows you to mock out Ohai data in your Chef testing.

For more information, see the [Fauxhai repository](https://github.com/chef/fauxhai).

### Ohai

Ohai is a tool for collecting system configuration data, which it then provides to Chef Infra Client to use in cookbooks.

For more information, see the [Ohai documentation](https://docs.chef.io/ohai/).
