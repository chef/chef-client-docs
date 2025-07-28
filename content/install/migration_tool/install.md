+++
title = "Install Chef Infra Client using the migration tool in an online environment"

[menu.install]
title = "Online install"
identifier = "install/migration_tool/install_online"
parent = "install/migration_tool"
weight = 20
+++

This page documents how to install Chef Infra Client RC3 in an online environment.

## Supported platforms

Chef Infra Client 19 RC3 is supported on:

- Linux x86-64
- Windows x86-64

## Prerequisites

- a valid Chef License key

## Install Chef Infra Client on Linux

To install Chef Infra Client on Linux, follow these steps:

1. Optional: Verify that Chef Infra Client isn't already installed on your system:

    ```sh
    chef-client --version
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until August 26, 2025.

    Using curl:

    ```sh
    curl -o chef-migration-tool.v1.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424"
    ```

    Using Wget:

    ```sh
    wget -O "chef-migration-tool.v1.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424"
    ```

1. Extract the migration tool and make it executable.

    ```sh
    tar -xvf chef-migration-tool.v1.tar.gz -C /path/to/temp/folder
    cd /path/to/temp/folder
    chmod +x chef-migrate
    mv chef-migrate /usr/local/bin/
    ```

1. Optional: Verify that the migration tool is installed.

    ```sh
    chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`chef-migrate apply`](reference):

    ```sh
    sudo chef-migrate apply online --fresh-install --download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-chef-infra-client-19.1.rc2.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682" --license-key "<LICENSE_KEY>"

1. Verify that Chef Infra Client is installed.

    ```sh
    chef-client --version
    ```

## Install Chef Infra Client on Windows

To install Chef Infra Client on Windows, follow these steps:

1. Optional: Verify that Chef Infra Client isn't already installed on your system:

    ```powershell
    chef-client --version
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until August 26, 2025.

    Using curl:

    ```powershell
    curl -o chef-migration-tool.v1.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424"
    ```

    Using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424" -OutFile "chef-migration-tool.v1.tar.gz"
    ```

1. Extract the migration tool and make it executable.

    ```powershell
    mkdir C:\migrate-tool
    copy "chef-migration-tool.v1.tar.gz" "C:\migrate-tool\"
    cd C:\migrate-tool
    tar -xf chef-migration-tool.v1.tar.gz
    ```

1. Optional: Verify that the migration tool is installed.

    ```powershell
    .\chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`chef-migrate apply`]({{< relref "reference" >}}):

    ```powershell
    .\chef-migrate apply online --fresh-install --download-url "<WIN_TAR_PACKAGE_URL>"
    ```

1. Verify that Chef Infra Client is installed.

    ```powershell
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
