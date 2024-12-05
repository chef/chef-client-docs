+++
title = "Apply a license in Chef Test Kitchen Enterprise"

[menu.kitchen]
title = "License"
identifier = "kitchen/license"
parent = "kitchen"
weight = 30
+++

Chef Infra Client 19 and Chef InSpec 6 both require a valid license for operation.
Given their direct dependency on the Test Kitchen Enterprise, we've enhanced Test Kitchen Enterprise to prompt users for a license, activate it, and securely store it on disk.
Additionally, the license is transmitted to the provisioned VM, allowing the Chef Infra Client to function effectively during the verification phase alongside InSpec 6.

The following sections provide further details on this process.

## How Test Kitchen Enterprise uses the license

During the converge phase, the local license is transferred to the virtual machine (VM) and provided as an argument to the Chef Infra Client, allowing the execution to proceed into the infra phase.
Additionally, the Chef Infra Client validates the license received from Test Kitchen Enterprise and saves it on the provisioned VM for future use.

During the verification phase, the license is transmitted to Chef Inspec through the kitchen-inspec plugin and is used for the license validation on the Chef Inspec side.

## Which license is needed?

As Test-Kitchen is part of the Chef Workstation suite, any license with the Chef Workstation entitlement can be used with Test-Kitchen.
Users will need to obtain a free, trial, or commercial license which has Chef Workstation entitlement enabled to use the Test Kitchen Enterprise seamlessly. Chef Infra Client and Chef compliance comes with bundled Chef Workstation by default.

## What are the licensing changes?

Unlike other products like Chef Infra Client, Chef InSpec, and Chef Workstation, Test-Kitchen doesn’t enforce licensing.
The main use of a license in the Test Kitchen is to ensure a valid license is available to execute tests.

The user can pass a license key from Test Kitchen Enterprise to the provisioned VM to install and execute Chef Infra Client 19.
Additionally, this license is used by Chef Inspec 6 during the verification phase.

## Pass a license to Test Kitchen Enterprise

A license that's entitled to use Chef Workstation can be used in the Test Kitchen Enterprise in four different ways:

- Setting an environment variable.
- Passing the Chef license through the `kitchen.yml` file.
- Creating and persisting a license using the `test-kitchen` CLI
- Using a pre-existing license stored on the disk from an earlier Chef Infra Client or Chef Workstation installation.

### Add the license as an environment variable

You can configure the license key directly in the same shell that initiates Test Kitchen. The licensing library used by Test Kitchen automatically reads this license and applies it during execution.

- Set the license using an environment variable using `export`:

  ```sh
  export CHEF_LICENSE_KEY="<LICENSE_KEY>"
  ```

### Pass the license through the `kitchen.yml` file

You can includee the license in the `kitchen.yml` file, which serves as a configuration file outlining the procedures for Test Kitchen to execute automated tests on the code.
The Chef Infra Client installation is managed by the Kitchen provisioner, so it should be appropriately configured within the provisioner settings.

```yaml
provisioner:
  name: chef_infra
  product_name: chef
  chef_license: accept-no-persist
  chef_license_key: <LICENSE_KEY>
```

### Add the license using the `test-kitchen` CLI




1. You can add a license using the `test-kitchen` CLI:

    ```sh
    sudo kitchen license
    ```

1. At the first prompt, select **I already have a license ID**

    ```text
    sudo kitchen license
    ------------------------------------------------------------
      License ID Validation

      To continue using Chef InSpec, a license ID is required.
      (Free, Trial, or Commercial)

      If you generated a license previously, you might
      have received it in an email.

      If you are a commercial user, you can also find it in the
      supportlink.chef.io portal.
    ------------------------------------------------------------

    Please choose one of the options below (Press ↑/↓ arrow to move and Enter to select)
    ‣ I already have a license ID
      I don't have a license ID and would like to generate a new license ID
      Skip
    ```

1. Enter your license key at the second prompt.

    ```text
    Please choose one of the options below I already have a license ID
    Please enter your license ID:  <LICENSE_KEY>
    ✔ [Success] License validated successfully.
    ------------------------------------------------------------
    License Details
      Asset Name       : Workstation
      License ID       : <LICENSE_KEY>
      Type             : Free Tier
      Status           : Active
      Validity         : Unlimited
      No. Of Units     : 10 Nodes
    ------------------------------------------------------------
    ```

    Test-kitchen obtains the license, then validates and persists it on the disk.

### Use a pre-existing license

If the user already has a license activated with any other products such as chef-infra-client, chef-workstation, or InSpec, test-kitchen can automatically read it and use it during the provisioning and verifying steps. The stored license will be saved on the `~/.chef/licenses.yml` file. For example:

```yaml
---
:file_format_version: 4.0.0
:licenses:
- :license_key: <LICENSE_KEY>
  :license_type: :free
  :update_time: '2024-10-23T15:02:53+05:30'
:license_server_url: https://services.chef.io/licensing
```

