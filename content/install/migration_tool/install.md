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

Chef Infra Client is supported on:

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

1. Download the Chef Infra Client migration tool (migrate-ice).

    Before downloading, have your Progress Chef License ID ready.

    First, get the latest version:

    ```sh
    curl "https://commercial-acceptance.downloads.chef.co/stable/migrate-ice/versions/latest?license_id=<LICENSE_ID>"
    ```

    Replace `<LICENSE_ID>` with your Progress Chef License ID.

    The response returns the latest version number. Use this version to download the migration tool package.

    Using curl:

    ```sh
    curl -o migration-tools-<VERSION>-linux.tar.gz "https://commercial-acceptance.downloads.chef.co/current/migrate-ice/packages?v=<VERSION>&license_id=<LICENSE_ID>"
    ```

    Using Wget:

    ```sh
    wget -O "migration-tools-<VERSION>-linux.tar.gz" "https://commercial-acceptance.downloads.chef.co/current/migrate-ice/packages?v=<VERSION>&license_id=<LICENSE_ID>"
    ```

    Replace:
    - `<VERSION>` with the version number from the previous step
    - `<LICENSE_ID>` with your Progress Chef License ID

1. Extract the migration tool and make it executable.

    ```sh
    tar -xvf migration-tools-<VERSION>-linux.tar.gz -C /path/to/temp/folder
    cd /path/to/temp/folder
    chmod +x migrate-ice
    mv migrate-ice /usr/local/bin/
    ```

1. Optional: Verify that the migration tool is installed.

    ```sh
    migrate-ice --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`migrate-ice apply`](reference):

    You can install Chef Infra Client using either the download URL or by specifying a version number.

    **Method 1: Using download URL**

    ```sh
    sudo migrate-ice apply online --fresh-install --download-url "<CHEF_TAR_DOWNLOAD_URL>"
    ```

    Replace `<CHEF_TAR_DOWNLOAD_URL>` with the Chef Infra Client package download URL.

    **Method 2: Using version number**

    ```sh
    sudo migrate-ice apply online --fresh-install --chef-version <VERSION> --license-key "<LICENSE_KEY>"
    ```

    Replace `<VERSION>` with the Chef Infra Client version number (for example, 19.1.150) and `<LICENSE_KEY>` with your Progress Chef License key.

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

1. Download the Chef Infra Client migration tool (migrate-ice).

    Before downloading, have your Progress Chef License ID ready.

    First, get the latest version:

    ```powershell
    curl "https://commercial-acceptance.downloads.chef.co/stable/migrate-ice/versions/latest?license_id=<LICENSE_ID>"
    ```

    Replace `<LICENSE_ID>` with your Progress Chef License ID.

    The response returns the latest version number. Use this version to download the migration tool package.

    Using curl:

    ```powershell
    curl -o migration-tools-<VERSION>-windows.zip "https://commercial-acceptance.downloads.chef.co/current/migrate-ice/packages?v=<VERSION>&license_id=<LICENSE_ID>"
    ```

    Using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://commercial-acceptance.downloads.chef.co/current/migrate-ice/packages?v=<VERSION>&license_id=<LICENSE_ID>" -OutFile "migration-tools-<VERSION>-windows.zip"
    ```

    Replace:
    - `<VERSION>` with the version number from the previous step
    - `<LICENSE_ID>` with your Progress Chef License ID

1. Extract the migration tool.

    ```powershell
    mkdir C:\migrate-tool
    move "migration-tools-<VERSION>-windows.zip" "C:\migrate-tool\"
    cd C:\migrate-tool
    Expand-Archive -Path "migration-tools-<VERSION>-windows.zip" -DestinationPath "."
    ```

1. Optional: Verify that the migration tool works.

    ```powershell
    .\migrate-ice --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client using [`migrate-ice apply`](reference):

    You can install Chef Infra Client using either the download URL or by specifying a version number.

    **Method 1: Using download URL**

    ```powershell
    .\migrate-ice apply online --fresh-install --download-url "<CHEF_TAR_DOWNLOAD_URL>"
    ```

    Replace `<CHEF_TAR_DOWNLOAD_URL>` with the Chef Infra Client package download URL.

    **Method 2: Using version number**

    ```powershell
    .\migrate-ice apply online --fresh-install --chef-version <VERSION> --license-key "<LICENSE_KEY>"
    ```

    Replace `<VERSION>` with the Chef Infra Client version number (for example, 19.1.150) and `<LICENSE_KEY>` with your Progress Chef License key.

1. Verify the Chef Infra Client installation.

    ```powershell
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
