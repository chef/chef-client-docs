+++
title = "Getting Started in an Acceptance Environment"
linkTitle = "Getting Started in a Acceptance Environment"

[menu.get_started]
title = "Getting Started in a Acceptance Environment"
identifier = "get_started/acceptance"
parent = "get_started"
weight = 12
+++

The experience of using Chef Infra with the acceptance environment is identical to that of the production environment, with only one additional step required before executing the commands.

To avoid potential conflicts, consider removing the license file before switching to the acceptance environment.

To delete the license file, use the following commands:

- **macOS or Linux:**

    ```sh
    rm /Users/<YourUsername>/.chef/licenses.yaml
    ```

- **Windows (Command Prompt):**

    ```sh
    del C:\Users\<YourUsername>\.chef\licenses.yaml
    ```

- **Windows (PowerShell):**

    ```sh
    Remove-Item C:\Users\<YourUsername>\.chef\licenses.yaml
    ```

To set the license server URL for the acceptance environment, use the following commands for your operating system:

- **macOS or Linux:** Open your terminal and run:

    ```sh
    export CHEF_LICENSE_SERVER=https://licensing-acceptance.chef.co/License
    ```

- **Windows (Command Prompt):** Open the Command Prompt and run:

    ```sh
    set CHEF_LICENSE_SERVER=https://licensing-acceptance.chef.co/License
    ```

- **Windows (PowerShell):** Open PowerShell and run:

    ```sh
    $env:CHEF_LICENSE_SERVER="https://licensing-acceptance.chef.co/License"
    ```

This sets the `CHEF_LICENSE_SERVER` environment variable to direct it to the acceptance environment of the licensing server.

You can proceed to use Chef Infra with one of the license keys provided in the [License Keys for the Acceptance Environment]({{< relref "how_to_apply_a_license/#license-keys-for-the-acceptance-environment" >}}) section.
