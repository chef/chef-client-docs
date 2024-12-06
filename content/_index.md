+++
title = "Chef Infra Client 19 RC1"
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
This release---Release Candidate 1 (RC1)---is a preview for a very limited audience to provide candid feedback of Chef Infra Client,
the new Infra Client migration tool, and updated Test Kitchen developer tools to ensure a seamless transition at the time of general availability (GA).

The new Chef Infra Client migration tool eases the transition from previous methods of installing and maintaining earlier versions of Infra Client to the Infra Client 19 release candidates and the final LTS version.

The new Test Kitchen Enterprise bundle is a fully Chef-maintained version of Test Kitchen and will be a part of Chef Workstation at the time of release.

Chef Infra Client 19 RC1 is only intended for non-production environments to verify existing deployment patterns and content against customer-specific infrastructure platforms.

## Key features

Chef Infra Client 19 has the following key features:

Key capabilities in Chef Infra Client 19 include:

- Chef Infra Client 19 will be the long-term support (LTS) version, moving to Habitat-based packaging instead of traditional omnibus builds.
- Test Kitchen Enterprise will be a foundational development tool for testing cookbooks and profiles across versions of Chef Infra Client.
  Chef InSpec will be fully supported by Chef in a modularized Chef Workstation toolkit.
- Infra Client 19 and Test Kitchen Enterprise will utilize standard licensing for commercial, community, and trial customers.
- Chef InSpec resource packs will be modularized to yield enhanced performance
- The Chef Infra Client migration tool will facilitate installation and upgrades from previous versions to Chef Infra 19, supporting side-by-side installations.

Some significant changes that customers moving to Chef Infra Client 19 should be aware of include:

- RC1 is only supported on Linux x86-64 infrastructure; this will be broadened to include traditional Chef platforms in future releases.
- Omnibus builds won't be provided for Infra Client and associated tools.
- OS-native and Habitat-based packaging are provided.
- Chef Workstation components will be modularized to provide better support for individual tools.
- Chef InSpec resource packs will be modularized for Inspec as a part of the InSpec 7 LTS release (separate from the Infra Client LTS release)

## Chef Infra Client migration tool

The Chef Infra Client migration tool can create a fresh install of Chef Infra Client or upgrade to the latest version.

The `chef-migrate` command-line tool supports:

- New installation of Chef Infra Client 19.
- Installation of Chef Infra Client 19 RC1, either by removing or leaving the previous version of Infra Client and running in side-by-side mode, with the path to the most recent version taking precedence.
- Upgrading from Chef Infra Client 17.x and 18.x (also referred to as "Omnibus distributions").
- Upgrading to Chef Infra Client 19 RC1 and subsequent versions (also referred to as "Habitat-packaged")
- During the release candidate time frame, automatically downloading from the new distribution point and checking prerequisites for the client.
