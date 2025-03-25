+++
title = "Install Chef Workstation"

[menu.workstation]
title = "Install"
identifier = "workstation/install"
parent = "workstation"
weight = 20
+++

## Platform Support

Chef Workstation RC2 is supported on Linux x86-64 systems.

## Prerequisites

Chef Workstation is a Chef Habitat package and Habitat must be installed to run it.

### Install Chef Habitat



Please follow the [instructions](https://docs.chef.io/habitat/install_habitat/ "https://docs.chef.io/habitat/install_habitat/") or use one of the following commands to install Habitat.

```sh
curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable -v 1.6.652
```

Note that the current directory should be writeable, and you may need to use `chmod 777 ./install.sh` to execute the installation script.

Verify the installed hab version

```sh
hab --version hab 1.6.652/20230206155653
```

## Install Chef Workstation

To install Chef Workstation Habitat package, run following command:

```sh
sudo hab pkg install --binlink --force chef/chef-development-kit-enterprise --channel unstable
```

Users will see the download of Chef Workstation and its components.

Verify the versions with:

```sh
chef-dke -v Product Name: Chef Workstation Product Version: 0.1.4 Default Installed Components: Chef Infra Client Version: 19.0.85 Chef CLI Version: 5.6.17 Chef Test Kitchen Enterprise Version: 1.0.14 Berkshelf Version: 8.0.17 Ohai Version: 19.0.7 Fauxhai Version: 9.3.22 Chef Vault Version: 4.1.15 Cookstyle Version: 7.32.13
```