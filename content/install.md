+++
title = "Install Chef Infra Client"
linkTitle = "Download and install"

[menu.install]
title = "Install"
identifier = "install/install"
parent = "install"
weight = 10
+++

This page documents how to do a clean install of Chef Infra Client RC1 using the Chef Infra Client migration tool on a system that doesn't have a previous version of Chef Infra Client installed.

To upgrade to Chef Infra Client 19 RC1 from an earlier major version, see the [upgrade documentation]({{< relref "/upgrade" >}}).

## Supported platforms

Chef Infra Client 19 RC1 is supported on Linux x86-64 systems.

## Prerequisites

- a valid Chef license key

## Install Chef Infra Client

1. Optional: Verify that Chef Infra Client isn't already installed on your system:

    ```sh
    chef-client --version
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available in zipped tar format from a pre-signed URL from an S3 bucket and is available for 90 days from November 26, 2024.

    Using curl:

    ```sh
    curl -o chef-migration-tool.v1.tar.gz https://chef-hab-migration-tool-bucket.s3.amazonaws.com/migration-tools_Linux_x86_64.tar.gz\?AWSAccessKeyId\=AKIAW4FPVFT6LUYZUYOB\&Signature\=FMsMGzoZe1YTYA4DbpOIEB%2FHHSw%3D\&Expires\=1740411440
    ```

    Using Wget:

    ```sh
    wget -o "chef-migration-tool.v1.tar.gz" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/migration-tools_Linux_x86_64.tar.gz\?AWSAccessKeyId\=AKIAW4FPVFT6LUYZUYOB\&Signature\=FMsMGzoZe1YTYA4DbpOIEB%2FHHSw%3D\&Expires\=1740411440"
    ```

    {{< note >}}

    If the command line doesn't fetch the migration tool file, add quotes around the S3 bucket URL---some shell environments don't interpret the path correctly.

    {{< /note >}}

1. Extract the migration tool in a temporary directory.

    Use the `-C` flag select a directory to unzip and un-tar the files.

    ```sh
    tar -xvf chef-migration-tool.v1.tar.gz -C /path/to/folder
    ```

1. Optional: Verify that the migration tool is installed.

    ```sh
    cd /path/to/folder
    ./chef-migrate --help
    ```

    The migration tool returns available commands and usage guidelines.

1. Install Chef Infra Client RC1 with the migration tool using the `apply online` command.

    ```sh
    sudo ./chef-migrate apply online --fresh_install --preserve true --download.url "https://unstable-habitat-tarball.s3.amazonaws.com/chef-chef-infra-client-19.0.54-20241121145703.tar.gz?AWSAccessKeyId=AKIA2L25YRBIC3WVJTRM&Signature=XDGliip78EyaiazMnbi7N8Pao%2Bk%3D&Expires=1740407376" --license.key <VALID_LICENSE_KEY>
    ```

    Replace `<VALID_LICENSE_KEY>` with a valid license key.

    The migration tool validates your Chef license, downloads Chef Infra Client from the specified download URL, and installs Chef Infra Client.
    The Chef Infra Client RC1 package is available in zipped tar format from this pre-signed URL for 90 days from November 26, 2024.

    {{< note >}}

    Use the `--debug` CLI option to get additional information about the install process.

    Logs are available in `/var/log/chef19migrate.log`.

    {{< /note >}}

1. Verify that Chef Infra Client 19 RC1 is installed:

    ```sh
    chef-client --version
    ```

    It returns version number 19.0.54 or greater.

    You can also verify that Chef Infra Client is installed by finding it in the `/hab/pkgs/chef/chef-infra-client/19.0.54` directory.

## Next step

- Add a [Chef license]({{< relref "/license" >}}) to Chef Infra Client.