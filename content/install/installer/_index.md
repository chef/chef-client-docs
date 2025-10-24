+++
title = "Install Chef Infra Client RC3 with a native installer"
linkTitle = "Native installer"

[menu.install]
title = "Install"
identifier = "install/installer/install"
parent = "install/installer"
weight = 10
+++

The Chef Infra Client native installers provide an efficient way to install Chef Infra Client on Windows, Debian, or RPM-based Linux distributions.
You can download and install the pre-built `.msi`, `.deb`, or `.rpm` packages using your existing package management tools, simplifying the deployment process for managing system configurations.

## Supported platforms

This installation method is supported on Linux and Windows x86-64 systems.

## Prerequisites

This installation process has the following prerequisites:

- Chef Workstation isn't installed on the target system.
- On Debian-based systems, the dpkg package manager is installed on the target system.
- On RPM-based systems, the RPM and either the DNF or Yum package managers are installed on the target system.

  For Amazon Linux 2, use the RPM and Yum package managers.

- You have a valid Progress Chef license key.
- The target system is connected to the internet.

## Install Chef Infra Client

To install Chef Infra Client 19, follow these steps:

1. Download the Chef Infra Client installer.

    {{< accordion-list data-allow-all-closed="true" >}}

    {{< accordion-item accordion-title="Download Debian-based installer" >}}

    For Debian-based distributions:

    - Using Wget:

      ```sh
      wget -O "chef-ice-19.2.rc3-linux.deb" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.deb?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=cmJmplCvrkVXK5MtqCmidrz3rds%3D&Expires=1776916085"
      ```

    - Using curl:

      ```sh
      curl -o "chef-ice-19.2.rc3-linux.deb" "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.deb?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=cmJmplCvrkVXK5MtqCmidrz3rds%3D&Expires=1776916085"
      ```

    {{< /accordion-item >}}
    {{< accordion-item accordion-title="Download RPM-based installer" >}}

    For RPM-based distributions:

    - Using Wget:

      ```sh
      wget -O chef-ice-19.2.rc3-linux.rpm "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.rpm?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=FUbFKD2qMux2TBK7ltNPLuExQGk%3D&Expires=1776916329"
      ```

    - Using curl:

      ```sh
      curl -o chef-ice-19.2.rc3-linux.rpm "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/linux/x86_64/chef-ice-19.2.rc3-linux.rpm?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=FUbFKD2qMux2TBK7ltNPLuExQGk%3D&Expires=1776916329"
      ```

    {{< /accordion-item >}}
    {{< accordion-item accordion-title="Download Windows installer" >}}

    For Windows:

    - using curl:

      ```sh
      curl -o chef-ice-19.2.rc3-windows.msi "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.msi?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=rmb4GgaxE6oPEfVHiAugsg7xMBI%3D&Expires=1776916373"
      ```

    - using PowerShell:

      ```ps1
      Invoke-WebRequest -Uri "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/chef-ice/19.2.RC3/windows/x86_64/chef-ice-19.2.rc3-windows.msi?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=rmb4GgaxE6oPEfVHiAugsg7xMBI%3D&Expires=1776916373" -OutFile "chef-ice-19.2.rc3-windows.msi"
      ```

    {{< /accordion-item >}}
    {{< /accordion-list >}}

1. Go to the directory with the installer and install the package.

   {{< accordion-list data-allow-all-closed="true" >}}

   {{< accordion-item accordion-title="Install on Debian-based distributions" >}}

   For Debian-based distributions:

   ```sh
   sudo -E dpkg -i chef-ice-19.2.rc3-linux.deb
   ```

   {{< /accordion-item >}}
   {{< accordion-item accordion-title="Install on RPM-based distributions" >}}

   For RPM-based distributions:

   ```sh
   sudo -E dnf install chef-ice-19.2.rc3-linux.rpm -y
   ```

   or:

   ```sh
   sudo -E rpm -ivh chef-ice-19.2.rc3-linux.rpm
   ```

   {{< /accordion-item >}}
   {{< accordion-item accordion-title="Install on Windows" >}}

   Install on Windows:

   - Double-click on the MSI package and install using Windows Package Manager.

   or:

   - Using Powershell:

     ```sh
     msiexec /i "chef-ice-19.2.rc3-windows.msi"
     ```

   {{< /accordion-item >}}
   {{< /accordion-list >}}

1. Verify the installation:

    ```sh
    chef-client --version
    ```

## Next steps

After installing Chef Infra Client, you can test it by running an [example cookbook](/cookbooks).
