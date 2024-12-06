+++
title = "Using Test Kitchen"
linkTitle = "Using Test Kitchen"

[menu.kitchen]
title = "Using Test Kitchen"
identifier = "kitchen/using_test_kitchen"
parent = "kitchen"
weight = 11
+++


## Running Converge with Test Kitchen

The [Test Kitchen documentation](https://kitchen.ci/docs/getting-started/creating-cookbook/) describes the process for creating converge and verify tests. The Dokken driver documentation is in the [kitchen-dokken GitHub repository](https://github.com/chef/kitchen-dokken).

## Habitat-based changes

The Chef Infra Client 19 will be accessible using Habitat instead of the public Omnitruck APIs. Consequently, we've updated the provisioner to facilitate the installation of the Habitat-based Chef Infra Client, including passing through the license required from `kitchen.yml` file.
