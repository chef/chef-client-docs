+++
title = "Upgrade to Chef Infra Client RC2"

[menu.install]
title = "Upgrade"
identifier = "install/upgrade"
parent = "install"
weight = 20
+++

This page documents how to upgrade to Chef Infra Client 19 RC2 from Chef Infra Client 18 or earlier.

To create a fresh install of Chef Infra Client 19 RC2, see the [install documentation]({{< relref "/install" >}}).

## Supported platforms

Chef Infra Client 19 RC2 is supported on Linux x86-64 systems.

## Prerequisites

- a valid Chef license key

## Upgrade Chef Infra Client

1. Optional: Verify which Chef Infra Client version is currently installed and where it's installed.

    ```sh
    chef-client --version
    ```

    Use `which` to identify the current path to the `chef-client` CLI:

    ```sh
    which chef-client
    ```

    This returns the path the `chef-client` CLI, for example `/usr/bin/chef-client`.

    This may be a symbolic link to the actual folder where the `chef-client` CLI and other tools from a previous install resides.

    You can use `ls -al` to identify any symbolic links:

    ```sh
    ls -al /usr/bin
    ```

    Which returns something like the following:

    ```sh
    total 56
    drwxr-xr-x   1 root root 4096 Nov 28 17:02 .
    drwxr-xr-x   1 root root 4096 Nov 28 17:02 ..
    lrwxrwxrwx   1 root root   11 Nov 28 17:02 chef-client -> /hab/chef/bin/chef-client
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until May 22, 2025.

    Using curl:

    ```sh
    curl -o chef-migration-tool.v1.tar.gz https://chef-hab-migration-tool-bucket.s3.amazonaws.com/migration-tools_Linux_x86_64.tar.gz\?AWSAccessKeyId\=AKIAW4FPVFT6LUYZUYOB\&Signature\=2P3xjN53%2Bib%2BnZBqFk5%2FsEORUzI%3D\&Expires\=1747912109
    ```

    Using Wget:

    ```sh
    wget -O "chef-migration-tool.v1.tar.gz" https://chef-hab-migration-tool-bucket.s3.amazonaws.com/migration-tools_Linux_x86_64.tar.gz\?AWSAccessKeyId\=AKIAW4FPVFT6LUYZUYOB\&Signature\=2P3xjN53%2Bib%2BnZBqFk5%2FsEORUzI%3D\&Expires\=1747912109
    ```

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

1. Upgrade Chef Infra Client RC2 using the migration tool.

    ```sh
    sudo ./chef-migrate apply online --preserve true --download.url "https://unstable-habitat-tarball.s3.amazonaws.com/chef-chef-infra-client-19.0.54-20241121145703.tar.gz?AWSAccessKeyId=AKIA2L25YRBIC3WVJTRM&Signature=Kp6oGpPRqwiNEhKh8UWlUPJZ6DU%3D&Expires=1747912507" --license.key <VALID_LICENSE_KEY>
    ```

    Replace `<VALID_LICENSE_KEY>` with a valid license key.

    The migration tool validates your Chef license, downloads Chef Infra Client from the specified download URL, and installs Chef Infra Client.
    The Chef Infra Client RC2 package is available for download as a zipped tar file from this pre-signed URL until May 22, 2025.

    {{< note >}}

    Use the `--debug` CLI option to get additional information about the install process.

    Logs are available in `/var/log/chef19migrate.log`.

    {{< /note >}}

1. Verify that Chef Infra Client 19 RC2 is installed:

    ```sh
    chef-client --version
    ```

    It returns version number 19.0.54 or greater.

    You can also verify that Chef Infra Client is installed by finding it in the `/hab/pkgs/chef/chef-infra-client/19.0.54` directory.

    And verify that symbolic links point to this version:

    ```sh
    ls -al /usr/bin
    ```

    This returns something like:

    ```sh
    total 56
    drwxr-xr-x   1 root root 4096 Nov 28 17:02 .
    drwxr-xr-x   1 root root 4096 Nov 28 17:02 ..
    lrwxrwxrwx   1 root root   11 Nov 28 17:02 chef-client -> /hab/chef/bin/chef-client
    ```

## Next step

- Add a [Chef license]({{< relref "/license" >}}) to Chef Infra Client.
