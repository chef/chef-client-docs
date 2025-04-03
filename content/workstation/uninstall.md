+++
title = "Uninstall Chef Workstation and its tools"

[menu.workstation]
title = "Uninstall"
identifier = "workstation/uninstall"
parent = "workstation"
weight = 1000
+++

The page documents how to uninstall Chef Workstation and its component tools.

## Uninstall Chef Workstation

To uninstall Chef Workstation, use the [`hab pkg uninstall`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-uninstall) command:

- ```sh
  sudo hab pkg uninstall chef/chef-workstation
  ```

## Uninstall Chef Workstation packages

To uninstall a Workstation tool, use the [`hab pkg uninstall`](https://docs.chef.io/habitat/habitat_cli/#hab-pkg-uninstall) command:

- ```sh
  sudo hab pkg uninstall <PACKAGE>
  ```

  Replace `<PACKAGE>` with one of the following packages:

  - `chef/berkshelf`
  - `chef/chef-cli`
  - `chef/chef-infra-client`
  - `chef/chef-test-kitchen-enterprise`
  - `chef/chef-vault`
  - `chef/cookstyle`
  - `chef/fauxhai`
  - `chef/ohai`
