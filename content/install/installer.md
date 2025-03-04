+++
title = "Install Chef Infra Client RC2 using a native installer"
linkTitle = "Download and install"

[menu.install]
title = "Native installer"
identifier = "install/native"
parent = "install"
weight = 20

+++

The Chef Infra Client Native Installers provide a seamless way to install the Chef Infra Client and ensure compatibility with Debian and RPM-based distributions. Users can download and install the pre-built .deb or .rpm package using their existing RPM or DEB-based installation workflows, simplifying the deployment process for managing system configurations. The current native installers are supported on x86_64-based Linux installations.

## Prerequisites

Before installing the package, ensure your system meets the following requirements:

1. **Supported operating system and package manager**
  - To install the `Debian-based` distributions such as Ubuntu, use the following command:
    ```shell
    sudo apt update && sudo apt install dpkg
    ```
  - Verify if `dpkg` is installed:
    ```shell
    dpkg --version
    ```
  - To install `RPM-based` distributions such as Red Hat Enterprise Linux (RHEL), CentOS, or Fedora, use the following command:
    ```shell
    sudo yum install rpm
    ```
  - Verify if `rpm` is installed:
    ```shell
    rpm --version
    ```

2. **License key**
  - Ensure you have a valid license key for the Chef Infra Client.
  - Export the license key as an environment variable:
    ```shell
    export LICENSE_KEY="<your-license-key>"
    ```

3. **Internet access**
  - Ensure your system can access external URLs for validation and any required dependencies.

## Downloading the Installer

To get the latest version of the Chef Infra Client Installer, use the following command:

- Depending on the distribution, use wget or curl to download the desired installer.

  Example:

  - For `Debian-based` distributions such as Ubuntu.
  ```shell
  wget <https://example.com/chef-infra-client_<version>-<release>_<architecture>.deb
  ```
  or
  ```shell
  curl -LO <https://example.com/chef-infra-client_<version>-<release>_<architecture>.deb
  ```

  - For `RPM-based` distributions such as Red Hat Enterprise Linux (RHEL), CentOS, or Fedora.
  ```shell
  wget <https://example.com/chef-infra-client-<version>-<release>.<os-distribution>.<architecture>.rpm
  ```
  or
  ```shell
  curl -LO <https://example.com/chef-infra-client-<version>-<release>.<os-distribution>.<architecture>.rpm
  ```

## Installation steps

To install the package, follow these steps:

1. **Navigate to the directory with the installer**
  ```shell
  cd /path/to/downloaded/installer
  ```

2. **Install the package**
  - For `Debian-based` distributions such as Ubuntu.
    ```shell
    sudo -E dpkg -i chef-infra-client_<version>-<release>_<architecture>.deb
    ```
  - For `RPM-based` distributions such as Red Hat Enterprise Linux (RHEL), CentOS, or Fedora.
    ```shell
    sudo -E dnf install chef-infra-client-<version>-<release>.<os-distribution>.<architecture>.rpm -y
    ```

3. **Verify the installation**
  - Verify the installed version:
    ```shell
    chef-client --version
    ```

## Installation scenarios

### Installation of Chef Infra Client DEB

#### 1. Fresh Install

When no existing Chef Infra Client is detected, the installer performs a fresh setup. It uses the `--fresh_install` flag to install and configure Chef automatically.

```shell
Selecting previously unselected package chef-infra-client.
(Reading database ... 168881 files and directories currently installed.)
Preparing to unpack chef-infra-client-19.0.54-1_amd64.deb ...
Unpacking chef-infra-client (19.0.54) ...
Setting up chef-infra-client (19.0.54) ...
Postinstall: Detected fresh installation.
Running post-install tasks...
Executing: /hab/migration/bin/chef-migrate apply airgap --fresh_install /hab/migration/bundle/chef-chef-infra-client-19.0.54-20241121145703.tar.gz
Extracting package tar to ... /hab
Extracting package tar to /hab... completed
Starting chef-client installation and configuration...
Completed chef-client installation and configuration.
chef-client migration completed successfully!

To activate your Chef license, please set the following environment variable in your shell profile or current session:

    export CHEF_LICENSE_KEY=

Instructions:
1. For Current Session: Run the above command directly in your terminal. This will activate the license for the current session only.
2. For Persistent Activation: Add the command to your shell profile file (e.g., ~/.bashrc, ~/.zshrc, or ~/.profile). 
   After saving the file, reload the configuration using:
         source ~/.bashrc   # For bash users
         source ~/.zshrc    # For zsh users

For further assistance, visit <https://docs.chef.io/licensing/>.
```

#### 2. Migration from older Chef Client

If a previous version of Chef Infra Client is detected, the installer upgrades or migrates your existing installation. It omits the --fresh_install flag and applies the new version through chef-migrate.

```shell
Selecting previously unselected package chef-infra-client.
(Reading database ... 168881 files and directories currently installed.)
Preparing to unpack chef-infra-client-19.0.54-1_amd64.deb ...
Unpacking chef-infra-client (19.0.54) ...
Setting up chef-infra-client (19.0.54) ...
Postinstall: Detected upgrade installation.
Running post-install tasks...
Executing: /hab/migration/bin/chef-migrate apply airgap  /hab/migration/bundle/chef-chef-infra-client-19.0.54-20241121145703.tar.gz 
Validating provided flag values...
Validating chef-client license with <https://services.chef.io>
chef-client license validation completed successfully
Validating provided flag values... completed successfully
Processing provided flag values...
Deleting Omnibus chef-client...
Omnibus chef-client successfully deleted.
Processing provided flag values... completed successfully
Extracting package tar to ... /hab
Extracting package tar to /hab... completed
Starting chef-client installation and configuration...
Completed chef-client installation and configuration.
chef-client installtion completed successfully!

To activate your Chef license, please set the following environment variable in your shell profile or current session:

    export CHEF_LICENSE_KEY=

Instructions:
1. For Current Session: Run the above command directly in your terminal. This will activate the license for the current session only.
2. For Persistent Activation: Add the command to your shell profile file (e.g., ~/.bashrc, ~/.zshrc, or ~/.profile). 
   After saving the file, reload the configuration using:
         source ~/.bashrc   # For bash users
         source ~/.zshrc    # For zsh users

For further assistance, visit <https://docs.chef.io/licensing/>.
```

#### 3. Conflict When Chef Workstation Is Installed

If the Chef Workstation is already on your system, the installation process fails with a conflict. You must remove the Chef Workstation before installing the Chef Infra Client.

```shell
Selecting previously unselected package chef-infra-client.
dpkg: regarding chef-infra-client-19.0.54-1_amd64.deb containing chef-infra-client:
 chef-infra-client conflicts with chef-workstation
  chef-workstation (version 0.4.2-1) is present and installed.

dpkg: error processing archive chef-infra-client-19.0.54-1_amd64.deb (--install):
 conflicting packages - not installing chef-infra-client
Errors were encountered while processing:
 chef-infra-client-19.0.54-1_amd64.deb
```

If errors occur during the installation, review the error messages and ensure the prerequisites are met.

### Installation of Chef Infra Client RPM

An RPM can be installed using the `DNF` tool. Below is a sample command to install a Chef Infra RPM:

```shell
sudo -E dnf install chef-infra-client-19.0.54-1.amzn2023.x86_64.rpm -y
```

#### 1. Conflicts with Omnibus-based Chef Workstation

The installation will fail if the Omnibus-based Chef Workstation is already installed, resulting in a conflict. You will see a console log similar to the one below:

```shell
Error:
 Problem: package chef-infra-client-19.0.54-1.amzn2023.x86_64 from @System conflicts with chef-workstation provided by chef-workstation-25.1.1074-1.amazon2023.x86_64 from @commandline
  - conflicting requests
  - problem with installed package chef-infra-client-19.0.54-1.amzn2023.x86_64
(try to add '--allowerasing' to command line to replace conflicting packages or '--skip-broken' to skip uninstallable packages)
```

#### 2. Migration from Omnibus-based Chef to Habitat-based Chef Infra Client

The existing Omnibus-based Chef Infra Client will be migrated to the new Habitat-based Chef Client. You can view the logs as shown below:

```shell
Last metadata expiration check: 2:48:04 ago on Mon Jan 27 06:27:55 2025.
Dependencies resolved.
=====================================================================================================================================================================================================================
 Package                                                Architecture                                Version                                                  Repository                                         Size
=====================================================================================================================================================================================================================
Installing:
 chef-infra-client                                      x86_64                                      19.0.54-1.amzn2023                                       @commandline                                      198 M

Transaction Summary
=====================================================================================================================================================================================================================
Install  1 Package

Total size: 198 M
Installed size: 211 M
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                             1/1
  Installing       : chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1
  Running scriptlet: chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1
Validating provided flag values...
Validating chef-client license with https://services.chef.io
chef-client license validation completed successfully
Validating provided flag values... completed successfully
Processing provided flag values...
Deleting Omnibus chef-client...
Omnibus chef-client successfully deleted.
Processing provided flag values... completed successfully
Extracting package tar to ... /hab
Extracting package tar to /hab... completed
Starting chef-client installation and configuration...
Completed chef-client installation and configuration.
chef-client installtion completed successfully!

========================================================================================================================
To activate your Chef license, please set the following environment variable in your shell profile or current session:

  export CHEF_LICENSE_KEY=xxxx

Instructions:
1. For Current Session: Run the above command directly in your terminal. This will activate the license for the current session only.
2. For Persistent Activation: Add the command to your shell profile file (e.g., ~/.bashrc, ~/.zshrc, or ~/.profile).
   After saving the file, reload the configuration using:
     source ~/.bashrc   # For bash users
     source ~/.zshrc    # For zsh users

For further assistance, visit https://docs.chef.io/licensing/.
========================================================================================================================

  Verifying        : chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1

Installed:
  chef-infra-client-19.0.54-1.amzn2023.x86_64

Complete!
```

#### 3. Fresh Installation of Habitat-based Chef to Chef Infra Client

A fresh Habitat-based Chef Client will be installed. You can view the logs below:

```shell
Last metadata expiration check: 2:49:33 ago on Mon Jan 27 06:27:55 2025.
Dependencies resolved.
=====================================================================================================================================================================================================================
 Package                                                Architecture                                Version                                                  Repository                                         Size
=====================================================================================================================================================================================================================
Installing:
 chef-infra-client                                      x86_64                                      19.0.54-1.amzn2023                                       @commandline                                      198 M

Transaction Summary
=====================================================================================================================================================================================================================
Install  1 Package

Total size: 198 M
Installed size: 211 M
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                             1/1
  Installing       : chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1
  Running scriptlet: chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1
Extracting package tar to ... /hab
Extracting package tar to /hab... completed
Starting chef-client installation and configuration...
Completed chef-client installation and configuration.
chef-client migration completed successfully!

========================================================================================================================
To activate your Chef license, please set the following environment variable in your shell profile or current session:

  export CHEF_LICENSE_KEY=

Instructions:
1. For Current Session: Run the above command directly in your terminal. This will activate the license for the current session only.
2. For Persistent Activation: Add the command to your shell profile file (e.g., ~/.bashrc, ~/.zshrc, or ~/.profile).
   After saving the file, reload the configuration using:
     source ~/.bashrc   # For bash users
     source ~/.zshrc    # For zsh users

For further assistance, visit https://docs.chef.io/licensing/.
========================================================================================================================

  Verifying        : chef-infra-client-19.0.54-1.amzn2023.x86_64                                                                                                                                                 1/1

Installed:
  chef-infra-client-19.0.54-1.amzn2023.x86_64

Complete!
```
