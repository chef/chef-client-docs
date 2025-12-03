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
    curl -o chef-ice-19.2.rc3-linux.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=htVtnPFhoan9wyXixccqDFp0jmU%3D&Expires=1780533226"
    ```

    Download using Wget:

    ```sh
    wget -O "chef-ice-19.2.rc3-linux.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=htVtnPFhoan9wyXixccqDFp0jmU%3D&Expires=1780533226"
    ```

1. On an internet-connected machine, download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until April 23, 2026.

    Using curl:

    ```sh
    curl -o migration-tools-1.1.rc3-linux.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/linux/migration-tools-1.1.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=O8rQUc0jy%2BeP7U1WspJasr7qMTY%3D&Expires=1780533385"
    ```

    Using Wget:

    ```sh
    wget -O "migration-tools-1.1.rc3-linux.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/linux/migration-tools-1.1.rc3-linux.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=O8rQUc0jy%2BeP7U1WspJasr7qMTY%3D&Expires=1780533385"
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
    curl -o chef-ice-19.2.rc3-windows.tar.gz "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=2jIjDACxF0EYf8yICEp698kt0xY%3D&Expires=1780533373"
    ```

    Download using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=2jIjDACxF0EYf8yICEp698kt0xY%3D&Expires=1780533373" -OutFile "chef-ice-19.2.rc3-windows.tar.gz"
    ```

1. On an internet-connected machine, download the Chef Infra Client migration tool.

    The migration tool is available for download as a ZIP file using a pre-signed address from an S3 bucket until April 23, 2026.

    Using curl:

    ```powershell
    curl -o migration-tools-1.1.rc3-windows.zip "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/windows/migration-tools-1.1.rc3-windows.zip?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=xyfZ7g7D5jLF5jY%2B8DfBkEedSUA%3D&Expires=1780533399"
    ```

    Using PowerShell:

    ```powershell
    Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/migrate-ice/1.1.RC3/windows/migration-tools-1.1.rc3-windows.zip?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=xyfZ7g7D5jLF5jY%2B8DfBkEedSUA%3D&Expires=1780533399" -OutFile "migration-tools-1.1.rc3-windows.zip"
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
