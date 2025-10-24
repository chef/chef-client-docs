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

1. Install Chef Infra Client using [`chef-migrate apply`](reference):

    ```sh
    sudo chef-migrate apply online --fresh-install --download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682" --license-key "<LICENSE_KEY>"
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify the Chef Infra Client installation.

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
    cd C:\migrate-tool
    Expand-Archive -Path "migration-tools-1.1.rc3-windows.zip" -DestinationPath "."
    ```

1. Optional: Verify that the migration tool works.

    ```powershell
    .\chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`chef-migrate apply`](reference):

    ```powershell
    .\chef-migrate apply online --fresh-install --download-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=a8SYQUWS%2FCEgDBNATtNi2gwb7XY%3D&Expires=1776916396" --license-key "<LICENSE_KEY>"
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify the Chef Infra Client installation.

    ```powershell
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
