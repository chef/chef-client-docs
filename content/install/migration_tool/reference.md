+++
title = "Migration tool CLI reference"

[menu.install]
title = "CLI reference"
identifier = "install/migration_tool/reference"
parent = "install/migration_tool"
weight = 999
+++

## Syntax

The `chef-migrate apply` command upgrades or installs Chef Infra Client to version 19.

This command has the following basic syntax:

```sh
chef-migrate apply {airgap|online} [flags]
```

It supports two subcommands:

- `airgap`: Uses pre-downloaded airgapped bundles to perform the install or upgrade.
- `online`: Uses network-connected resources to download and install Chef Infra Client 19.

## Flags

<!-- markdownlint-disable MD006 MD007 -->

`--debug`
: Enable debug logs. Logs are available in `/var/log/chef19migrate.log`. Valid values are: `true` or `false`.

`--download-url <URL>`
: Specify the Chef Infra Client download location.

`--fresh-install`
: Perform a fresh installation. Valid values are: `true` or `false`.

`--fstab <option>`
: Remount Chef Infra Client from `/opt/chef` to `/hab`.
  This maintains system integrity while transitioning from an Omnibus-based Infra Client installation to a Habitat-based setup.

  Valid values:

  - `apply`: Performs the mount migration from `/opt/chef` to `/hab`. Default behavior.
  - `fail`: Checks whether `/opt/chef` is already mounted and logs the result without performing the migration.
  - `ignore`: Skips the mount migration check entirely.

  Default value: `apply`.

`--habitat`
: Install Chef Habitat along with Chef Infra Client.

`--habitat-upgrade`
: Upgrade Chef Habitat to the latest version.

`--help`
: CLI command help.

`--license-key <key>`
: A Progress Chef License key for downloading Chef Infra Client.

`--license-server <URL>`
: URL of the private or public Chef licensing service (optional).

`--preserve`
: Preserve the existing Omnibus installation. Valid values are: `true` or `false`.

`--process-config <option>`
: Analyzes the `client.rb` config file to determine if it references the Omnibus-based Chef Infra Client installation (`/opt/chef`). This identifies potential conflicts when migrating to a Habitat-based setup.

  Valid values:

  - `ignore`: Skips the configuration check entirely.
  - `warn`: Logs a warning if `/opt/chef` is found in `client.rb` but continues execution.
  - `error`: Aborts execution if `/opt/chef` is found, preventing potential conflicts.

  Default value: `error`.

`--selinux-ignore-warnings`
: Ignore warnings related to SELinux handling.

`--selinux-profile <option>`
: Install a default or custom SELinux profile.

  Valid options: `default` or `<PROFILE_FILE_PATH>`.

`--symlink`
: Replaces symbolic links to essential binaries---for example, `ruby`, `chef-client`, and `openssl`---from Omnibus-based to Habitat-based Chef Infra Client.

  This processes binaries in `/opt/chef/bin` and `/opt/chef/embedded/bin`. Each file within these directories is evaluated and if it's an executable associated with Chef, the tool creates a symlink to the corresponding binary within Chef Habitat. If no equivalent is found in Habitat, the file is left unchanged.

  Default value: `false`.

<!-- markdownlint-enable MD006 MD007 -->

## Examples

### Upgrade Chef Infra Client

These examples show how to upgrade Chef Infra Client to version 19 RC2 from an earlier version.

Standard online upgrade:

```sh
chef-migrate apply online --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>"
```

Standard airgapped upgrade:

```sh
chef-migrate apply airgap </PATH/TO/BUNDLE> --license-key "<LICENSE_KEY>"
```

### Install Chef Infra Client

These examples show how to perform a fresh install of Chef Infra Client 19 RC2.

Standard online installation:

```sh
chef-migrate apply online --fresh-install --download-url "<DOWNLOAD_URL>" --license-key "<LICENSE_KEY>"
```

Standard airgapped installation:

```sh
chef-migrate apply airgap </PATH/TO/BUNDLE> --fresh-install --license-key "<LICENSE_KEY>"
```

### Manage Omnibus-based Chef Infra Client

Preserve an Omnibus-based Chef Infra Client installation:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --preserve
```

Log a warning if the `client.rb` config file references the Omnibus-based Chef Infra Client installation (`/opt/chef`):

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --process-config warn
```

Replace the existing Omnibus-based Chef binaries (for example, `ruby`, `chef-client`, and `openssl`) with symbolic links pointing to their Habitat-based equivalents.

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --preserve --symlink
```

Remount Chef Infra Client from `/opt/chef` to `/hab`:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --fstab apply
```

Abort the migration process if `/opt/chef` is already mounted:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --fstab fail
```

### Manage Chef Habitat

Install Chef Habitat while installing Chef Infra Client:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --habitat
```

Upgrade Chef Habitat while installing Chef Infra Client:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --habitat-upgrade
```

### SELinux profiles

Install the default SELinux profile:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --selinux-profile default --selinux-ignore-warnings
```

Install a custom SELinux profile:

```sh
chef-migration apply {airgap|online} --license-key "<LICENSE_KEY>" --selinux-profile <PATH/TO/CUSTOM/PROFILE>
```
