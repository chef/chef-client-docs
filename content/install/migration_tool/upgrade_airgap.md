+++
title = "Upgrade Chef Infra Client to version 19 RC3 using the migration tool in an air-gapped environment"

[menu.install]
title = "Air-gapped upgrade"
identifier = "install/migration_tool/upgrade_airgap"
parent = "install/migration_tool"
weight = 20
+++

This page documents how to upgrade Chef Infra Client to version 19 RC3 in an air-gapped environment.

## Supported platforms

Chef Infra Client 19 RC3 is supported on:

- Linux x86-64
- Windows x86-64

## Prerequisites

- a valid Chef License key

## Upgrade to Chef Infra Client 19 RC3 on Linux

To upgrade Chef Infra Client, follow these steps:

1. On an internet-connected machine, download the Chef Infra Client 19 RC3 tar file.

    Chef Infra Client is available in a zipped tar file using a pre-signed URL from an S3 bucket until April 23, 2026.

    Download using curl:

    ```sh
    curl -o chef-ice-19.2.rc3-windows.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682"
    ```

    Download using Wget:

    ```sh
    wget -O "chef-ice-19.2.rc3-windows.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682"
    ```

1. On an internet-connected machine, download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until April 23, 2026.

    Using curl:

    ```sh
    curl -o migration-tools-1.1.rc3-linux.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/linux/migration-tools-1.1.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=a5W9L7B1mn07h%2BFYQFBp0fhqbzo%3D&Expires=1776916415"
    ```

    Using Wget:

    ```sh
    wget -O "migration-tools-1.1.rc3-linux.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/linux/migration-tools-1.1.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=a5W9L7B1mn07h%2BFYQFBp0fhqbzo%3D&Expires=1776916415"
    ```

1. Extract the migration tool and make it executable.

    ```sh
    tar -xvf migration-tools-1.1.rc3-linux.tar.gz -C /path/to/temp/folder
    cd /path/to/temp/folder
    chmod +x chef-migrate
    mv chef-migrate /usr/local/bin/
    ```

1. Optional: Verify that the migration tool is installed.

    ```sh
    chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client by specifying the path to the tar file using [`chef-migrate apply`](reference).

    ```sh
    sudo chef-migrate apply airgap <PATH/TO/BUNDLE> --license-key "<LICENSE_KEY>"
    ```

    Replace:

    - `<PATH/TO/BUNDLE>` with the path to the Chef Infra Client tar file.
    - `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify that Chef Infra Client is installed.

    ```sh
    chef-client --version
    ```

## Upgrade to Chef Infra Client 19 RC3 on Windows

To upgrade Chef Infra Client, follow these steps:

1. On an internet-connected machine, download the Chef Infra Client 19 RC3 tar file.

    Chef Infra Client is available in a tar file using a pre-signed address from an S3 bucket until April 23, 2026.

    Download using curl:

    ```powershell
    curl -o chef-ice-19.2.rc3-windows.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=a8SYQUWS%2FCEgDBNATtNi2gwb7XY%3D&Expires=1776916396"
    ```

    Download using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=a8SYQUWS%2FCEgDBNATtNi2gwb7XY%3D&Expires=1776916396" -OutFile "chef-ice-19.2.rc3-windows.tar.gz"
    ```

1. On an internet-connected machine, download the Chef Infra Client migration tool.

    The migration tool is available for download as a ZIP file using a pre-signed address from an S3 bucket until April 23, 2026.

    Using curl:

    ```powershell
    curl -o migration-tools-1.1.rc3-windows.zip "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/windows/migration-tools-1.1.rc3-windows.zip?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=AbB2Lr%2BgpryRhtfkkFFXuYekNfM%3D&Expires=1776988102"
    ```

    Using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/windows/migration-tools-1.1.rc3-windows.zip?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=AbB2Lr%2BgpryRhtfkkFFXuYekNfM%3D&Expires=1776988102" -OutFile "migration-tools-1.1.rc3-windows.zip"
    ```

1. Extract the migration tool.

    ```powershell
    mkdir C:\migrate-tool
    move "migration-tools-1.1.rc3-windows.zip" "C:\migrate-tool\"
    move "chef-ice-19.2.rc3-windows.tar.gz" "C:\migrate-tool\"
    cd C:\migrate-tool
    Expand-Archive -Path "migration-tools-1.1.rc3-windows.zip" -DestinationPath "."
    ```

1. Optional: Verify that the migration tool works.

    ```powershell
    .\chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Upgrade Chef Infra Client by specifying the path to the tar file using [`chef-migrate apply`](reference).

    ```powershell
    .\chef-migrate apply airgap "C:\migrate-tool\chef-ice-19.2.rc3-windows.tar.gz" --license-key "<LICENSE_KEY>"
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify the Chef Infra Client upgrade.

    ```powershell
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
