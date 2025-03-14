+++
title = "Migration tool"

+++

## Overview

Use the Migration Tool (`chef-migrate`) to install or upgrade versions of Chef Infra Client 19.
The tool provides flexible options for installing or migrating to Chef Infra 19, supporting both online and airgap installation modes.

### Key Features

- New installation of Chef Infra 19 Client (`chef-client`)
- Installation of the Chef Infra 19 RC1 Client, either removing the previous version or leaving the previous client installed (side-by-side mode, with the path to the most recent version taking precedence)
- Upgrading from the 17.x and 18.x versions of the Chef Infra Client (also referred to as “Omnibus distributions”)
- Upgrading to Chef Infra 19 RC1 Client and subsequent versions (also referred to as “Habitat-packaged”)

## Install the Chef Infra Client migration tool

To install the migration tool, run these commands:

```sh
wget <MIGRATION_TOOL_URL>
chmod +x chef-migrate-cli
mv chef-migrate-cli /usr/local/bin/
```

Please refer to the [page](https://progresssoftware.atlassian.net/wiki/spaces/Infra19/pages/1642201135 "https://progresssoftware.atlassian.net/wiki/spaces/Infra19/pages/1642201135") for the download URL of the Chef Migrate tool.

## Usage

The `chef-migrate apply` command upgrades Chef Infra Client to version 19.

It supports two subcommands:

- `online`: Uses network-connected resources to download and install Chef Infra 19.
- `airgap`: Uses pre-downloaded airgap bundles to perform the migration.

### General Command Structure

```sh
chef-migrate apply [command] [flags]
```

Run `apply` with help for more details:

```sh
chef-migrate-cli apply --help
```

## Online migration

The online migration method downloads the necessary files from the specified URL and installs Chef Infra 19 while handling configurations and dependencies.

### Syntax

```sh
chef-migrate apply online [flags]
```

### Options

`--debug`
: Enable debug logs (true/false).

`--download-url <URL>`
: Specify the Chef Infra Client download location.

`--fresh-install`
: Perform a fresh installation (true/false).

`--fstab <option>`
: Modify `/opt/chef` mount options. Default: `apply`.

`--habitat-upgrade`
: Upgrade Habitat to the latest version.

`--license-key <key>`
: License key for downloading Chef Infra Client.

`--license-server <URL>`
: URL of the private/public licensing service (optional).

`--preserve`
: Preserve the existing Omnibus installation (true/false).

`--process-config <option>`
: Parse `client.rb` for hardcoded `/opt/chef` paths (`ignore`, `warn`, `error`). Default: `error`.

`--selinux-ignore-warnings`
: Ignore warnings related to SELinux handling.

`--selinux-profile <option>`
: Apply a default/custom SELinux profile. Valid options: `default` or `<profile_file_path>`.

`--symlink`
: Create symbolic links for compatibility (default: false).

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

## Airgap Migration

The airgap migration method requires pre-downloaded bundles and doesn't require network access.

### Syntax

```sh
chef-migrate apply airgap [airgap_bundle] [flags]
```

### Options

`--debug`
: Enable debug logs (true/false).

`--fresh-install`
: Perform a fresh installation (true/false).

`--fstab <option>`
: Modify `/opt/chef` mount options (`apply`, `fail`, `ignore`). Default: `apply`.

`--habitat-upgrade`
: Upgrade Habitat to the latest version.

`--license-key <key>`
: License key for downloading Chef Infra Client.

`--license-server <URL>`
: URL of the private/public licensing service (optional).

`--preserve`
: Preserve the existing Omnibus installation (true/false).

`--process-config <option>`
: Parse `client.rb` for hardcoded `/opt/chef` paths (`ignore`, `warn`, `error`). Default: `error`.

`--selinux-ignore-warnings`
: Ignore warnings related to SELinux handling.

`--selinux-profile <option>`
: Apply a default/custom SELinux profile. Valid options: `default` or `<profile_file_path>`.

`--symlink`
: Create symbolic links for compatibility (default: false).

### Examples

Standard Airgap Migration:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --license-key "<LICENSE_KEY>"
```

Applying a Custom SELinux profile:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --license-key "<LICENSE_KEY>" --selinux-profile /custom/selinux/profile
```

## Fresh Install

The fresh install method ensures a clean installation of Chef Infra 19 without any prior version dependencies.

### Supported Flags for Fresh Install

`--license-key <key>`
: License key for downloading Chef Infra Client (Online only).

`--license-server <URL>`
: URL of the private/public licensing service (optional).

`--download-url <URL>`
: Specify the Chef Infra Client download location (Online only).

`--habitat`
: Install Habitat along with Chef Infra Client.

`--selinux-ignore-warnings`
: Ignore warnings related to SELinux handling.

`--selinux-profile <option>`
: Apply a default/custom SELinux profile. Valid options: `default` or `<profile_file_path>`.

### Syntax

```sh
chef-migrate apply online/airgap --fresh-install [flags]
```

### Examples

Standard Fresh Installation:

```sh
chef-migrate apply online --fresh-install --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>"
```

Standard Fresh Installation on Airgap environment:

```sh
chef-migrate apply airgap /path/to/airgap_bundle --fresh-install --license-key "<LICENSE_KEY>"
```

## Detailed Flag Reference for `chef-migrate`

### Handling mounted `/opt/chef` directory in `chef-migrate`

The `--fstab` flag in `chef-migrate` remounts the Chef installation from `/opt/chef` to the Habitat environment (`/hab`). This maintains system integrity while transitioning from an omnibus-based Chef installation to a Habitat-based setup.

When enabled, the `--fstab` flag verifies whether `/opt/chef` is currently mounted and migrates it to `/hab` while ensuring a rollback mechanism is in place. This migration is necessary to align with the Habitat-based Chef deployment and ensure seamless execution of Chef components post-migration.

#### Options

The `--fstab` flag supports three options that dictate how the migration process is handled:

1. apply – Performs the mount migration from `/opt/chef` to `/hab`. Default behavior.

2. fail – Checks whether `/opt/chef` is already mounted and logs the result without performing the migration.

3. ignore – Skips the mount migration check entirely.

#### Validation and execution

When the `apply` option is selected, the tool follows a step-by-step approach:

1. Check Existing Mounts

    - If `/hab` is already mounted, the process exits gracefully without making changes.

    - If `/opt/chef` isn't mounted, the process skips migration since no remounting is needed.

2. Backup and Remounting

    - The tool identifies the device currently mounted to `/opt/chef` and stores it for rollback purposes.

    - It creates the `/hab` directory if it doesn't exist.

    - The same device is mounted to `/hab`.

    - `/opt/chef` is unmounted after successful migration.

#### Rollback Mechanism

In case of a migration failure, the rollback process is triggered to restore the previous mount state. The rollback follows these steps:

1. If the `/hab` directory was mounted during the migration, it's unmounted to prevent conflicts.

2. Remount `/opt/chef` – The previously stored device is remounted to `/opt/chef`.

3. Log Rollback Completion – The system logs the successful rollback, ensuring it remains in a functional state.

#### Examples

Standard operation:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --fstab apply
```

Abort the migration if `/opt/chef` is mounted:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --fstab error
```

### Upgrade Chef Habitat

The `--habitat-upgrade` flag in `chef-migrate` ensures that the Chef Habitat (`hab`) binary on the system is updated to the latest version available in the migration package. This upgrade is crucial for maintaining compatibility with the latest Habitat features and ensuring a smooth migration process.

When enabled, the `--habitat-upgrade` flag checks the currently installed version of Habitat, compares it with the version provided in the chef-client package, and upgrades it if necessary. If the installed version is already up to date, no changes are made. The upgrade process includes a rollback mechanism to restore the system to its previous state in case of failure.

### Execution Flow

The tool follows a structured approach to upgrading Habitat:

1. Check for Existing Habitat Installation

    - If Habitat isn't installed on the system, the upgrade process is skipped.

    - If Habitat is installed, its current version is retrieved.

2. Determine Upgrade Requirements

    - The migration package is examined to extract the Habitat version included in it.

    - If the installed version matches or is newer than the package version, no upgrade is required.

    - If the installed version is older, an upgrade process is initiated.

3. Backup Critical Files for Rollback

    - The original Habitat binary (`/usr/bin/hab`) is backed up to a temporary location.

    - The `/hab` directory is also backed up to preserve existing data in case of a rollback.

    - The original symlink target of `/usr/bin/hab` is recorded to restore it if needed.

4. Perform Habitat Upgrade

    - The new Habitat version is installed from the migration package.

    - The `/usr/bin/hab` symlink is updated to point to the new binary under `/hab/bin/hab`.

    - A verification step ensures that the new version is correctly installed and functional.

#### Rollback in Case of Failure

- If any step fails, the rollback mechanism restores the previous Habitat binary and its configuration.

- The original `/usr/bin/hab` symlink is restored to its previous state.

- The backed-up `/hab` directory is reinstated to preserve system integrity.

#### Examples

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --habitat-upgrade
```

### Handling --symlink in `chef-migrate`

The `--symlink` flag in `chef-migrate` ensures that binaries from the Habitat-based Chef installation are used instead of the existing omnibus Chef binaries. This process is necessary for seamless execution after migration, allowing system components and scripts to interact with the correct Chef executables.

When the `--symlink` flag is enabled, the migration tool first takes a backup of the existing Chef installation to ensure that any unexpected failures can be rolled back safely. It then determines the correct locations of essential binaries like `ruby`, `chef-client`, and `openssl` within the Habitat environment. Using these resolved paths, it systematically replaces the existing omnibus Chef binaries with symbolic links pointing to their Habitat-based equivalents.

The directories processed for this transition include `/opt/chef/bin` and `/opt/chef/embedded/bin`. Each file within these directories is evaluated, and if it's an executable associated with Chef, the tool creates a symlink to the corresponding binary within Habitat. If no equivalent is found in Habitat, the file is left unchanged.

#### Validation and Constraints

Before executing the symlink replacement process, `chef-migrate` validates whether the `--symlink` flag can be used in conjunction with other options. Specifically, it enforces a dependency on the `--preserve` flag, ensuring that it's not set to `false` when using `--symlink`. This restriction prevents scenarios where the existing Chef installation is deleted before symlink creation, which would lead to broken references and potential failures.

#### Rollback Mechanism

In case of an error or failure during the migration process, a rollback mechanism is in place to restore the system to its original state. This involves deleting and recreating the original Chef installation directory and restoring the backed-up Chef binaries. This ensures that even if the migration is unsuccessful, the system remains functional with its previous Chef configuration intact.

#### Examples

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --preserve --symlink
```

### Preserve Omnibus-based Chef Infra Client

The `--preserve` flag in `chef-migrate` controls whether the existing Omnibus Chef Infra Client should be retained or removed during migration. This feature ensures flexibility in managing legacy Chef installations while transitioning to a Habitat-based setup.

When the flag is set, the tool retains the Omnibus Chef Infra Client, preventing its deletion. If the flag isn't enabled, the tool automatically removes the existing Omnibus installation to avoid conflicts. The process involves the following steps:

1. Validation – If `true`, the Omnibus client is preserved; otherwise, it's deleted. Deletion is the default behavior

2. Deletion Process – If the Omnibus client isn't preserved, the tool:

    - Checks if the Chef package is installed and removes it using the system's package manager.

    - Verifies the existence of the Omnibus Chef directory and deletes it after taking a backup.

3. Rollback Mechanism – In case of migration failure, the rollback restores the Omnibus Chef Infra Client by recreating the directory and restoring the backup.

#### Examples

To avoid deletion of Omnibus chef-client:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --preserve
```

### Handling --process-config in `chef-migrate`

The `--process-config` flag in `chef-migrate` analyzes the `client.rb` config file to determine if it references the Omnibus Chef installation (`/opt/chef`). This check helps identify potential conflicts when migrating to a Habitat-based setup.

1. Handling the `--process_config` Flag

    - The user specifies how configuration processing should be handled using one of the following options:

        - `"ignore"`: Skips the configuration check entirely.

        - `"warn"`: Logs a warning if `/opt/chef` is found in `client.rb` but continues execution.

        - `"error"`: Aborts execution if `/opt/chef` is found, preventing potential conflicts. Default behaviour.

    - If an invalid option is provided, the tool logs a message and skips processing.

2. Configuration Check Process

    - The handler scans the `client.rb` file for references to `/opt/chef`.

    - If found:

        - A warning is displayed if the mode is `"warn"`, allowing execution to proceed.

        - Execution is halted if the mode is `"error"`, ensuring conflicts are avoided.

    - If `/opt/chef` isn't found, a success message is logged, indicating no issues.

#### Examples

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --process-config warn
```

### Install an SELinux profile

Use the `--selinux-profile` flag to install an SELinux profile.
It ensures that Chef-related processes have appropriate security policies enforced by SELinux.
This handler provides flexibility for users to either use a default SELinux profile or specify a custom one.

1. Processing the `--selinux-profile` Flag

    - If the flag isn't provided, no action is taken.

    - If a profile is specified:

        - The system's SELinux mode is checked (`Enforcing`, `Permissive`, or `Disabled`).

        - The profile is copied to `/etc/selinux/`, either from the embedded default file or from a user-specified location.

        - The profile is compiled into a binary policy module.

        - The compiled policy module is installed on the system.

2. SELinux Mode Validation

    - The system's SELinux mode is retrieved using the `getenforce` command.

    - If SELinux is `Disabled` or `Permissive`, a warning is issued, but execution continues.

    - The handler doesn't modify the system's SELinux mode; it only installs policies.

    - On Windows, SELinux isn't applicable, and the handler exits with an error.

3. Copying the SELinux profile

    - If the user specifies a profile path, it's read from that location.

    - If the default profile is used, it's extracted from an embedded file.

    - The profile is saved in `/etc/selinux/` with the same filename as the source.

    - If a custom profile is provided, the handler ensures the file exists before proceeding.

4. Compiling the SELinux profile

    - The profile is compiled into a `.mod` file using `checkmodule`.

    - A `.pp` (policy package) file is generated using `semodule_package`.

    - The intermediate `.mod` file is deleted after compilation.

    - Make sure the required commands (`checkmodule`, `semodule_package`, `semodule`) must be available; otherwise, validation fails

5. Installing the SELinux Module

    - The compiled `.pp` file is installed using `semodule -i`.

    - A success message confirms the installation.

#### Examples

Install the default SELinux profile:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --selinux-profile default --selinux-ignore-warnings
```

Install a custom SELinux profile:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>" --selinux-profile --selinux-profile /custom/selinux/profile
```
