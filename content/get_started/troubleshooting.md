+++
title = "Troubleshooting"
linkTitle = "Troubleshooting"

[menu.get_started]
title = "Troubleshooting"
identifier = "get_started/troubleshooting"
parent = "get_started"
weight = 13
+++

If you initially chose to use the production environment but later decide to explore the acceptance environment, the license keys from the production environment will still be on your system. To avoid potential conflicts, consider removing the license file before switching to the acceptance environment.

The `licenses.yaml` exists in the following locations based on your operating system:

- **macOS or Unix system:** On macOS or Unix systems, the `licenses.yaml` file is located here:

    ```sh
    /Users/<YourUsername>/.chef/
    ```

    Replace \<YourUsername\> with your actual username.

- **Windows Systems:** On Windows systems, the `licenses.yaml` file is typically located at:

    ```sh
    C:\Users\<YourUsername>\.chef\
    ```

    Replace \<YourUsername\> with your actual Windows username.

To delete the license file, use the following commands:

- **macOS or Linux:**

    ```sh
    rm /Users/sosaha/.chef/licenses.yaml
    ```

- **Windows (Command Prompt):**

    ```sh
    del C:\Users\<YourUsername>\.chef\licenses.yaml
    ```

- **Windows (PowerShell):**

    ```sh
    Remove-Item C:\Users\<YourUsername>\.chef\licenses.yaml
    ```

You can remove your `licenses.yaml` file to clear any existing licenses on your system.

## Check if the license server URL for acceptance is set

You can verify if the `CHEF_LICENSE_SERVER` environment variable is set by running the following command:

- **macOS or Linux:**

    ```sh
    echo $CHEF_LICENSE_SERVER
    ```

- **Windows (Command Prompt):**

    ```sh
    echo %CHEF_LICENSE_SERVER%
    ```

- **Windows (PowerShell):**

    ```sh
    $env:CHEF_LICENSE_SERVER
    ```

## Unset the license server URL

If you need to unset the `CHEF_LICENSE_SERVER`, you can use the following commands:

- **macOS or Linux:**

    ```sh
    unset CHEF_LICENSE_SERVER
    ```

- **Windows (Command Prompt):**

    ```sh
    set CHEF_LICENSE_SERVER=
    ```

- **Windows (PowerShell):**

    ```sh
    Remove-Item Env:CHEF_LICENSE_SERVER
    ```
