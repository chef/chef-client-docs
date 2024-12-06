+++
title = "Apply a license in Chef Test Kitchen Enterprise"

[menu.kitchen]
title = "Add a license"
identifier = "kitchen/license"
parent = "kitchen"
weight = 30
+++

Chef Infra Client 19 and Chef InSpec 6 both require a valid license for operation.
Given their direct dependency on the Test Kitchen Enterprise, we've enhanced Test Kitchen Enterprise to prompt users for a license, activate it, and securely store it on disk.
Additionally, the license is transmitted to the provisioned VM, allowing the Chef Infra Client to function effectively during the verification phase alongside Chef InSpec 6.

The following sections provide further details on this process.

## Which license do I need?

As Test Kitchen Enterprise is part of the Chef Workstation suite, you can use any license that's entitled to run Chef Workstation with Test Kitchen Enterprise.
Obtain a free, trial, or commercial license which has Chef Workstation entitlement enabled to use the Test Kitchen Enterprise seamlessly.
Chef Workstation is bundled with Chef Infra Client and Chef compliance by default.

## How Test Kitchen Enterprise uses the license

Unlike other products like Chef Infra Client, Chef InSpec, and Chef Workstation, Test Kitchen Enterprise doesn't enforce licensing.
Test Kitchen Enterprise uses the license to execute tests.

During the converge phase, Test Kitchen Enterprise transfers the license to the virtual machine (VM) and adds it as an argument to Chef Infra Client, allowing the Infra Client run to proceed. Chef Infra Client validates the license received from Test Kitchen Enterprise and saves it on the provisioned VM for future use.

During the verification phase, the kitchen-inspec plugin transmits the license to Chef Inspec which validates it with Chef's licensing service.

## Set a license in Test Kitchen Enterprise

Test Kitchen Enterprise accepts any license that's entitled to use Chef Workstation.

You can set a license Test Kitchen Enterprise in the following four ways:

- Set the license key in an environment variable.
- Pass the license through the `kitchen.yml` file.
- Create and persist a license using the `test-kitchen` CLI.
- Use a pre-existing license stored on disk from an earlier Chef Infra Client or Chef Workstation installation.

### Add the license as an environment variable

You can configure the license key directly in the same shell that initiates Test Kitchen. The licensing library used by Test Kitchen automatically reads this license and applies it during execution.

- Set the license using an environment variable using `export`:

  ```sh
  export CHEF_LICENSE_KEY="<LICENSE_KEY>"
  ```

### Pass the license through the `kitchen.yml` file

You can include the license in the `kitchen.yml` file, which serves as a configuration file outlining the procedures for Test Kitchen to execute automated tests on the code.
The Chef Infra Client installation is managed by the Kitchen provisioner, so it should be appropriately configured within the provisioner settings.

- Define the license key in the `kitchen.yml` file:

  ```yaml
  provisioner:
    name: chef_infra
    product_name: chef
    chef_license: accept-no-persist
    chef_license_key: <LICENSE_KEY>
  ```

  Note: `chef_license` defines the acceptance of the [End User License Agreement](https://docs.chef.io/licensing/accept/#chef-workstation).

### Add the license using the `test-kitchen` CLI

Follow these instructions to add a license using the `test-kitchen` CLI:

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

    Test Kitchen Enterprise obtains the license, then validates and persists it on the disk.

1. Optional: Verify a valid license is saved on disk.

    The following command verifies that a license is saved on disk, verifies it with the licensing server, and prints licensing details to the standard output.
    If there isn't a valid license, it will ask you to activate one.

    ```sh
    kitchen license
    ```

    The following command returns the details of all licenses stored on disk.

    ```sh
    kitchen license list
    ```

### Use a pre-existing license

If you already have a license activated with any other products---such as Chef Infra Client, Chef Workstation, or Chef InSpec---Test Kitchen Enterprise automatically reads and uses it during the provisioning and verifying steps.

Licenses are saved in the `~/.chef/licenses.yml` file.
For example:

```yaml
---
:file_format_version: 4.0.0
:licenses:
- :license_key: <LICENSE_KEY>
  :license_type: :free
  :update_time: '2024-10-23T15:02:53+05:30'
:license_server_url: https://services.chef.io/licensing
```
