+++
title = "Getting Started in a Production Environment"
linkTitle = "Getting Started in a Production Environment"

[menu.get_started]
title = "Getting Started in a Production Environment"
identifier = "get_started/production"
parent = "get_started"
weight = 11
+++

The usage instructions are identical across all operating systems, with the only difference being the method for setting environment variables. The `CHEF_LICENSE_SERVER` environment variable is only required for accessing the acceptance environment of the licensing server.

To get started in a production environment, follow these steps:

1. Run the chef-client in local-mode using the `--why-run` flag, which is a type of Chef Infra Client run on your local that does everything except modify the system.
1. Accept the EULA if prompted, which typically occurs during the first run of Chef products:

    ```sh
    chef-client --local-mode --why-run
    ```

    Chef Infra looks for valid licenses on your system and at the initial run (because a license is unavailable), it prompts you to enter a license key:

    ![Enter a license key](/images/chef-client/get_started/enter-license-key.png)

1. Select `I already have a license ID` and enter one of the license keys from the **License Keys for the Production Environment** table int he following section: [How to Apply a License]({{< relref "how_to_apply_a_license" >}}). Because an environment variable has not been set to use the acceptance environment of the license server, communication defaults to the production environment.

    ![License validated successfully](/images/chef-client/get_started/license-validated-successfully.png)

1. After entering one of the license keys, the run should proceed and complete successfully.

    ![License details](/images/chef-client/get_started/license-details.png)

## License generation

To generate a license, follow these steps:

1. Select `I don't have a license ID and would like to generate a new license ID`.

    ![Generate a new license ID](/images/chef-client/get_started/generate-a-new-license-id.png)

1. Select the desired license type and follow the link provided on the screen to generate your license by completing the form. You will receive the license in an email.

    ![Registration link](/images/chef-client/get_started/registration-link.png)

1. Select `Validate license now` and enter the license ID you received in the email. After that, the run should proceed and complete successfully.

    ![Generated license validated successfully](/images/chef-client/get_started/generated-license-validated-successfully.png)
