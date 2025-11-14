+++
title = "Chef Infra Client 19 RC3"
linkTitle = "Chef Infra Client"

[cascade]
  [cascade.params]
    breadcrumbs = true
    st_robots = ''

[menu.landing_page]
title = "Chef Infra Client"
+++

To provide enterprise stability, Progress Chef has created a [Long Term Support (LTS) model](https://www.chef.io/blog/long-term-support-progress-chef-providing-stability) for products.
Chef Infra Client 19 is the first LTS version for infrastructure management and compliance mode.
This release---Release Candidate 3 (RC3)---is a preview for a limited audience to provide candid feedback on Chef Infra Client,
the new Infra Client migration tool, and updated Test Kitchen developer tools to ensure a seamless transition at the time of general availability (GA).

The new Chef Infra Client migration tool simplifies the transition from previous methods of installing and maintaining earlier versions of Infra Client to Chef Infra Client 19 release candidates and the final LTS version.

The new Test Kitchen Enterprise bundle is a fully Chef-maintained version of Test Kitchen that will be part of Chef Workstation at the time of release.

**Important:** Use Chef Infra Client 19 RC3 in non-production environments to verify existing deployment patterns and content against customer-specific infrastructure platforms.

## Supported environments

Chef Infra Client RC3 supports testing in non-production environments on Linux and Windows x86-64 systems.
Agentless Mode and Chef Workstation 26 RC3 are supported on Linux systems.

This release allows you to:

- Determine if the migration tool can upgrade your infrastructure to Chef Infra Client 19
- Gain familiarity with Habitat-based builds
- Prepare for new licensing requirements

## Key features

Chef Infra Client 19 has the following key features:

- **Long-term support (LTS):** Chef Infra Client 19 uses Habitat-based packaging instead of traditional omnibus builds.
- **Test Kitchen Enterprise:** A foundational development tool for testing cookbooks and profiles across versions of Chef Infra Client.
  Chef InSpec receives full support from Chef in a modularized Chef Workstation toolkit.
- **Standard licensing:** Infra Client 19 and Test Kitchen Enterprise use standard licensing for commercial, community, and trial customers.
- **Enhanced performance:** Chef InSpec resource packs will be modularized to improve performance.
- **Migration tool:** The Chef Infra Client migration tool installs and upgrades from previous versions to Chef Infra 19, supporting side-by-side installations.

## Important changes

Customers moving to Chef Infra Client 19 should be aware of these significant changes:

- **Platform support:** RC3 supports Linux and Windows x86-64 infrastructure. Future releases will expand support to include traditional Chef platforms.
- **Packaging changes:** Chef no longer provides Omnibus builds for Infra Client and associated tools.
- **New packaging options:** Chef now offers OS-native and Habitat-based packaging.
- **Modular components:** Chef Workstation components become modularized to provide better support for individual tools.
- **InSpec changes:** Chef InSpec resource packs become modularized for InSpec as part of the InSpec 7 LTS release (separate from the Infra Client LTS release).
