+++
title = "Install Chef Infra Client using the migration tool"
linkTitle = "Migration tool"
+++

The Chef Infra Client migration tool (`chef-migrate`) allows you to install or upgrade of the Chef Infra Client to the latest version in both online and airgappeed environments.

It has the following functions:

- Install Chef Infra Client 19 RC2.
- Install Chef Infra Client 19 RC2 and remove or keep the previous Infra Client version installed in side-by-side mode, with the path to the most recent version taking precedence.
- Upgrade from Omnibus Chef Infra Client 17.x or 18.x versions.
- Upgrade from Habitat-packaged Chef Infra Client 19 RC1.

To install or upgrade Chef Infra Client, see these guides:

- [Install airgapped]({{< relref "install_airgap" >}})
- [Install online]({{< relref "install_online" >}})
- [Upgrade airgapped]({{< relref "upgrade_airgap" >}})
- [Upgrade online]({{< relref "upgrade_online" >}})

And see the [`chef-migrate` CLI reference]({{< relref "reference" >}}).
