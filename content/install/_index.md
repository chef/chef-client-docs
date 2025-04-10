+++
title = "Install Chef Infra Client"
linkTitle = "Install"

[menu.install]
title = "Overview"
parent = "install"
weight = 10
+++

Use either a native installer or the Chef Infra Client migration tool to install or upgrade Chef Infra Client.

## Native installers

The [Chef Infra Client native installers]({{< relref "installer" >}}) provide an efficient way to install the Chef Infra Client on both Debian and RPM-based distributions.
Users can download and install the pre-built `.deb` or `.rpm` packages using their existing package management tools, simplifying the deployment process for managing system configurations.

## Migration tool

The [Chef Infra Client migration tool]({{< relref "migration_tool" >}}) (`chef-migrate`) allows you to install or upgrade of the Chef Infra Client to the latest version in both online and airgapped environments.

It has the following functions:

- Install Chef Infra Client 19 RC2.
- Install Chef Infra Client 19 RC2 and remove or keep the previous Infra Client version installed. If the previous version is kept in side-by-side mode, the path to the most recent version takes precedence.
- Upgrade from Omnibus-based Chef Infra Client 17.x or 18.x versions.
- Upgrade from Habitat-packaged Chef Infra Client 19 RC1.
