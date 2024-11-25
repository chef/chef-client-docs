+++
title = "Using Test-Kitchen"
linkTitle = "Using Test-Kitchen"

[menu.kitchen]
title = "Using Test-Kitchen"
identifier = "kitchen/using_test_kitchen"
parent = "kitchen"
weight = 11
+++

The release of the Chef Infra 19 introduced a few licensing-related changes to the test-kitchen to ensure compatibility with Infra 19. Test-kitchen needs to comply with the licensing changes for chef-19, however, there is no benefit to the community and hence those changes are not pushed up to test-kitchen/test-kitchen. Instead, we forked chef/test-kitchen.

As part of the forking process, test kitchen has been re-branded to Chef Test Kitchen Enterprise, with the version commencing at 1.0.0. Additionally, the repository has been renamed to chef/chef-test-kitchen-enterprise. There are no changes to how we invoke test-kitchen; this update primarily focuses on branding modifications.

## Installation

The RC1 build of chef-test-kitchen-enterprise is primarily available as a Habitat package. The installation can be downloaded using the following command:

```sh
sudo hab pkg install --binlink --force chef/chef-test-kitchen-enterprise
```

The hab package is named `chef/chef-test-kitchen-enterprise`. By using the `--binlink` option, you can add the kitchen binary to your current path. Additionally, the `--force` flag allows you to overwrite any existing binaries.

To verify the success of the installation, run the following command:

```sh
kitchen version
```

## Supported drivers, provisioners, and verifier

For the RC1 release, only the kitchen-dokken plugin is supported. This allows us to leverage the Dokken driver to create platform containers and use the Dokken provisioner for configuring the Chef Infra Client 19 within those containers. By default, Dokken employs the `chef/chef-hab` Docker image to establish the Chef Infra Client 19 on the container through a Habitat-based methodology. The default verifier is InSpec 6.

### Sample kitchen.yml for Chef Infra Client 19

```sh
---
driver:
  name: dokken
  privileged: true

provisioner:
  name: dokken

transport:
  name: dokken

verifier:
  name: inspec

platforms:
  - name: ubuntu-20.04
  - name: centos-8

suites:
  - name: default
    run_list:
      - "cookbook"
    verifier:
      inspec_tests:
        - test/integration/default
```

### Using Chef Infra Client 18 or an older version

To provision containers using Chef Infra Client version 18 or earlier, you can modify the driver configuration in the `kitchen.yml` file. Set the `chef_image` configuration to `chef/chef` and specify the desired version in the `chef_version` configuration.

```sh
driver:
  name: dokken
  privileged: true
  chef_version: 18.3.0
  chef_image: "chef/chef"
```

## License usage in Test Kitchen

The Chef Infra Client 19 and InSpec 6 both require a valid license for operation. Given their direct dependency on the test-kitchen, we have enhanced the test-kitchen to prompt users for a license, activate it, and securely store it on disk. Additionally, the license is transmitted to the provisioned Virtual Machine (VM), allowing Chef Infra Client to function effectively during the verification phase alongside InSpec 6. The following sections provide further details on this process.

### Which license is needed?

As Test Kitchen is part of the Chef workstation suite, any license with the Chef workstation entitlement can be used with Test-Kitchen. You must obtain a free, trial, or commercial license that has a workstation entitlement enabled to use the Test Kitchen seamlessly. Chef Infra and Chef compliance come with a bundled workstation entitlement enabled.

### What are the licensing changes?

Unlike other products like Chef Infra Client, InSpec, and Workstation, Test Kitchen does not enforce licensing. The main use of a license in  Test Kitchen is to ensure a valid license is available to execute tests.

You can pass the `license_key` from Test Kitchen to the provisioned VM to install and execute Chef Infra 19. Additionally, this license will be used by InSpec 6 during the verification phase.

### How to use the Chef Workstation license in Test Kitchen

The Chef Workstation license can be used in Test Kitchen in the following ways:

- Set the ENV variable.
- Pass the chef-license through the kitchen.yml file.
- Use the stored license on the disk.

#### Set the ENV variable

You can configure the license key directly in the same shell that initiates Test Kitchen. The licensing library used by Test Kitchen will automatically read this license and apply it during execution. You can use the following command to set the ENV variable:

```sh
export CHEF_LICENSE_KEY="free-e2deddad-837a-445e-8529-************-1698"
```

#### Pass through the kitchen.yml file

You can include the license in the kitchen.yml file, which serves as a configuration file outlining the procedures for Test Kitchen to execute automated tests on the code. The installation of the Chef Infra Client is managed by the Kitchen provisioner, and thus it should be appropriately configured within the provisioner settings.

```sh
provisioner:
  name: chef_infra
  product_name: chef
  chef_license: accept-no-persist
  chef_license_key: free-e2deddad-837a-445e-8529-************-1698
```

Here the `chef_license` is the End User License Agreement (EULA) license acceptance and `chef_license_key` sets the license key.

#### Use the stored license on the disk

If a license is already activated with any other products such as Chef Infra Client, Chef Workstation, or Chef InSpec, Test Kitchen can automatically read it and use it during the provisioning and verifying steps. The stored license will be saved on the `~/.chef/licenses.yml` file which will look similar to the following:

```sh
---
:file_format_version: 4.0.0
:licenses:
- :license_key: free-e2deddad-837a-445e-8529-************-1698
  :license_type: :free
  :update_time: '2024-10-23T15:02:53+05:30'
:license_server_url: https://services.chef.io/licensing
```

### How to store the license on the disk with Test Kitchen

Test Kitchen also comes with in-house license commands that can be used to interactively get a license, validate it, and persist it on the disk. The details of the commands are as follows:

`kitchen license`
: It checks if there is already a license on the disk, verifies it with the licensing server, and prints it on the stdout. If not, it asks you to activate one.

![License details](/images/chef-client/kitchen/license_details.png)

`kitchen license list`
: This command lists the details of all licenses already stored on the disk.

![License list](/images/chef-client/kitchen/license_list.png)

`kitchen license add`
: You can use this command to activate more licenses.

### How Test Kitchen uses the license

During the converge phase, the local license is transferred to the Virtual Machine (VM) and provided as an argument to the Chef Infra Client, allowing the execution to proceed into the Infra phase. Additionally, the Chef Infra Client validates the license received from the Kitchen and save it on the provisioned VM for future use.

During the verification phase, the license gets transmitted to InSpec through the kitchen-inspec plugin and it will be used for license validation on the InSpec side.

## Habitat-based changes

The Chef Infra Client 19 will be accessible through Habitat instead of the public Omnitruck APIs. As a result of this, the provisioner was updated to facilitate the installation of the Habitat-based Chef Infra Client on provisioned VMs.

Expeditor in the chef/chef GitHub repo creates the Omnibus images for chef/chef on Docker hub. The Habitat-based Chef images are only created by the same pipeline on chef-19 branches and pushed out to a new repo (chef/chef-hab) on Docker hub.

The OS containers on Docker hub at dokken/linux_flavor_os will still be published at the same location.
