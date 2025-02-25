+++
title = "Chef Development Kit Enterprise"

[menu.dke]
title = "Chef DKE overview"
identifier = "dke/overview"
parent = "dke"
weight = 10
+++

## Overview

Start your infrastructure automation with <u>Chef Developement Kit
Enterprise</u> Chef Developement Kit Enterprise gives you everything you
need to get started with Chef - ad hoc remote execution, remote
scanning, configuration tasks, cookbook creation tools as well as robust
dependency and testing software - all in one easy-to-install package.

We’ve rebranded the Chef workstation to the Chef development kit
enterprise referred to as Chef DKE, and substantial changes have been
made in installation and licensing.

This update emphasizes branding changes and supports licensing.

Now Chef DKE comes with Chef Test Kitchen Enterprise instead of a
community-driven test-kitchen.

**Tools available in this RC2 release**

| Chef Command Line Tool                                                       |
|------------------------------------------------------------------------------|
| Chef Test Kitchen Enterprise (currently supports only kitchen dokken driver) |
| Chef Infra Client 19                                                         |
| Cookstyle                                                                    |
| Berkshelf                                                                    |
| Chef Vault                                                                   |
| Ohai                                                                         |
| Fauxhai                                                                      |

## Platform Support

Chef Development Kit Enterprise RC2 is only supported on the Linux
x86_64 architecture/platform.

## Prerequisites

Chef Development Kit Enterprise is a habitat package that requires
habitat to be installed as a prerequisite.

## Install Habitat

Please follow the
[instructions](https://docs.chef.io/habitat/install_habitat/) or use one
of the following commands to install Habitat.

curl
https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh
\| sudo bash -s -- -c stable -v 1.6.652

Or

curl -o install.sh
https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh

./install.sh -c stable -v 1.6.652

Note that the current directory should be writeable and you may need to
chmod 777 ./install.sh to execute the installation script. Verify the
version installed with:

hab --version

hab 1.6.652/20230206155653

**Hab Setup**

Once installed, setup Habitat with:

hab cli setup

During the setup, users will be prompted for multiple defaults. Our
recommended settings to get to Test Kitchen Enterprise are shown below:

- Connect to an on-premises Builder instance? \[yes/No/quit\] **No**

- Set up a default origin? \[Yes/no/quit\] **no**

- Set up a default Builder personal access token? \[yes/No/quit\] **No**

- Set up a default Habitat Supervisor control gateway secret ?
  \[yes/No/quit\] **No**

root@520f013a6154:/migration# hab setup

+---------------------------------------------+

Chef License Acceptance

Before you can continue, 1 product license must be accepted.

View the license at https://www.chef.io/end-user-license-agreement

License that needs accepting:

\* Habitat

Do you accept the 1 product license? \[yes/No/quit\] yes

Accepting 1 product license...

✓ 1 product license accepted.

+---------------------------------------------+

Habitat CLI Setup

=================

Welcome to hab setup. Let's get started.

Habitat Builder Instance

Habitat packages can be stored in either the public builder instance

https://bldr.habitat.sh or in an on-premises builder depot instance. If

you do not set a builder URL now, the \`hab\` CLI will default to using

the public builder instance. This can be overridden at any time after

setup.

Connect to an on-premises Builder instance? \[yes/No/quit\] No

Alright, maybe another time. You can also set a \`HAB_BLDR_URL\`

environment variable or pass the \`--url\` flag to the cli.

Set up a default origin

Every package in Habitat belongs to an origin, which indicates the

person or organization responsible for maintaining that package. Each

origin also has a key used to cryptographically sign packages in that

origin.

Selecting a default origin tells package building operations such as

'hab pkg build' what key should be used to sign the packages produced.

If you do not set a default origin now, you will have to tell package

building commands each time what origin to use.

For more information on origins and how they are used in building

packages, please consult the docs at

https://www.habitat.sh/docs/create-packages-build/

Set up a default origin? \[Yes/no/quit\] no

Alright, maybe another time. You can also set a \`HAB_ORIGIN\`
environment

variable when using the cli.

Habitat Personal Access Token

While you can perform tasks like building and running Habitat packages

without needing to authenticate with Builder, some operations like

uploading your packages to Builder, or checking the status of your build

jobs from the Habitat client will require you to use an access token.

The Habitat Personal Access Token can be generated via the Builder

Profile page (https://bldr.habitat.sh/#/profile). Once you have

generated your token, you can enter it here.

If you would like to save your token for use by the Habitat client,

please enter your access token. Otherwise, just enter No.

For more information on using Builder, please read the documentation at

https://www.habitat.sh/docs/using-builder/

Set up a default Builder personal access token? \[yes/No/quit\] No

Alright, maybe another time. You can also set a \`HAB_AUTH_TOKEN\`

environment variable or pass the \`--auth\` flag to the cli.

Supervisor Control Gateway Secret

The Supervisor control gateway secret is used to authenticate hab client

commands to a Supervisor. When a new Supervisor is created, a unique

secret is generated automatically and stored locally in a file:

\`/hab/sup/default/CTL_SECRET\`. When issuing commands to a local

Supervisor, the control gateway secret is retrieved from this file.

Typically, a default Supervisor control gateway secret would only be

needed if you wish to send commands to a remote supervisor, in which

case, a default control gateway secret would need to match the one

already in use by the remote supervisor.

Set up a default Habitat Supervisor control gateway secret?
\[yes/No/quit\] No

Alright, maybe another time. You can also set a \`HAB_CTL_SECRET\`

environment variable when issuing commands to a remote Supervisor.

CLI Setup Complete

That's all for now. Thanks for using Habitat!

## Install Chef Development Kit Enterprise

Once Habitat installation is finished then use the Habitat installer to
get the latest package from the Habitat Builder site:  
Install Chef DKE using the following command

sudo hab pkg install --binlink --force
chef/chef-development-kit-enterprise --channel unstable

Users will see the download of Chef Development Kit Enterprise and its
components.

✓ Installed chef/cookstyle/7.32.13/20250204071253

✓ Installed chef/chef-vault/4.1.15/20250203110841

✓ Installed chef/fauxhai/9.3.22/20250204065137

✓ Installed chef/ohai/19.0.7/20250203133705

✓ Installed chef/berkshelf/8.0.17/20250203081548

✓ Installed chef/chef-test-kitchen-enterprise/1.0.14/20250204082641

✓ Installed chef/chef-cli/5.6.17/20250205114629

✓ Installed chef/chef-infra-client/19.0.85/20250204212822

✓ Installed chef/chef-development-kit-enterprise/0.1.4/20250205135036

Verify the versions with:

chef-dke -v

Product Name: Chef Development Kit Enterprise

Product Version: 0.1.4

Default Installed Components:

Chef Infra Client Version: 19.0.85

Chef CLI Version: 5.6.17

Chef Test Kitchen Enterprise Version: 1.0.14

Berkshelf Version: 8.0.17

Ohai Version: 19.0.7

Fauxhai Version: 9.3.22

Chef Vault Version: 4.1.15

Cookstyle Version: 7.32.13

**Newly introduced commands**  
We have introduce the new command chef-dke which for now only have
version sub-command.

chef-dke -v

Product Name: Chef Development Kit Enterprise

Product Version: 0.1.4

Default Installed Components:

Chef Infra Client Version: 19.0.85

Chef CLI Version: 5.6.17

Chef Test Kitchen Enterprise Version: 1.0.14

Berkshelf Version: 8.0.17

Ohai Version: 19.0.7

Fauxhai Version: 9.3.22

Chef Vault Version: 4.1.15

Cookstyle Version: 7.32.13

**Deprecated** **commands:**

chef command is deprecated, and you can use chef-cli command to execute
all commands that were previously functional with chef command.

chef -v // no longer work

chef-dke -v // will work

chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options) // No
longer work

chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options) // will
work

For the RC2 release chef report command is not available

# Apply a license in Chef Development Kit Enterprise

Execution of Chef Infra Client 19 and Chef Test Kitchen Enterprise
requires a valid license.

we’ve enhanced Test Kitchen Enterprise, chef-cli and chef infra to
prompt users for a license, activate it, and securely store it on disk.
Additionally, the license is transmitted to the provisioned VM, allowing
the Chef Infra Client to function effectively during the verification
phase alongside Chef InSpec.

The following sections provide further details on this process

## Which license do I need?

You can use any license that’s entitled to run Chef DKE. Obtain a free,
trial, or commercial license that has Chef Workstation entitlement
enabled to use the Test Kitchen Enterprise seamlessly.

To execute Chef Infra 19 it requires a license entitled to use that
Product.  
  
**Add the license as an environment variable**

You can set the license key adding the CHEF_LICENSE_KEY environment
variable:

export CHEF_LICENSE_KEY=\<LICENSE_KEY\>

Note: if you are using local licensing server you need to set this env
variable also

export CHEF_LICENSE_SERVER=\<LICENSE_SERVER\>

### Add the license using the test-kitchen CLI

Follow these instructions to add a license using the test-kitchen CLI:

1.  You can add a license using the test-kitchen CLI:

> sudo kitchen license

2.  At the first prompt, select **I already have a license ID**

3.  sudo kitchen license

4.  ------------------------------------------------------------

5.  License ID Validation

6.  

7.  To continue using Chef InSpec, a license ID is required.

8.  (Free, Trial, or Commercial)

9.  

10. If you generated a license previously, you might

11. have received it in an email.

12. 

13. If you are a commercial user, you can also find it in the

14. supportlink.chef.io portal.

15. ------------------------------------------------------------

16. 

17. Please choose one of the options below (Press ↑/↓ arrow to move and
    Enter to select)

18. ‣ I already have a license ID

19. I don't have a license ID and would like to generate a new license
    ID

20. Skip

21. Enter your license key at the second prompt.

22. Please choose one of the options below I already have a license ID

23. Please enter your license ID: \<LICENSE_KEY\>

24. ✔ \[Success\] License validated successfully.

25. ------------------------------------------------------------

26. License Details

27. Asset Name : Workstation

28. License ID : \<LICENSE_KEY\>

29. Type : Free Tier

30. Status : Active

31. Validity : Unlimited

32. No. Of Units : 10 Nodes

33. ------------------------------------------------------------

34. Optional: Verify a valid license is saved on disk.  
    The following command verifies that a license is saved on disk,
    verifies it with the licensing server, and prints licensing details
    to the standard output. If there isn’t a valid license, it will ask
    you to activate one.

> kitchen license
>
> The following command returns the details of all licenses stored on
> disk.
>
> kitchen license

**Standalone installation of components:**  
Users can install the components included with the Chef Development Kit
Enterprise without needing to install the Chef DKE. Below are the
components that can be installed independently.

| Chef Command Line Tool                                    |
|-----------------------------------------------------------|
| Chef Test Kitchen Enterprise (only kitchen dokken driver) |
| Chef Infra Client                                         |
| Cookstyle                                                 |
| Berkshelf                                                 |
| Chef Vault                                                |
| Ohai                                                      |
| Fauxhai                                                   |

Users can install any of the components and utilize them effectively.

**installing Chef Command Line Tool**

sudo hab pkg install chef/chef-cli --channel unstable --binlink --force

To use

chef-cli -v

**for installing Chef Test Kitchen Enterprise**

sudo hab pkg install chef/chef-test-kitchen-enterprise --channel
unstable --binlink --force

To use

kitchen -v

**for installing Chef Infra Client**

sudo hab pkg install chef/chef-infra-client --channel unstable --binlink
--force

To use

chef-client -v

**for installing Cookstyle**

sudo hab pkg install chef/cookstyle --channel unstable --binlink --force

To use

cookstyle -v

**for installing Berkshelf**

sudo hab pkg install chef/berkshelf --channel unstable --binlink --force

To use

berks -v

**for installing Chef Vault**

sudo hab pkg install chef/chef-vault --channel unstable --binlink
--force

To use

chef-vault \<args\>

**for installing Ohai**

sudo hab pkg install chef/ohai --channel unstable --binlink --force

To use

ohai -v

**for installing Fauxhai**

sudo hab pkg install chef/fauxhai --channel unstable --binlink --force

To use

fauxhai -v

### To Use different version of any tool

By default, the Chef Development Kit Enterprise utilizes the latest
version of the installed tools.

Suppose you wish to use a different version of any tool that is not
included with the Chef Development Kit Enterprise. In that case, you
will need to install that specific version and set the environment
variable for the corresponding tool.

Below is a list of environment variables for the tools:

| **Name**                     | **Env variable name**     |
|------------------------------|---------------------------|
| Chef client                  | CHEF_INFRA_CLIENT_VERSION |
| Berkshelf                    | BERKSHELF_VERSION         |
| Chef CLI                     | CHEF_CLI_VERSION          |
| Chef vault                   | CHEF_VAULT_VERSION        |
| Cookstyle                    | COOKSTYLE_VERSION         |
| Fauxhai                      | FAUXHAI_VERSION           |
| Ohai                         | OHAI_VERSION              |
| Chef Test Kitchen Enterprise | KITCHEN_VERSION           |
| Knife                        | NA                        |
| Inspec                       | NA                        |
