+++
title = "Chef Client Migration Tool"
linkTitle = "Chef Client Migration Tool"

[menu.migrate]
title = "Chef Client Migration Tool"
identifier = "migrate/overview"
parent = "migrate"
weight = 10
+++

The Chef Client Migration Tool provides a flexible capability to install (or upgrade to) the latest Chef Infra Client from previous versions. The installation of the migration tool for RC1, in addition to the command line options available are detailed in the following section.  The `chef-migrate` command-line tool supports:

- New installation of Chef Infra 19 Client (chef-client)
- Installation of the Chef Infra 19 RC1 Client, either removing the previous version or leaving the previous client installed (side-by-side mode, with the path to the most recent version taking precedence)
- Upgrading from the 17.x and 18.x versions of the Chef Infra Client (also referred to as "Omnibus distributions")
- Upgrading to Chef Infra 19 RC1 Client and subsequent versions (also referred to as "Habitat-packaged")
- (During the release candidate time frame) automatically downloading from the new distribution point and checking prerequisites for the client
- Performing the download of the latest client and installing in a non-internet-accessible ("airgap") environment
- Enabling automated workflows to perform these same use cases and scenarios
