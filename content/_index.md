+++
title = "Chef Infra Client 19 RC2"
linkTitle = "Chef Infra Client"

[cascade]
  [cascade.params]
    product = []
    product_version = ''
    breadcrumbs = true
    st_robots = ''

[menu.landing_page]
title = "Chef Infra Client"
+++

To provide enterprise stability, Progress Chef has created a [Long Term Support (LTS) model](https://www.chef.io/blog/long-term-support-progress-chef-providing-stability) for products.
Chef Infra Client 19 is the first LTS version for infrastructure management and compliance mode.
This release---Release Candidate 2 (RC2)---is a preview for a very limited audience to provide candid feedback of Chef Infra Client,
the new Infra Client migration tool, and updated Test Kitchen developer tools to ensure a seamless transition at the time of general availability (GA).

The new Chef Infra Client migration tool eases the transition from previous methods of installing and maintaining earlier versions of Infra Client to the Infra Client 19 release candidates and the final LTS version.

The new Test Kitchen Enterprise bundle is a fully Chef-maintained version of Test Kitchen and is part of Chef Workstation at the time of release.

Chef Infra Client 19 RC2 is only intended for non-production environments to verify existing deployment patterns and content against customer-specific infrastructure platforms.

## Supported environments

The Chef Infra Client RC2 release is for testing in non-production environments only and is supported on Linux x86-64 systems.

This release allows you to determine if the migration tool can successfully upgrade your infrastructure to Chef Infra Client 19, to gain familiarity with Habitat-based builds, and prepare for new licensing requirements.

## Key features

Chef Infra Client 19 has the following key features:

- Chef Infra Client 19 is the long-term support (LTS) version, moving to Habitat-based packaging instead of traditional omnibus builds.
- Test Kitchen Enterprise is a foundational development tool for testing cookbooks and profiles across versions of Chef Infra Client.
  Chef InSpec is fully supported by Chef in a modularized Chef Workstation toolkit.
- Infra Client 19 and Test Kitchen Enterprise will utilize standard licensing for commercial, community, and trial customers.
- Chef InSpec resource packs is modularized to yield enhanced performance
- The Chef Infra Client migration tool installs and upgrades from previous versions to Chef Infra 19, supporting side-by-side installations.

Some significant changes that customers moving to Chef Infra Client 19 should be aware of include:

- RC2 is only supported on Linux x86-64 infrastructure; this is broadened to include traditional Chef platforms in future releases.
- Omnibus builds aren't provided for Infra Client and associated tools.
- OS-native and Habitat-based packaging are provided.
- Chef Workstation components are modularized to provide better support for individual tools.
- Chef InSpec resource packs is modularized for Inspec as part of the InSpec 7 LTS release (separate from the Infra Client LTS release)
