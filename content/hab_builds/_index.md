+++
title = "Hab-based builds"
linkTitle = "Hab-based builds"

[menu.hab]
title = "Overview"
identifier = "hab/overview"
parent = "hab"
weight = 10
+++

**Habitat-based Build and Delivery System:** The migration of Chef 19 to Habitat reduces dependencies on specific operating systems, enabling support for new platforms and systems more efficiently. The flexibility of this architecture also allows organizations to scale operations across diverse infrastructures effectively.

For RC1, the Habitat package for Infra Client 19 has been exported to tar. The tar is available off-the-shelf using the location specified in the download instructions or you can generate it on-demand using the instructions in the following section.

## How do I generate the tar if I need to?

To generate the tar, follow these steps:

1. Install Habitat. Follow the instructions at the following page to do this: [Get Chef Habitat](https://docs.chef.io/habitat/install_habitat/). Alternatively, use the following command to install Habitat:

    ```curl
    curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash -s -- -c stable -v 1.6.652
    ```

1. When Habitat is installed, run through the Habitat setup by running the following command:

    ```sh
    hab setup
    ```

1. Create a tar using the following command:

    ```sh
    hab pkg export tar chef/chef-infra-client --auth <auth-token>
    ```

## How to install Chef Infra Client RC1

You can use the migration tool to install Chef Infra Client 19 RC1 as a fresh install. You can also use the migration tool to install Chef Infra client 19 RC1 when migrating from older Omnibus builds of Chef Infra Client.

Refer to the migration tool documentation for instructions on how to install Infra Client using the migration tool.
