+++
title = "Apply a license in Chef Infra Client"
linkTitle = "Apply a license"

[menu.licensing]
title = "Apply a license"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

Chef Infra Client 19 requires a license to run. This document describes how to set a license and verify that it's accepted.

## Add a license

Chef Infra Client has three ways to set a license: with a command line option, an environment variable, or the command line interactive dialog.

After setting a license key, Chef Infra Client validates it with Progress Chef's licensing service.

### Environment variable

You can set the license key adding the `CHEF_LICENSE_KEY` environment variable:

```sh
export CHEF_LICENSE_KEY=<LICENSE_KEY>
```

### Command line option

You can set the license key using the `--chef-license-key` CLI option:

```sh
chef-client --chef-license-key=<LICENSE_KEY>
```

### Interactive license dialog

If you run a `chef-client` command, Chef Infra Client starts an interactive licensing dialog if a license key isn't already set.

1. Verify the version of Chef Infra Client you have installed:

    ```sh
    chef-client --version
    ```

    It should return version 19.0.54 or greater for Infra Client RC 1.

1. Run `chef-client` in local mode and why-run mode:

    ```sh
    chef-client --local-mode --why-run
    ```

    Local mode runs Chef Infra Client on your local machine as if it were running against Chef Infra Server. why-run mode shows you what Chef Infra Client would configure had an actual Chef Infra Client run occurred.

1. At the first prompt, select **I already have a license ID**.

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

