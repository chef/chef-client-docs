+++
title = "Troubleshooting the Chef Infra Client migration tool"

[menu.install]
title = "Troubleshooting"
identifier = "install/migration_tool/troubleshooting"
parent = "install/migration_tool"
weight = 100
+++

This page documents troubleshooting steps for using the migration tool to install or upgrade Chef Infra Client RC2 on a node.

## error reading config file

The migration tool returns the following error when upgrading Chef Infra Client:

```plain
Failure while processing flag `process-config`, Error: error reading config file: failed to open file /etc/chef/client.rb: open /etc/chef/client.rb: no such file or directory.
```

To upgrade Chef Infra Client, the migration tool requires a [client.rb file](https://docs.chef.io/config_rb_client/) on the node. Create a [fresh install]({{< relref "/install/migration_tool/install.md" >}}) of Chef Infra Client instead.
