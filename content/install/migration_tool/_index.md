+++
title = "Install Chef Infra Client using the migration tool"
linkTitle = "Migration tool"

[menu.install]
title = "Overview"
parent = "install/migration_tool"
weight = 10
+++

The Chef Infra Client migration tool (`chef-migrate`) allows you to install or upgrade Chef Infra Client to the latest version in both online and air-gapped environments.

**Key functions:**

- **Fresh installation:** Install Chef Infra Client 19 RC3
- **Side-by-side installation:** Install Chef Infra Client 19 RC3 and remove or keep the previous Infra Client version. If you keep the previous version in side-by-side mode, the path to the most recent version takes precedence
- **Omnibus upgrade:** Upgrade from Omnibus-based Chef Infra Client 17.x or 18.x versions
- **Habitat upgrade:** Upgrade from Habitat-packaged Chef Infra Client 19 RC releases

**Supported platforms:**

- Linux x86-64
- Windows x86-64

To install or upgrade Chef Infra Client, see these guides:

- [Install](install)
- [Online upgrade](upgrade_online)
- [Air-gapped upgrade](upgrade_airgap)
- [`chef-migrate` CLI reference](reference)
