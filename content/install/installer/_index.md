+++
title = "Install Chef Infra Client RC2 using a native installer"
linkTitle = "Native installer"

[menu.install]
title = "Install"
identifier = "install/installer/install"
parent = "install/installer"
weight = 10
+++

The Chef Infra Client native installers provide an efficient way to install the Chef Infra Client on both Debian and RPM-based distributions.
Users can download and install the pre-built `.deb` or `.rpm` packages using their existing package management tools, simplifying the deployment process for managing system configurations.

## Supported platforms

Chef Infra Client 19 RC2 is supported on Linux x86-64 systems.

## Prerequisites

This install process has the following prerequisites:

- Chef Workstation _isn't_ installed on the target system.
- On Debian-based systems, the dpkg package manager is installed on the target system.
- On RPM-based systems, the RPM and either the DNF or Yum package managers are installed on the target system.

  For Amazon Linux 2, use the RPM and Yum package managers.

- You have a valid Progress Chef License key.
- The target system is connected to the internet.

## Install Chef Infra Client

To install Chef Infra Client 19, follow these steps:

1. Add your Progress Chef License key to your machine's environment:

    ```sh
    export CHEF_LICENSE_KEY=<LICENSE_KEY>
    ```

    Replace `<LICENSE_KEY>` with your Progress Chef License key.

1. Download the Chef Infra Client installer.

    {{< accordion-list data-allow-all-closed="true" >}}

    {{< accordion-item accordion-title="Download Debian-based installer" >}}

    For Debian-based distributions:

    - Using Wget:

      ```sh
      wget -O "chef-infra-client-19.1.rc2_amd64.deb" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_installer_folder/chef-infra-client-19.1.rc2_amd64.deb?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=juoMKNP%2BAnq6cV61c%2BIrj2OIhFI%3D&Expires=1756222738"
      ```

    - Using curl:

      ```sh
      curl -o "chef-infra-client-19.1.rc2_amd64.deb" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_installer_folder/chef-infra-client-19.1.rc2_amd64.deb?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=juoMKNP%2BAnq6cV61c%2BIrj2OIhFI%3D&Expires=1756222738"
      ```

    {{< /accordion-item >}}
    {{< accordion-item accordion-title="Download RPM-based installer" >}}

    For RPM-based distributions:

    - Using Wget:

      ```sh
      wget -O chef-infra-client-19.1.rc2.amzn2.x86_64.rpm "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_installer_folder/chef-infra-client-19.1.rc2.amzn2.x86_64.rpm?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=YNL2rOEpPflwG4PPyvIcofHBZ%2Fc%3D&Expires=1756222794"
      ```

    - Using curl:

      ```sh
      curl -o chef-infra-client-19.1.rc2.amzn2.x86_64.rpm "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/rc2_hab_pkg_chef_client/rc2_installer_folder/chef-infra-client-19.1.rc2.amzn2.x86_64.rpm?AWSAccessKeyId=AKIAW4FPVFT6BIP2EQW7&Signature=YNL2rOEpPflwG4PPyvIcofHBZ%2Fc%3D&Expires=1756222794"
      ```

    {{< /accordion-item >}}
    {{< /accordion-list >}}

1. Navigate to the directory with the installer

    ```sh
    cd /path/to/downloaded/installer
    ```

1. Install the package.

   {{< accordion-list data-allow-all-closed="true" >}}

   {{< accordion-item accordion-title="Install on Debian-based distributions" >}}

   For Debian-based distributions:

   ```sh
   sudo -E dpkg -i chef-infra-client-19.1.rc2_amd64.deb
   ```

   {{< /accordion-item >}}
   {{< accordion-item accordion-title="Install on RPM-based distributions" >}}

   For RPM-based distributions:

   ```sh
   sudo -E dnf install chef-infra-client-19.1.rc2.amzn2.x86_64.rpm -y
   ```

   or:

   ```sh
   sudo -E rpm -ivh chef-infra-client-19.1.rc2.amzn2.x86_64.rpm
   ```

   {{< /accordion-item >}}
   {{< /accordion-list >}}

1. Verify the installation:

    ```sh
    chef-client --version
    ```

## Next step

After installing Chef Infra Client, you can test it by running an [example cookbook](/cookbooks).
