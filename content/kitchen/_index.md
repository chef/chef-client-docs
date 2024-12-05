+++
title = "Chef Test Kitchen Enterprise overview"
linkTitle = "Test Kitchen Enterprise"

[menu.kitchen]
title = "Overview"
identifier = "kitchen/overview"
parent = "kitchen"
weight = 10
+++

We've rebranded Test Kitchen, previously released as a component in Chef Workstation, as Chef Test Kitchen Enterprise, starting with version 1.0.0.
Test Kitchen Enterprise's repository is [chef/chef-test-kitchen-enterprise](https://github.com/chef/chef-test-kitchen-enterprise) and is a direct fork from the original community version.

They way that users invoke Test Kitchen Enterprise wasn't altered.
This update emphasizes branding changes.
The [community Test Kitchen documentation](https://kitchen.ci/docs/getting-started/introduction/) and [Test Kitchen documentation](https://docs.chef.io/workstation/kitchen/) included with the Chef Workstation documentation is still accurate.

We implemented several licensing-related changes to Test Kitchen Enterprise to pass the license through to Chef Infra Client 19.
These modifications are implemented only in Chef Test Kitchen Enterprise and aren't backported to the community version of Test Kitchen.

We anticipate that additional drivers and features---which will be supported directly by Chef---will also be added to Chef Test Kitchen Enterprise in future releases.
