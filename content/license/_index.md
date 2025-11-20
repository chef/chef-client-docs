+++
title = "Apply a license in Chef Infra Client"
linkTitle = "Apply a license"

[menu.licensing]
title = "Apply a license"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

This document outlines the licensing requirements and enforcement policies for Chef Infra Client 19.

## Licensing requirements

Chef Infra Client 19 has different licensing requirements depending on how you install it:

- **API Downloads**: You need a license key to download Chef Infra Client 19 software through the API.
- **Runtime Execution**: Chef Infra Client 19 requires a valid license to run if you install it as an unofficial distribution (for example, Chef Infra Client 19 installed as a Ruby gem).

## License enforcement policy

### No enforcement

Chef Infra Client doesn't require a license if you download official distributions (customer portal, HAB).

### License required

You need a license key to run Chef Infra Client when you:

- Download it from unofficial sources (public Ruby gem)
- Use runtime installations and workflows

## Add a license

You can set a license in Chef Infra Client 19 using one of three methods:

- An environment variable
- A command line option
- The command line interactive dialog

After you set a license key, Chef Infra Client validates it with Progress Chef's licensing service.

### Environment variable

Set the license key by adding the `CHEF_LICENSE_KEY` environment variable:

```sh
export CHEF_LICENSE_KEY=<LICENSE_KEY>
```

### Command line option

Set the license key using the `--chef-license-key` CLI option:

```sh
chef-client --chef-license-key=<LICENSE_KEY>
```

### Interactive license dialog

If you run a `chef-client` command and a license key isn't already set, Chef Infra Client starts an interactive licensing dialog.

To set a license key with the CLI interactive dialog, follow these steps:

1. Verify the version of Chef Infra Client you have installed:

    ```sh
    chef-client --version
    ```

    This should return version 19.0.54 or greater for Infra Client RC 1.

1. Run `chef-client` in local mode and why-run mode:

    ```sh
    chef-client --local-mode --why-run
    ```

    Local mode runs Chef Infra Client on your local machine as if it were running against Chef Infra Server.
    Why-run mode shows you what Chef Infra Client would configure during a Chef Infra Client run.

1. At the first prompt, select **I already have a license ID**:

    ```text
    Please choose one of the options below (Press ↑/↓ arrow to move and Enter to select)
    ‣ I already have a license ID
      I don't have a license ID and would like to generate a new license ID
      Skip
    ```

1. Enter your license key at the second prompt.

    ```text
    Please enter your license ID:  <LICENSE_KEY>
    ✔ [Success] License validated successfully.
    ```

    After entering the license key, Chef Infra Client verifies your license and the run completes.

## Next step

After installing Chef Infra Client and adding a license, you can test it by running an [example cookbook](/cookbooks).
