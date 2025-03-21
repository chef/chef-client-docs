+++
title = "Chef Infra Client native installer troubleshooting"

[menu.install]
title = "Troubleshooting"
identifier = "install/installer/troubleshooting"
parent = "install/installer"
weight = 200
+++

## Conflicts with Chef Workstation

If the Chef Workstation is already on your system, the installation process fails with a conflict.

The installer returns the following error on Debian-based systems:

```sh
Selecting previously unselected package chef-infra-client.
dpkg: regarding chef-infra-client-19.1.rc2_amd64.deb containing chef-infra-client:
 chef-infra-client conflicts with chef-workstation
  chef-workstation (version 0.4.2-1) is present and installed.

dpkg: error processing archive chef-infra-client-19.1.rc2_amd64.deb (--install):
 conflicting packages - not installing chef-infra-client
Errors were encountered while processing:
 chef-infra-client-19.1.rc2_amd64.deb
```

The installer returns the following error on RPM-based systems:

```sh
Error:
 Problem: package chef-infra-client-19.0.54-1.amzn2023.x86_64 from @System conflicts with chef-workstation provided by chef-workstation-25.1.1074-1.amazon2023.x86_64 from @commandline
  - conflicting requests
  - problem with installed package chef-infra-client-19.0.54-1.amzn2023.x86_64
(try to add '--allowerasing' to command line to replace conflicting packages or '--skip-broken' to skip uninstallable packages)
```

To resolve the error:

1. [Uninstall Chef Workstation](https://docs.chef.io/workstation/install_workstation/#uninstalling).
1. [Reinstall Chef Infra Client]({{< relref "install" >}}).


## Error: invalid license

The installation process requires a valid Progress Chef License key.

The installer returns the following error if you don't add a valid license:

```sh
Validating chef-client license with https://services.chef.io
Invalid License Key: ssfree-833b40cf-336a-42ee-b71d-f14a0
chef-client installation failed. Error: invalid license
warning: %post(chef-infra-client-19.1.0-1.amzn2.x86_64) scriptlet failed, exit status 1

Error in POSTIN scriptlet in rpm package chef-infra-client
  Verifying        : chef-infra-client-19.1.0-1.amzn2.x86_64
```

To resolve this error:

1. Add a valid Progress Chef License key to your machine's environment:

    ```sh
    export CHEF_LICENSE_KEY=<LICENSE_KEY>
    ```

1. Install Chef Infra Client.

    On Debian-based distributions:

    ```sh
    sudo -E dpkg -i chef-infra-client-19.1.rc2_amd64.deb
    ```

    On RPM-based distributions, use the `dnf reinstall` command:

    ```sh
    sudo -E dnf reinstall chef-infra-client-19.1.rc2.amzn2.x86_64.rpm
    ```
