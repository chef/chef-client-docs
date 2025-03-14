+++
title = "Install Chef Infra Client using the migration tool"
linkTitle = "Download and install"

[menu.install]
title = "Install"
identifier = "install/install"
parent = "install"
weight = 10
+++

This page documents how to do a clean install of Chef Infra Client RC2 using the Chef Infra Client migration tool on a system that doesn't have a previous version of Chef Infra Client installed.

To upgrade to Chef Infra Client 19 RC2 from an earlier major version, see the [upgrade documentation]({{< relref "/upgrade" >}}).

## Supported platforms

Chef Infra Client 19 RC2 is supported on Linux x86-64 systems.

## Prerequisites

- a valid Chef License key

## Install the Chef Infra Client migration tool

1. Optional: Verify that Chef Infra Client isn't already installed on your system:

    ```sh
    chef-client --version
    ```

1. Download the Chef Infra Client migration tool.

    The migration tool is available for download as a zipped tar file using a pre-signed URL from an S3 bucket until May 22, 2025.

    Using curl:

    ```sh
    curl -o chef-migration-tool.v1.tar.gz https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424
    ```

    Using Wget:

    ```sh
    wget -O "chef-migration-tool.v1.tar.gz" https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_migration_tool/migration-tools_Linux_x86_64.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=hbgCCCl9r48WHDP%2FFQtNTN9pFJw%3D&Expires=1756222424
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

## Optional: Download Chef Infra Client

If you're installing Chef Infra Client in an airgapped environment, download the Chef Infra Client 19 RC2 tar file using an internet-connected machine.

Download using curl:

  ```sh
  curl -o chef-chef-infra-client-19.1.rc2.tar.gz https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-chef-infra-client-19.1.rc2.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682
  ```

Download using wget:

  ```sh
  wget -O "chef-chef-infra-client-19.1.rc2.tar.gz" https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_tar_folder/chef-chef-infra-client-19.1.rc2.tar.gz?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=Q91HiSIzOxffl52La8EvqSXSqWk%3D&Expires=1756222682
  ```

## Install Chef Infra Client 19 RC2

Use the `chef-migrate apply` command to install or upgrade Chef Infra Client to version 19 RC2 in either an internet-connected or airgapped environment.

## Fresh install

The fresh install method ensures a clean installation of Chef Infra 19 without any prior version dependencies.

### Syntax

```sh
chef-migrate apply <ENVIRONMENT> --fresh-install [flags]
```

Replace `<ENVIRONMENT>` with either `online` or `airgap`.

### Examples

Standard Fresh Installation:

```sh
chef-migrate apply online --fresh-install --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>"
```

Standard Fresh Installation on airgapped environment:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --fresh-install --license-key "<LICENSE_KEY>"
```

## Online migration

The online migration method downloads and installs Chef Infra 19 while handling configurations and dependencies.

### Syntax

```sh
chef-migrate apply online [flags]
```

### Examples

Standard Online Migration:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>"
```

Preserving Existing Omnibus Installation:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --preserve true
```

Install 'default' SELinux profile:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --selinux-profile default --selinux-ignore-warnings
```

## Airgapped migration

To migrate in an airgapped environment,

An airgapped migration requires pre-downloaded bundles and doesn't require network access.

### Syntax

```sh
chef-migrate apply airgap [airgap_bundle] [flags]
```

### Examples

Standard airgapped migration:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --license-key "<LICENSE_KEY>"
```

To upgrade and apply a custom SELinux profile:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --license-key "<LICENSE_KEY>" --selinux-profile <PROFILE_PATH>
```

### Probably delete this

1. Install Chef Infra Client RC2 with the migration tool using the `apply online` command.

    ```sh
    sudo ./chef-migrate apply online --fresh_install --preserve true --download.url "https://unstable-habitat-tarball.s3.amazonaws.com/chef-chef-infra-client-19.0.54-20241121145703.tar.gz?AWSAccessKeyId=AKIA2L25YRBIC3WVJTRM&Signature=Kp6oGpPRqwiNEhKh8UWlUPJZ6DU%3D&Expires=1747912507" --license.key <VALID_LICENSE_KEY>
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

## Migration tool CLI reference

The `chef-migrate apply` command upgrades or installs Chef Infra Client to version 19.

This command has the following basic syntax:

```sh
chef-migrate apply [command] [flags]
```

It supports two subcommands:

- `online`: Uses network-connected resources to download and install Chef Infra 19.
- `airgap`: Uses pre-downloaded airgapped bundles to perform the migration.

### Flags

`--debug`
: Enable debug logs. Valid values are: `true` or `false`.

`--download-url <URL>`
: Specify the Chef Infra Client download location.

`--fresh-install`
: Perform a fresh installation. Valid values are: `true` or `false`.

`--fstab <option>`
: Modify `/opt/chef` mount options. Default: `apply`.

`--habitat`
: Install Habitat along with Chef Infra Client.

`--habitat-upgrade`
: Upgrade Habitat to the latest version.

`--help`
: Get CLI command help.

`--license-key <key>`
: License key for downloading Chef Infra Client.

`--license-server <URL>`
: URL of the private or public Chef licensing service (optional).

`--preserve`
: Preserve the existing Omnibus installation. Valid values are: `true` or `false`.

`--process-config <option>`
: Parse `client.rb` for hardcoded `/opt/chef` paths (`ignore`, `warn`, `error`). Default: `error`.

`--selinux-ignore-warnings`
: Ignore warnings related to SELinux handling.

`--selinux-profile <option>`
: Apply a default/custom SELinux profile. Valid options: `default` or `<PROFILE_FILE_PATH>`.

`--symlink`
: Create symbolic links for compatibility (default: false).

## Next step

- Add a [Chef license]({{< relref "/license" >}}) to Chef Infra Client.
