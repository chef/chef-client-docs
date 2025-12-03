+++
title = "Install Chef Infra Client using the migration tool in an air-gapped environment"
draft = true

[menu.install]
title = "Air-gapped install"
identifier = "install/migration_tool/install_airgap"
parent = "install/migration_tool"
weight = 20
+++

This page documents how to do a fresh install of Chef Infra Client RC3 in an air-gapped environment.

## Supported platforms

Chef Infra Client 19 RC3 is supported on Linux x86-64 systems.

## Prerequisites

- a valid Chef License key

## Install Chef Infra Client

To install Chef Infra Client, follow these steps:

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

1. Install Chef Infra CLient using [`chef-migrate apply`](reference):

    ```sh
    sudo chef-migrate apply airgap <PATH/TO/BUNDLE> --fresh-install --license-key "<LICENSE_KEY>"
    ```

1. Verify that Chef Infra Client is installed.

    ```sh
    chef-client --version
    ```

## Next step

- [Add a Chef license](/license)
