+++
title = "Licensing Chef Infra Client"
linkTitle = "Licensing"

[menu.licensing]
title = "Apply a license"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

Before running Chef Infra Client, you must accept the Chef EULA and add a license key.
You can [request a trial license](https://www.chef.io/license-generation-free-trial) if you'd like to try out Chef Infra Client.

For more information on Chef licenses, see [Chef's licensing documentation](https://docs.chef.io/licensing/).

## Accept the Chef EULA

You must accept the [Chef End User License Agreement (EULA)](https://www.chef.io/end-user-license-agreement) before running Chef Infra Client using one of the following methods:

- [command line option](#command-line-option)
- [environment variable](#environment-variable)

If you don't set a command line argument or environment variable, Chef Infra Client requests acceptance through an interactive prompt. If the prompt can't be displayed, then the product will fail with exit code 172.

If the product attempts to persist the accepted license and fails, Chef Infra Client sends a message to STDOUT and continues to run. In a future invocation, you will need to accept the license again.

### Command line option

Use the `--chef-license <VALUE>` argument to accept the Chef EULA.

Replace `<VALUE>` with one of the following options.

`accept`
: Accept the license and attempts to persist a marker file locally. Persisting these marker files means future invocations don't require accepting the license again.

`accept-silent`
: Similar to `accept`, but no messaging is sent to STDOUT.

`accept-no-persist`
: Similar to `accept-silent`, but no marker file is persisted. Future invocation will require accepting the license again.

### Environment variable

Use the `CHEF_LICENSE="<VALUE>"` environment variable to accept the Chef EULA.

Replace `<VALUE>` with one of the following options:

`accept`
: Accept the license and attempts to persist a marker file locally. Persisting these marker files means future invocations don't require accepting the license again.

`accept-silent`
: Similar to `accept`, but no messaging is sent to STDOUT.

`accept-no-persist`
: Similar to `accept-silent`, but no marker file is persisted. Future invocation will require accepting the license again.

## License key

You can add a license key to Chef Infra Client using one of three methods:

- [environment variable](#environment-variable-1)
- [command line option](#command-line-option-1)
- [interactive license dialog](#interactive-license-dialog)

{{< note >}}

Existing commercial customers of Progress Chef can use an asset serial number from the [Progress support portal](https://community.progress.com/s/products/chef) as a license key.

{{< /note >}}

### Environment variable

- You can set the license key adding the `CHEF_LICENSE_KEY` environment variable:

  ```sh
  export CHEF_LICENSE_KEY=<LICENSE_KEY>
  ```

### Command line option

- You can set the license key using the `--chef-license-key` CLI option:

  ```sh
  chef-client --chef-license-key=<LICENSE_KEY>
  ```

### Interactive license dialog

The easiest way to add a license key to Chef Infra Client is to run it.
Start a Client run and it starts an interactive licensing dialog
if a license key isn't already set and it doesn't detect an automated method of setting the license key.

To set a license key with the CLI interactive dialog, follow these steps:

1. Verify the version of Chef Infra Client you have installed:

    ```sh
    chef-client --version
    ```

    It should return version 19.0.54 or greater for Infra Client RC 1.

1. Run `chef-client` in local mode and why-run mode:

    ```sh
    chef-client --local-mode --why-run
    ```

    Local mode runs Chef Infra Client on your local machine as if it were running against Chef Infra Server. why-run mode shows you what Chef Infra Client would configure if a Chef Infra Client run occurs.

1. At the first prompt, select **I already have a license ID**.

    ```bash
    ------------------------------------------------------------
      License ID Validation

      To continue using Chef Infra, a license ID is required.
      (Free, Trial, or Commercial)

      If you generated a license previously, you might
      have received it in an email.

      If you are a commercial user, you can also find it in the
      https://community.progress.com/s/products/chef portal.
    ------------------------------------------------------------

    Please choose one of the options below (Press ↑/↓ arrow to move and Enter to select)
    ‣ I already have a license ID
      I don't have a license ID and would like to generate a new license ID
      Skip
    ```

1. Enter your license key at the second prompt.

   ```bash
   Please choose one of the options below I already have a license ID
   Please enter your license ID:  <LICENSE_KEY>
   ✔ [Success] License validated successfully.
   ------------------------------------------------------------
   License Details
     Asset Name       : Infra
     License ID       : <LICENSE_KEY>
     Type             : Trial
     Status           : Active
     Validity         : Unlimited
     No. Of Units     : 10 Targets
   ------------------------------------------------------------
   ```

Chef Infra Client validates the license key, displays information about the license entitlements, and then executes the run.
Infra Client stores license keys for future use and won't prompt you for the license key for the duration of your license.

## Chef Local License Service

For large or isolated (air-gapped) fleets, Chef Infra Client can retrieve a license key from a [Chef Local License Service](https://docs.chef.io/licensing/local_license_service/).
With Chef Local License Service, Infra Client users don't need to know a license key---only the service URL.

Chef Infra Client sends a request to the Local License Service for a list of license keys and then uses that response to license itself during execution.
Infra Client won't prompt you for a license key.
Infra Client doesn't store license keys for long-term use when they're retrieved from a Chef Local License Service.

Use one of the following methods to set a Local License Service URL:

- [command line option](#command-line-option-2)
- [environment variable](#environment-variable-2)

### Command line option

- Use the `--chef-license-server` command line option to set a Chef Local License Service URL. For example:

  ```bash
  --chef-license-server https://license-server.example.com
  ```

### Environment variable

- Use the `CHEF_LICENSE_SERVER` environment variable to set a Chef Local License Service URL. For example:

  ```bash
  export CHEF_LICENSE_SERVER=https://license-server.example.com
  ```

#### Multiple license servers

You can deploy multiple Chef Local License Services, which provides resiliency and redundancy for managing licenses.

- To set multiple Chef Local License Services, enter up to five URLs as a comma-separated list. For example:

  ```bash
  export CHEF_LICENSE_SERVER=https://license-server-01.example.com,https://license-server-02.example.com
  ```

  Chef Infra Client tries each URL and uses the first one that works.

This capability is basic and you must synchronize the license servers, otherwise you may get inconsistent results.
