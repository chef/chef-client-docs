+++
title = "Chef Infra Client"
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

To provide enterprise stability with long term solutions, Progress Chef has stated its' [Long Term Support (LTS) model](https://www.chef.io/blog/long-term-support-progress-chef-providing-stability) for products. Infra Client 19 is the LTS version of client software for Infrastructure Management. With the first Release Candidate 1 (RC1) of Infra Client 19 we are moving to a Habitat (HAB) based package of Client bundle. This will work in tandem with a Test Kitchen Enterprise bundle (a Chef-maintained version of Test Kitchen included with Chef Workstation) and a migration or installable utility to migrate existing installations of omnibus builds to HAB builds.

Key capabilities in Infra Client 19 include:

- The introduction of licensing for Client software
- A Habitat (HAB) based builds mechanism of Infra Client
- The ability to manage clients with an agent-less mode of operation with out-of-the-box resources
- The usage of a Chef-maintained Test Kitchen bundle with the Client 19 package
- The usage of a migration or installation utility to migrate from an existing omnibus build package to a HAB package

Infra Client 19 RC1 is non-production usage software that can be used to verify existing deployment patterns of your client systems.

Some significant changes (which customers moving to Infra Client 19 should be aware of) include:

- Omnibus builds will not be provided for Infra Client and associated tools​
- All components of workstation packaged together through omnibus will cease to work​
- Native installers will cease to support esoteric platforms like AIX and Solaris​
- Resource packs will be modularized for InSpec as a part of the LTS release
