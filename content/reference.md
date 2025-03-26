+++
title = "Habitat command reference"

[menu.reference]
title = "Habitat reference"
+++

With Habitat-based Chef Infra Client builds, you can use the following common functions for troubleshooting.

## List the gems used with Habitat builds

```sh
sudo hab pkg exec chef/chef-infra-client gem list
```

## List all the gems used with Habitat builds

```sh
sudo hab pkg exec chef/chef-infra-client gem list --all
```

## Get the install path

```sh
sudo hab pkg exec chef/chef-infra-client gem env
```

## Get Ruby version

```sh
/hab/bin/hab pkg exec core/ruby3_1 ruby -v
```
