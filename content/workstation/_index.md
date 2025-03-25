+++
title = "Chef Workstation"

[menu.workstation]
title = "Overview"
identifier = "workstation/overview"
parent = "workstation"
weight = 10
+++

Start your infrastructure automation with Chef Workstation.
Workstation gives you everything you need to get started with Chef---ad hoc remote execution, remote scanning, configuration tasks, cookbook creation tools as well as robust dependency and testing software---all in one easy-to-install package.

We've rebranded Chef Workstation to Chef Workstation (Chef Workstation) and substantial changes have been made in installation and licensing.


## Chef Workstation tools

Chef Workstation includes the following components:

- Chef Test Kitchen Enterprise
- Chef Infra Client 19
- Cookstyle
- Berkshelf
- Chef Vault
- Ohai
- Fauxhai



We have introduce the new command chef-dke which for now only have version sub-command.

```sh
chef-dke -v Product Name: Chef Workstation Product Version: 0.1.4 Default Installed Components: Chef Infra Client Version: 19.0.85 Chef CLI Version: 5.6.17 Chef Test Kitchen Enterprise Version: 1.0.14 Berkshelf Version: 8.0.17 Ohai Version: 19.0.7 Fauxhai Version: 9.3.22 Chef Vault Version: 4.1.15 Cookstyle Version: 7.32.13
```

**Deprecated** **commands:**

`chef` command is deprecated, and you can use `chef-cli` command to execute all commands that were previously functional with `chef` command.

```sh
chef -v // no longer work
chef-dke -v // will work
chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options) // No longer work
chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options) // will work
```

For the RC2 release `chef report` command isn't available

## Apply a license in Chef Workstation

Execution of Chef Infra Client 19 and Chef Test Kitchen Enterprise requires a valid license.

How to apply license section can be linked here or can be copied from RC1 Docs [https://progresssoftware.atlassian.net/wiki/x/O4DZU](https://progresssoftware.atlassian.net/wiki/x/O4DZU)

## Install Chef Workstation tools

You can install the following Chef Workstation tools without installing Chef Workstation:

- Chef Command Line Tool `chef-cli`
- Chef Test Kitchen Enterprise (only kitchen dokken driver)
- Chef Infra Client
- Cookstyle
- Berkshelf
- Chef Vault
- Ohai
- Fauxhai

Users can install any of the components and use them effectively.
With chef-dke chef command is no longer supported and for now chef report is also not supported rest command can be used through chef-cli

**Installing Chef Command Line Tool**

```sh
sudo hab pkg install chef/chef-cli --channel unstable --binlink --force
```

To use

```sh
chef-cli -v
```

**Installing Chef Test Kitchen Enterprise**

```sh
sudo hab pkg install chef/chef-test-kitchen-enterprise --channel unstable --binlink --force
```

To use

```sh
kitchen -v
```

**Installing Chef Infra Client**

```sh
sudo hab pkg install chef/chef-infra-client --channel unstable --binlink --force
```

To use

```sh
chef-client -v
```

**Installing Cookstyle**

```sh
sudo hab pkg install chef/cookstyle --channel unstable --binlink --force
```

To use

```sh
cookstyle -v
```

**Installing Berkshelf**

```sh
sudo hab pkg install chef/berkshelf --channel unstable --binlink --force
```

To use

```sh
berks -v
```

**Installing Chef Vault**

```sh
sudo hab pkg install chef/chef-vault --channel unstable --binlink --force
```

To use

```sh
chef-vault <args>
```

**Installing Ohai**

```sh
sudo hab pkg install chef/ohai --channel unstable --binlink --force
```

To use

```sh
ohai -v
```

**Installing Fauxhai**

```sh
sudo hab pkg install chef/fauxhai --channel unstable --binlink --force
```

To use

```sh
fauxhai -v
```

### How to use the different versions of Chef Workstation components

If a user wishes to use alternative versions of Chef Workstation components beyond the default, they must first install the desired version of the component. Additionally, it's essential to set the environment variable to ensure proper execution.

Below is a comprehensive list of environment variables associated with the different components:

| **Name** | **Env variable name** |
| --- | --- |
| Chef Infra Client | `CHEF_INFRA_CLIENT_VERSION` |
| Berkshelf | `BERKSHELF_VERSION` |
| Chef CLI | `CHEF_CLI_VERSION` |
| Chef Vault | `CHEF_VAULT_VERSION` |
| Cookstyle | `COOKSTYLE_VERSION` |
| Fauxhai | `FAUXHAI_VERSION` |
| Ohai | `OHAI_VERSION` |
| Chef Test Kitchen Enterprise | `KITCHEN_VERSION` |
