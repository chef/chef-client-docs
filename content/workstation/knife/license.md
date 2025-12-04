+++
title = "Apply a license in Knife 19"

[menu.workstation]
title = "License Knife"
identifier = "workstation/knife/license"
parent = "workstation/knife"
weight = 30
+++

Depending on the version of Chef Infra Client that you're installing, Knife 19 bootstrap operations may require a valid Progress Chef license:

- Chef Infra Client 18 and earlier requires a license for all bootstrap operations because they use the standard download APIs.
- Chef Infra Client 19 RC3 doesn't require a license because it's distributed from pre-signed URLs.

<!---

**Chef Infra Client 19 GA:**
- A license will be required for all bootstrap operations unless you use custom installation scripts that bypass the Progress download infrastructure

--->

During bootstrap operations, Knife transfers the license to the target node and adds it as an argument to Chef Infra Client.
Chef Infra Client validates the license received from Knife and saves it on the provisioned node for future use.

## Which license do I need?

If you're installing Chef Infra Client 18 and earlier, you need a license that includes Chef Workstation entitlement.

Knife 19 is part of the Chef Workstation suite, so you can use any license that includes Chef Workstation entitlement.
You can obtain a free, trial, or commercial license with Chef Workstation enabled.
Chef Workstation is bundled with Chef Infra Client and Chef compliance by default.

To get a license, visit the [Progress Chef community portal](https://community.progress.com/s/products/chef).

For more information, see the [Chef licensing documentation](https://docs.chef.io/licensing/).

## Set a license

You can set a license in Knife 19 in four ways:

- Set the license key in an environment variable
- Pass the license through bootstrap parameters
- Create and persist a license using the `knife license` CLI
- Use a pre-existing license stored on disk from an earlier Chef Infra Client or Chef Workstation installation

### Set the license as an environment variable

To configure the license key directly in the shell that runs Knife 19, set the license using the `export` command:

```bash
export CHEF_LICENSE_KEY="<LICENSE_KEY>"
```

The licensing library used by Knife 19 automatically reads this license and applies it during execution.

### Set the license using the knife license CLI

To add a license using the `knife license` CLI:

1. Run the license command:

   ```bash
   knife license
   ```

1. At the first prompt, select **I already have a license ID**.

1. Enter your license key at the second prompt.

Knife 19 obtains the license, validates it, and saves it to disk.

#### Verify your license

To verify that a valid license is saved on disk, run the license command:

```bash
knife license
```

This command verifies that a license is saved on disk, validates it with the licensing server, and prints the license details to the standard output.
If there isn't a valid license, it prompts you to activate one.

To return the details of all licenses stored on disk, run the license list command:

```bash
knife license list
```

### Use a pre-existing license

If you already activated a license with Chef Infra Client, Chef Workstation, or Test Kitchen Enterprise, Knife 19 automatically reads and uses it during bootstrap operations.

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
