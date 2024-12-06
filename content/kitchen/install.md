+++
title = "Install Test Kitchen Enterprise"

[menu.kitchen]
title = "Install Test Kitchen Enterprise"
identifier = "kitchen/install"
parent = "kitchen"
weight = 20
+++

To install the new Chef Test Kitchen Enterprise, first ensure you have the latest Chef Habitat installer.

## Supported platforms

Chef Test Kitchen Enterprise RC1 is supported on Linux x86-64 systems.

## Install Chef Habitat

Chef Test Kitchen Enterprise is installed as a Habitat package using Chef Habitat.
Install and set up Chef Habitat if it's not already installed on your system.

{{< note >}}

For more information, see the [Chef Habitat install documentation](https://docs.chef.io/habitat/install_habitat/).

{{< /note >}}

1. Download and install Chef Habitat:

    ```sh
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable -v 1.6.652
    ```

1. Verify Chef Habitat is installed.

    ```sh
    hab --version
    ```

    Chef Habitat returns the installed version.

1. Set up Chef Habitat:

    ```sh
    hab cli setup
    ```

    Follow the prompts in the Habitat CLI.
    We recommend the following settings for running Test Kitchen Enterprise:

    - Connect to an on-premises Builder instance? [yes/No/quit] **No**
    - Set up a default origin? [Yes/no/quit] **No**
    - Set up a default Builder personal access token? [yes/No/quit] **No**
    - Set up a default Habitat Supervisor control gateway secret? [yes/No/quit] **No**

## Install Chef Test Kitchen Enterprise

1. Use Chef Habitat to install the Chef Test Kitchen Enterprise package:

    ```sh
    sudo hab pkg install --binlink --force chef/chef-test-kitchen-enterprise --channel unstable
    ```

    Chef Habitat downloads and installs Chef Test Kitchen Enterprise, it's components, and the `chef-cli` and `kitchen` CLI tools.

1. Verify these tools are installed:

    ```sh
    chef-cli --version
    kitchen --version
    ```

    You can also verify that the Test Kitchen Enterprise package is installed in `/hab/pkgs/chef/chef-test-kitchen-enterprise/1.0.5`.
