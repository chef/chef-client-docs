+++
title = "Chef Workstation"

[menu.workstation]
title = "Overview"
identifier = "workstation/overview"
parent = "workstation"
weight = 10
+++

Start automating your infrastructure with Chef Workstation. It provides everything you need to get started with Chef, including ad hoc remote execution, remote scanning, configuration tasks, cookbook creation tools, and robust dependency and testing software—all in one easy-to-install package.

With this release, we've changed how Chef Workstation is installed and licensed.

## Supported platforms

Chef Workstation is supported on Linux x86-64 systems.

## Install Chef Workstation

To install Chef Workstation, follow these steps:

1. If Chef Habitat isn't already installed on you system, download and install Chef Habitat:

    ```sh
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable
    ```

   For more information, see the [Chef Habitat install documentation](https://docs.chef.io/habitat/install_habitat/).

1. Verify Chef Habitat is installed.

    ```sh
    hab --version
    ```

1. If you haven't already configured Habitat, set up the `hab` CLI:

    ```sh
    hab cli setup
    ```

    Follow the prompts in the Habitat CLI.
    We recommend the following settings:

    - Connect to an on-premises Builder instance? [yes/No/quit] **No**
    - Set up a default origin? [Yes/no/quit] **No**
    - Set up a default Builder personal access token? [yes/No/quit] **No**
    - Set up a default Habitat Supervisor control gateway secret? [yes/No/quit] **No**

1. Install the Chef Workstation Habitat package:

    ```sh
    sudo hab pkg install --binlink --force chef/chef-development-kit-enterprise --channel unstable
    ```

1. Optional: Verify that Chef Workstation and its tools are installed:

    Chef Workstation returns a list of installed packages and their versions.

## Chef Workstation tools

Chef Workstation includes the following tools:

- Berkshelf
- `chef-cli` CLI
- Chef Infra Client 19
- Chef Test Kitchen Enterprise
- Chef Vault
- Cookstyle
- Fauxhai
- Ohai

These tools come bundled with Chef Workstation, however you can install them separately using the `hab pkg install` command.

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

#### Install separately

Berkshelf is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/berkshelf` package:

    ```sh
    sudo hab pkg install chef/berkshelf --channel unstable --binlink --force
    ```

1. If you have more than one version of the Berkshelf package installed, define the version that should run:

    ```sh
    export BERKSHELF_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    berks -v
    ```

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

For information on available commands, see the [`chef` CLI documentation](https://docs.chef.io/workstation/ctl_chef/).

#### Install separately

The `chef-cli` CLI is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/chef-cli` package:

    ```sh
    sudo hab pkg install chef/chef-cli --channel unstable --binlink --force
    ```

1. If you have more than one version of the Ohai package installed, define the version that should run:

    ```sh
    export CHEF_CLI_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    chef-cli -v
    ```

### Chef Infra Client

#### Install separately

Chef Infra Client is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/chef-infra-client` package:

    ```sh
    sudo hab pkg install chef/chef-infra-client --channel unstable --binlink --force
    ```

1. If you have more than one version of the Chef Infra Client package installed, define the version that should run:

    ```sh
    export CHEF_INFRA_CLIENT_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    chef-client -v
    ```

### Chef Test Kitchen Enterprise

Use Chef Test Kitchen Enterprise to automatically test cookbooks across any combination of platforms and test suites.

For more information, see the [Test Kitchen Enterprise documentation]({{< relref "kitchen" >}}).

#### Install separately

Chef Test Kitchen Enterprise is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, see the [Test Kitchen Enterprise install documentation]({{< relref "workstation/kitchen/install" >}}).

### Chef Vault

Chef Vault lets you encrypt a data bag item using asymmetric keys. When you provide Chef Vault with a list of public keys from your nodes, only the nodes with public keys entered on this list can decrypt the data bag item contents. Chef Vault is included in Chef Workstation and Chef Infra Client by way of the chef-vault Ruby Gem. chef-vault uses the knife vault subcommand.

For more information, see the [Chef Vault documentation](https://docs.chef.io/workstation/chef_vault/).

#### Install separately

Chef Vault is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/chef-vault` package:

    ```sh
    sudo hab pkg install chef/chef-vault --channel unstable --binlink --force
    ```

1. If you have more than one version of the Chef Vault package installed, define the version that should run:

    ```sh
    export CHEF_VAULT_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    chef-vault <args>
    ```

### Cookstyle

Cookstyle is a code linting tool that helps you write better Chef Infra cookbooks by detecting and automatically correcting style, syntax, and logic mistakes in your code.

For more information, see the [Cookstyle documentation](https://docs.chef.io/workstation/cookstyle/).

#### Install separately

Cookstyle is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/cookstyle` package:

    ```sh
    sudo hab pkg install chef/cookstyle --channel unstable --binlink --force
    ```

1. If you have more than one version of the Cookstyle package installed, define the version that should run:

    ```sh
    export COOKSTYLE_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    cookstyle -v
    ```

### Fauxhai

Fauxhai allows you to mock out Ohai data in your Chef testing.

For more information, see the [Fauxhai repository](https://github.com/chef/fauxhai).

#### Install separately

Fauxhai is included as a component of Chef Workstation. However, you can install it as a standalone application or you can install a different version of from the one bundled with Workstation.

To install this application, follow these steps:

1. Install the `chef/fauxhai` package:

    ```sh
    sudo hab pkg install chef/fauxhai --channel unstable --binlink --force
    ```

1. If you have more than one version of the Fauxhai package installed, define the version that should run:

    ```sh
    export FAUXHAI_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    fauxhai -v
    ```

### Ohai

Ohai is a tool for collecting system configuration data, which it then provides to Chef Infra Client to use in cookbooks.

For more information, see the [Ohai documentation](https://docs.chef.io/ohai/).

#### Install separately

Ohai is included as a component of Chef Workstation, however you can install it separately with the `hab pkg install` command.

1. Install the `chef/ohai` package:

    ```sh
    sudo hab pkg install chef/ohai --channel unstable --binlink --force
    ```

1. If you have more than one version of the Ohai package installed, define the version that should run:

    ```sh
    export OHAI_VERSION="<VERSION>"
    ```

1. Verify that the correct version runs:

    ```sh
    ohai -v
    ```
