+++
title = "Install Chef Infra Client using the migration tool in an online environment"

[menu.install]
title = "Online install"
identifier = "install/migration_tool/install_online"
parent = "install/migration_tool"
weight = 20
+++

This page documents how to install Chef Infra Client RC2 in an online environment.

## Supported platforms

Chef Infra Client 19 RC2 is supported on Linux x86-64 systems.

## Prerequisites

- a valid Chef License key

## Install Chef Infra Client

To install Chef Infra Client, follow these steps:

1. Optional: Verify that Chef Infra Client isn't already installed on your system:

    ```sh
    chef-client --version
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until August 26, 2025.

    Using curl:

    ```sh
    curl -o chef-migration-tool.v1.tar.gz https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424
    ```

    Using Wget:

    ```sh
    wget -O "chef-migration-tool.v1.tar.gz" https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424
    ```

1. Extract the migration tool and make it executable.

    ```sh
    tar -xvf chef-migration-tool.v1.tar.gz -C /path/to/temp/folder
    cd /path/to/temp/folder
    chmod +x chef-migrate-cli
    mv chef-migrate-cli /usr/local/bin/
    ```

1. Optional: Verify that the migration tool is installed.

    ```sh
    chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`chef-migrate apply`]({{< relref "reference" >}}):

    ```sh
    chef-migrate apply online --fresh-install --download-url "--download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-chef-infra-client-19.1.rc2.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682"" --license-key "<LICENSE_KEY>"

1. Verify that Chef Infra Client is installed.

    ```sh
    chef-client --version
    ```

## Next step

- [Add a Chef license]({{< relref "/license" >}})
