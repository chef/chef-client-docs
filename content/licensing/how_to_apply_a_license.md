+++
title = "How to Apply a License"
linkTitle = "How to Apply a License"

[menu.licensing]
title = "How to Apply a License"
identifier = "licensing/apply"
parent = "licensing"
weight = 11
+++

Details on how to obtain the different license types are provided in the following sections.

## Obrain a Free or Trial License

To obtain a free or trial license, follow these steps:

1. Go to the following page: [
Evaluate Chef](https://www.chef.io/license-generation-free-trial).
1. Fill in the fields in the form.
1. Select the Licensing Type (**Free Tier** or **Trial**).
1. Click **Submit**.
1. Enter the license key at the Command Line Interface (CLI) prompt, as an argument, or as an environment variable to activate the license.

## Obtain a Commercial License

To obtain a commercial license, follow these steps:

1. Contact [chef-sales@progress.com](mailto:chef-sales@progress.com) to initiate the purchasing process.
1. Specify your node count and duration needs during the consultation.
1. Upon purchase, a license key is provided.
1. Enter the license key at the CLI prompt, as an argument, or as an environment variable to activate the license.

## Provide the License Key

You can provide the license key in different ways, depending on your setup:

- **Using a command-line argument:** Provide the license key with the argument `--chef-license-key`:

```sh
--chef-license-key=<LICENSE_KEY>
```

- **Using an environment variable:** Set the `CHEF_LICENSE_KEY` environment variable to provide the license key:

```sh
export CHEF_LICENSE_KEY=<LICENSE_KEY>
```

## Specify a License Server

Refer to the following points for details on specifying a license server:

- **Acceptance Environment License Server:** In environments connected to an acceptance license server, set the `CHEF_LICENSE_SERVER` environment variable along with the `CHEF_LICENSE_KEY`:

```sh
export CHEF_LICENSE_SERVER=<LICENSE_SERVER_URL>
```

- **Local License Server:** If you have a local license server, you only need to set the `CHEF_LICENSE_SERVER`. The `CHEF_LICENSE_KEY` is not required in this case:

```sh
export CHEF_LICENSE_SERVER=<LOCAL_LICENSE_SERVER_URL>
```

## Sample License Keys

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

## License Keys for the Production Environment

| Type  | Key                                         | Validity Status | Notes                                                 |
|-------|---------------------------------------------|-----------------|-------------------------------------------------------|
| trial | tmns-3785e812-1704-4d08-836d-2f35bdfddce4-4914 | Expired         | License is entitled to both InSpec and Infra            |
| free  | free-833b40cf-336a-42ee-b71d-f14a078107b9-5090 | Active          | License is entitled to both InSpec and Infra            |
| trial | tmns-208db3d1-7588-4984-b1cc-ad47940f2f3d-3518 | Active          | License is entitled to both Infra and InSpec. (Expiration Date: 10th October, 2024) |
