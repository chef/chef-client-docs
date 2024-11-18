+++
title = "How to Apply a License"
linkTitle = "How to Apply a License"

[menu.licensing]
title = "How to Apply a License"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

Details on how to accept the End User License Agreement (EULA) and obtain the different license types are provided in the following sections.

## Accept the EULA

To accept the EULA in Chef Infra Client, you can use a command line option, environment variable, or config file.

### Options

Chef Infra Client accepts the following license acceptance options:

`accept`
: Accepts the license and attempts to persist a marker file locally. Persisting these marker files means that future invocations do not require the license to be accepted again.

`accept-silent`
: Similar to accept, but no messaging is sent to STDOUT.

`accept-no-persist`
: Similar to accept-silent, but no marker file is persisted. Future invocation requires the license to be accepted again.

### Command line option

Accept the Chef License with a command line invocation. For example:

```sh
chef-client --chef-license <LICENSE_OPTION>
```

### Environment variable

Accept the Chef License by setting an environment variable. For example:

```sh
export CHEF_LICENSE="<LICENSE_OPTION>"
chef-client OPTION VALUE
```

### Config file

You can accept the Chef License with the Chef Infra Client or Knife config files.

On a workstation, you can set this in the [`~/.chef/config.rb` or `~/.chef/knife.rb`](https://docs.chef.io/workstation/config_rb/) files, and on a node you can set this in the [`/etc/chef/client.rb file`](https://docs.chef.io/config_rb_client/).

```sh
chef_license "<LICENSE_OPTION>"
```

## Obtain a free or trial license

To obtain a free or trial license, follow these steps:

1. Go to the following page: [Evaluate Chef](https://www.chef.io/license-generation-free-trial).
1. Fill in the fields in the form.
1. Select the Licensing Type (**Free Tier** or **Trial**).
1. Click **Submit**.
1. Enter the license key at the Command Line Interface (CLI) prompt, as an argument, or as an environment variable to activate the license.

## Obtain a commercial license

To obtain a commercial license, follow these steps:

1. Contact [chef-sales@progress.com](mailto:chef-sales@progress.com) to initiate the purchasing process.
1. Specify your node count and duration needs during the consultation.
1. Upon purchase, a license key is provided.
1. Enter the license key at the CLI prompt, as an argument, or as an environment variable to activate the license.

## Provide the license key

You can provide the license key in different ways, depending on your setup:

- **Using a command-line argument:** Provide the license key with the argument `--chef-license-key`:

    ```sh
    --chef-license-key=<LICENSE_KEY>
    ```

- **Using an environment variable:** Set the `CHEF_LICENSE_KEY` environment variable to provide the license key:

    ```sh
    export CHEF_LICENSE_KEY=<LICENSE_KEY>
    ```

- **Using the interactive license dialog:** If a license is not provided in an argument or environment variable, an interactive dialog appears before execution, prompting you to either input a license key or generate one.

### Interactive license dialog

The easiest way to provide a license key to Chef Infra is to run Chef Infra.
Start a run and Infra will start an interactive licensing dialog
if a license key is not already set and it does not detect an automated method of setting the license key.

1. To start the interactive licensing dialog, start a run.

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

Chef Infra validates the license key, displays information about the license entitlements, and then executes the run.

Chef Infra stores license keys for future use and will not prompt you for the license key for the duration of your license.

## Specify a license server

Refer to the following points for details on specifying a license server:

- **Acceptance Environment License Server:** In environments connected to an acceptance license server, set the `CHEF_LICENSE_SERVER` environment variable along with the `CHEF_LICENSE_KEY`:

```sh
export CHEF_LICENSE_SERVER=<LICENSE_SERVER_URL>
```

- **Local License Server:** If you have a local license server, you only need to set the `CHEF_LICENSE_SERVER`. The `CHEF_LICENSE_KEY` is not required in this case:

```sh
export CHEF_LICENSE_SERVER=<LOCAL_LICENSE_SERVER_URL>
```

### Multiple license servers

You can set multiple Chef Local License Services, which provides resiliency and redundancy for managing licenses.

Enter up to five Chef Local License Service URLs as a comma-separated list. Chef Infra will try each URL and use the first one that works.

```bash
export CHEF_LICENSE_SERVER=https://license-server-01.example.com,https://license-server-02.example.com
```

This capability is basic and you must synchronize the license servers, otherwise you may get inconsistent results.

## Sample license keys

During testing, you will need sample license keys to enter into the CLI. Below are some keys you can use.

The URL for the acceptance environment is https://licensing-acceptance.chef.co/License, and for the production environment, it is https://services.chef.io/licensing.

| Type        | Key                                         | Validity Status | Notes                                    |
|-------------|---------------------------------------------|-----------------|------------------------------------------|
| commercial  | 5fd13cca-14b7-42b9-ad47-d52a0630c1ae       | Active          | License is entitled to both InSpec and Infra |
| commercial  | f5567204-f2d2-43b2-82a8-6359acfa3fb8       | Active          | License is entitled to Infra but not to InSpec. |
| commercial  | d0ad2bbb-707a-4ae6-b399-6ab8222e78b4       | Active          | License is entitled to InSpec but not Infra |
| commercial  | 9bc21f5f-e1c7-496f-8b97-c7aba9a3aaa8       | Expired         | License is entitled to both Infra and InSpec |
| trial       | tmns-0552c71e-ad20-4779-9bf3-19175a6a773d-9181 | Active          | License is entitled to both Infra and InSpec |
| trial       | tmns-6544d799-f03c-4060-9b16-8b731cab93ba-9098 | Expired         | License is entitled to both Infra and InSpec |
| free        | free-55eef3a8-2506-4b4c-927d-dd3c1245569d-872 | Active          | License is entitled to both Infra and InSpec |

## License keys for the production environment

| Type  | Key                                         | Validity Status | Notes                                                 |
|-------|---------------------------------------------|-----------------|-------------------------------------------------------|
| trial | tmns-3785e812-1704-4d08-836d-2f35bdfddce4-4914 | Expired         | License is entitled to both InSpec and Infra            |
| free  | free-833b40cf-336a-42ee-b71d-f14a078107b9-5090 | Active          | License is entitled to both InSpec and Infra            |
| trial | tmns-208db3d1-7588-4984-b1cc-ad47940f2f3d-3518 | Active          | License is entitled to both Infra and InSpec. (Expiration Date: 10th October, 2024) |
