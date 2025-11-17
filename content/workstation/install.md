+++
title = "Install Chef Workstation and its components"
linkTitle = "Install"

[menu.workstation]
title = "Install"
identifier = "workstation/install"
parent = "workstation"
weight = 20
+++

{{< readfile file="/content/reusable/md/workstation_modularize.md" >}}

## Supported platforms

Chef Workstation 26 RC3 and its components are supported on Linux x86-64 systems.

## Prerequisites

We use Chef Habitat to distribute and install Chef Workstation and its components.
If you haven't already, you must download and install Chef Habitat.
For more information, see the [Chef Habitat documentation](https://docs.chef.io/habitat/).

1. Download and install Chef Habitat:

    ```sh
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable
    ```

1. Verify Chef Habitat is installed.

    ```sh
    hab --version
    ```

## Install Chef Workstation

To install Chef Workstation, follow these steps:

1. Install the Chef Workstation Habitat package:

    ```sh
    sudo hab pkg install --binlink --force chef/chef-workstation --channel unstable
    ```

1. Optional: Verify that Chef Workstation and its tools are installed:

    ```sh
    chef-workstation -v
    ```

    Chef Workstation returns a list of installed packages and their versions.

## Install Chef Workstation tools

Follow these instructions to install a Workstation tool.

1. Install a package using [`hab pkg install`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-install):

    ```sh
    sudo hab pkg install <PACKAGE_IDENT> --channel unstable --binlink --force
    ```

    Replace `<PACKAGE_IDENT>` with the package identifier:

    - `chef/berkshelf`
    - `chef/chef-cli`
    - `chef/chef-infra-client`
    - `chef/chef-test-kitchen-enterprise`
    - `chef/chef-vault`
    - `chef/cookstyle`
    - `chef/fauxhai`
    - `chef/ohai`

    The `--binlink --force` options overwrite any existing package symbolic links in the system's PATH directory with the new version so you can run it directly in the command line.

1. Verify that the correct version runs:

    ```sh
    berks -v
    chef-cli -v
    chef-client -v
    chef-client -v
    chef-vault <args>
    cookstyle -v
    fauxhai -v
    ohai -v
    ```
