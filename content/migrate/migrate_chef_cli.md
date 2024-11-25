+++
title = "Migrate Chef CLI"
linkTitle = "Migrate Chef CLI"

[menu.migrate]
title = "Migrate Chef CLI"
identifier = "migrate/migrate_chef_cli"
parent = "migrate"
weight = 12
+++

The Chef Migrate Tool is a powerful, flexible, and easy-to-use Command-Line Interface (CLI) tool designed for seamless migration from earlier versions of Chef Infra Client to the latest Chef Infra Client (version 19). This tool facilitates a smooth transition from a Chef Infra Client Omnibus-based installation to a Chef Infra Client Habitat-based installation. The Chef Migrate Tool offers a range of commands that ensure a controlled and efficient migration process, making it suitable for both simple environments and complex infrastructures:

`apply`
: Performs the migration by applying changes

`assess`
: Performs a pre-flight assessment check

`remove`
: Uninstalls Chef Infra Client

The tool supports both online and air-gapped migrations, enabling flexibility depending on network connectivity and security constraints. It also includes options to assess the migration feasibility and remove existing installations, making it a comprehensive solution for Chef Infra Client upgrades.

## Command overview

To begin using the Chef Migrate Tool, ensure it is installed and accessible from your command line. You can view the help information by running the following command:

```sh
chef-migrate-cli --help
```

## Available commands

The `apply` command executes the migration process by applying the necessary changes to transition from an Omnibus-based installation to a Habitat-based installation.

- **Usage:**
    ```sh
    chef-migrate apply [command]
    ```
- **Sub-commands:**
  - **airgap:** Performs the migration using an airgapped bundle. This is suitable for environments where the target machines do not have internet access. All necessary resources must be pre-packaged and available locally.
  - **online:** Performs the migration using network-connected resources. This option requires an active internet connection to download the required assets during the migration process.
- **Example:**

    ```sh
    chef-migrate apply online <flags>
    chef-migrate apply airgap [bundle-path] <flags>
    ```

- **Global flags:** `-h, --help`: Displays the help information for the command or subcommand.

## Detailed usage example

To initiate an online migration, use the following command structure:

```sh
chef-migrate apply online [flags]
```

This command performs the migration using online resources, downloading the required packages, applying configuration changes, and verifying the upgrade.

## Command options

The online migration command comes with several configurable options that allow you to control the migration process. Each option is specified using flags, enabling you to tailor the behavior of the migration to your specific requirements.

### Available flags

The following table provides a detailed description of each available flag for the online migration:

| Flag | Description | Type | Default | Example |
|-------------------|--------------------------------------------------------------------|-----------------------|---------|--------------------------------|
| `--debug`          | Enables debug-level logging for detailed diagnostics.              | Boolean (`true/false`)  | `false`   | `--debug=true`                |
| `--download.url`    | Specifies the URL to download the Chef Infra Client package.       | String                | None    | `--download.url=<https://example.com/chef-client/package>`                 |
| `--fresh_install`   | Enables a fresh installation of Chef Infra Client.                 | Boolean (`true/false`)  | `false`   | `--fresh_install=true`           |
| `--license.key`     | Provides the license key for downloading the Chef Client.          | String                | None    | `--license.key=your-license-key` |
| `--license.server`  | Specifies the URL for the licensing service (optional).            | String                | None    | `--license.server=<https://licenses.example.com>`              |
| `--preserve`        | Determines whether to preserve the existing Omnibus installation.  | String (`true/false`)   | false   | `--preserve=true`                |
| `-h, --help`        | Displays help information for the `online` command.                  | Command               | None    | `--help`                         |

### Flag descriptions

`--debug`
: Enables detailed debug logs during the migration process. This is particularly useful for troubleshooting or gaining insights into the specific steps being executed. Set it to `true` to enable debug mode. Log file default location: `/var/log/chef19migrate.log`

    **Example:**

    ```sh
    chef-migrate apply online --debug=true
    ```

`--download.url`
: Specifies the URL from which the Chef Infra Client package will be downloaded. This allows you to define a custom source for the installation package if needed. For RC1, you do not need to specify anything for this flag.

    **Example:**

    ```sh
    chef-migrate apply online --download.url=<https://example.com/chef-client/package>
    ```

`--fresh_install`
: If set to true, this flag triggers a fresh installation of the Chef Infra Client instead of an upgrade. This is useful for scenarios where a clean install is preferred over upgrading the existing installation.

    **Example:**

    ```sh
    chef-migrate apply online --fresh_install=true
    ```

`--license.key`
: This flag allows you to specify a license key required for downloading the Chef Infra Client package. Ensure that the license key provided is valid for the target installation.

    **Example:**

    ```sh
    chef-migrate apply online --license.key=your-license-key
    ```

`--license.server`  [OPTIONAL]
: An optional flag that defines the URL of the private or public licensing service. If your environment uses a custom license server, specify its URL here. If a public license server is used, do not specify anything for this flag.

    **Example:**

    ```sh
    chef-migrate apply online --license.server=<https://licenses.example.com>
    ```

`--preserve`
: This flag controls whether to keep the existing Chef Omnibus installation intact during the migration. Set it to `true` if you want to preserve the previous setup; otherwise, the Omnibus installation will be removed.

    **Example:**

    ```sh
    chef-migrate apply online --preserve=true
    ```

`-h, --help`
: Displays the help information for the online migration command. Use this flag if you need a quick reference to the command syntax and options.

    **Example:**

    ```sh
    chef-migrate apply online --help
    ```

## Examples

Refer to the following sections for examples.

### Perform an online migration with default options

To perform a basic online migration without any special configurations, run:

```sh
chef-migrate apply online --license.key <VALID_LICENSE_KEY>
```

### Perform an online migration with debugging enabled

If you need detailed logs for troubleshooting, add the `--debug` flag:

```sh
chef-migrate apply online --license.key <VALID_LICENSE_KEY> --debug=true
```

### Fresh installation of Chef Infra Client

For a fresh installation rather than an upgrade, use the `--fresh_install` flag:

```sh
chef-migrate apply online --license.key <VALID_LICENSE_KEY> --fresh_install=true
```

### Preserve the existing Omnibus installation

To keep the existing Omnibus setup, set `--preserve` to true:

```sh
chef-migrate apply online --license.key <VALID_LICENSE_KEY> --preserve=true
```

You can see the documentation of the migration CLI by running `chef-migrate --help`.

The documentation pages are automatically created using RDOC as markdown.
