+++
title = "Install Chef Workstation tools"


[menu.workstation]
title = "Install Workstation tools"
identifier = "workstation/install/tools"
parent = "workstation/install"
weight = 30
+++

{{< readfile file="/content/reusable/md/workstation_modularize.md" >}}

## Install packages

Follow these instructions to install or upgrade each tool.

### Supported platforms

The Chef Workstation tools are supported on Linux x86-64 systems.

### Prerequisites

We use Chef Habitat to distribute and install these applications.
For more information, see the [Chef Habitat documentation](https://docs.chef.io/habitat/).

If you don't have Chef Habitat installed on your computer, follow these steps:

1. Download and install Chef Habitat:

    ```sh
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable
    ```

1. Verify Chef Habitat is installed.

    ```sh
    hab --version
    ```

### Berkshelf

To install Berkshelf, follow these steps:

1. Install the `chef/berkshelf` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/berkshelf --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    berks -v
    ```

### chef-cli

To install the chef-cli CLI, follow these steps:

1. Install the `chef/chef-cli` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/chef-cli --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    chef-cli -v
    ```

### Chef Infra Client

To install Chef Infra Client, see the [Chef Infra Client install documentation]({{< relref "/install" >}}) or follow these steps:

1. Install the `chef/chef-infra-client` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/chef-infra-client --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    chef-client -v
    ```

### Chef Test Kitchen Enterprise

To install Chef Test Kitchen Enterprise, see the [Test Kitchen Enterprise install documentation]({{< relref "workstation/kitchen/install" >}}) or follow these steps:

1. Install the `chef/chef-test-kitchen-enterprise` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/chef-test-kitchen-enterprise --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    chef-client -v
    ```

### Chef Vault

To install Chef Vault, follow these steps:

1. Install the `chef/chef-vault` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/chef-vault --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    chef-vault <args>
    ```

### Cookstyle

To install Cookstyle, follow these steps:

1. Install the `chef/cookstyle` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/cookstyle --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    cookstyle -v
    ```

### Fauxhai

To install Fauxhai, follow these steps:

1. Install the `chef/fauxhai` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/fauxhai --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    fauxhai -v
    ```

### Ohai

To install Ohai, follow these steps:

1. Install the `chef/ohai` package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install chef/ohai --channel unstable --binlink --force
    ```

1. Verify that the correct version runs:

    ```sh
    ohai -v
    ```
