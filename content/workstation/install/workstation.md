+++
title = "Install Chef Workstation"

[menu.workstation]
title = "Install Workstation"
identifier = "workstation/install/workstation"
parent = "workstation/install"
weight = 20

+++

This document describes how to install Chef Workstation and all its components.

## Supported platforms

Chef Workstation 26 RC3 is supported on Linux x86-64 systems.

## Install

To install Chef Workstation, follow these steps:

1. If Chef Habitat isn't already installed on you system, download and install Chef Habitat.

    For more information, see the [Chef Habitat install documentation](https://docs.chef.io/habitat/install_habitat/).

    ```sh
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable
    ```

1. Verify Chef Habitat is installed.

    ```sh
    hab --version
    ```

1. Install the Chef Workstation Habitat package:

    ```sh
    sudo hab pkg install --binlink --force chef/chef-workstation --channel unstable
    ```

1. Optional: Verify that Chef Workstation and its tools are installed:

    ```sh
    chef-workstation -v
    ```

    Chef Workstation returns a list of installed packages and their versions.
