+++
title = "Upgrade Chef Infra Client to version 19 RC3 using the migration tool in an online environment"

[menu.install]
title = "Online upgrade"
identifier = "install/migration_tool/upgrade_online"
parent = "install/migration_tool"
weight = 20
+++

This page documents how to upgrade Chef Infra Client to version 19 RC3 in an online environment.

## Supported platforms

Chef Infra Client 19 RC3 is supported on:

- Linux x86-64
- Windows x86-64

## Prerequisites

- a valid Chef License key

## Upgrade Chef Infra Client 19 RC2 on Linux

To upgrade Chef Infra Client, follow these steps:

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

1. Install Chef Infra Client using [`chef-migrate apply`](reference).

    ```sh
    sudo chef-migrate apply online --download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-chef-infra-client-19.1.rc2.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682" --license-key "<LICENSE_KEY>"
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify that Chef Infra Client is installed.

    ```sh
    chef-client --version
    ```

## Upgrade Chef Infra Client 19 RC2 on Windows

To upgrade Chef Infra Client, follow these steps:

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a ZIP file using a pre-signed address from an S3 bucket until August 26, 2025.

    Using curl:

    ```powershell
    curl -o chef-migration-tool.v1.zip "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/Windows/migration-tools_Windows_x86_64.zip?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=i5K3bQIqD35chzrTtS2uerU7ZDE%3D&Expires=1768953772"
    ```

    Using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/Windows/migration-tools_Windows_x86_64.zip?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=i5K3bQIqD35chzrTtS2uerU7ZDE%3D&Expires=1768953772" -OutFile "chef-migration-tool.v1.zip"
    ```

1. Extract the migration tool.

    ```powershell
    mkdir C:\migrate-tool
    move "chef-migration-tool.v1.zip" "C:\migrate-tool\"
    cd C:\migrate-tool
    Expand-Archive -Path "chef-migration-tool.v1.zip" -DestinationPath "."
    ```

1. Optional: Verify that the migration tool works.

    ```powershell
    .\chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Upgrade Chef Infra Client using [`chef-migrate apply`]({{< relref "reference" >}}).

    ```powershell
    .\chef-migrate apply online --download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/Windows/chef-chef-infra-client-19.1.rc2.windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=VCLjoJMbgSC%2Fkos4P%2BR2Ikm0Jww%3D&Expires=1767840014" --license-key "<LICENSE_KEY>"
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify the Chef Infra Client upgrade.

    ```powershell
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
