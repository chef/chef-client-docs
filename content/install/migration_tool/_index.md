+++
title = "Install Chef Infra Client using the migration tool"
linkTitle = "Migration tool"

[menu.install]
title = "Overview"
parent = "install/migration_tool"
weight = 10
+++

The Chef Infra Client migration tool (`chef-migrate`) allows you to install or upgrade Chef Infra Client to the latest version in both online and air-gapped environments.

It has the following functions:

- Install Chef Infra Client 19 RC3.
- Install Chef Infra Client 19 RC3 and remove or keep the previous Infra Client version installed in side-by-side mode, with the path to the most recent version taking precedence.
- Upgrade from Omnibus-based Chef Infra Client 17.x or 18.x versions.
- Upgrade from Habitat-packaged Chef Infra Client 19 RC1.

To install or upgrade Chef Infra Client, see these guides:

- [Install](install)
- [Online upgrade](upgrade_online)
- [Air-gapped upgrade](upgrade_airgap)
- [`chef-migrate` CLI reference](reference)
