+++
title = "Chef Infra Agentless"
linkTitle = "Agentless"

[menu.agentless]
title = "Agentless overview"
identifier = "agentless/overview"
parent = "agentless"
weight = 10
+++

#### **Note:** Here, assuming that Chef-Client Infra and Chef Server setup / installation is already completed. If not you may refer- [https://progresssoftware.atlassian.net/wiki/spaces/Infra19/pages/1547534429/Chef+Server+Setup](file:////wiki/spaces/Infra19/pages/1547534429/Chef+Server+Setup)

####   Overview

Chef Infra Agentless mode allows you to run Chef Infra Client against remote nodes
without requiring a Chef agent on them. When using Chef Habitat (hab),
you can test Agentless configurations by executing Chef Infra Client
within a Habitat package environment.

**This guide explains how to:**
• Set up Chef Infra Client in Habitat for Agentless testing
• Run Chef Infra Client against remote nodes using hab

**Step 1:** Install Chef Habitat on your workstation (Linux)

> To install Habitat, you can use the following command:

curl -sSL
https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh
\| sudo bash

> This command downloads the installation script from the official
> Habitat repository and executes it with superuser privileges.
>
> To verify installation run:
>
> The command hab -V displays the version of the Habitat CLI, allowing
> users to confirm the installed version and ensure they are using the
> latest features and updates.
>
> hab 1.6.1243/20241227194506

**Step 2:** Install Chef Infra Client as a Habitat Package, If not
installed.

> To install the Chef Infra Client, use the following command:

hab pkg install chef/chef-infra-client

> This Command pulls the latest Chef Infra Client package into the
> Habitat environment.
>
> To check the version of the Chef Infra Client, you can use the
> following command:

hab pkg exec chef/chef-infra-client chef-client -v

> This command executes the Chef Infra Client package within the Habitat
> environment and displays the version number.
> Chef Infra Client: 19.0.85

**Step 3:** Execute Agentless with hab

> Run Chef Infra Client inside the Habitat package environment using hab
> pkg exec.
>
> To execute the Chef Infra Client, use the following command:

hab pkg exec chef/chef-infra-client chef-client -t Target_Mode_Name

> This command allows you to run the Chef Infra Client in a specific
> Agentless, designated by Target_Mode_Name.
>
> To execute the Chef Infra Client in a zero configuration mode, use the
> following command:

hab pkg exec chef/chef-infra-client chef-client -z -t Target_Mode_Name
cookbook_receipe_file_path

Sample:

hab pkg exec chef/chef-infra-client chef-client -z -t
Target_mode_centos9 cis_rhel_7\_benchmark_v3.1.1/recipes/test2.rb

> This command allows you to run the Chef client locally, specifying the
> Agentless and the path to the cookbook recipe file you wish to
> utilise.

**Step 4:** Verify Execution

Check the output for:
• Successful connection to the target node
• Execution of the run-list and application of configurations
• A final report showing applied changes

Converging 1 resources

Recipe:
@recipe_files::/root/.chef/chef-repo/cookbooks/cis_rhel_7\_benchmark_v3.1.1/recipes/test2.rb

\* subversion\[checkout_project_code\] action sync (up to date)

Running handlers:

Running handlers complete

Infra Phase complete, 0/1 resources updated in 20 seconds

To verify manually, SSH or RDP into the target node and inspect the
system configuration.
