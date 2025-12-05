+++
title = "Chef Workstation 26 RC3"
linkTitle = "Workstation"

[menu.workstation]
title = "Overview"
identifier = "workstation/overview"
parent = "workstation"
weight = 10
+++

Chef Workstation 26 RC3 delivers a comprehensive, unified toolkit that empowers developers, operations teams, and system administrators to automate infrastructure management and compliance workflows. This release provides all essential tools required to efficiently build, test, and deploy infrastructure code, ensuring seamless configuration management across diverse environments.

Chef Workstation represents a complete development environment for Chef, consolidating critical tools into a single, cohesive package that streamlines the infrastructure-as-code workflow from development through production deployment.

## What's new in RC3

The RC3 release of Chef Workstation 26 represents a significant architectural evolution, featuring:

- **Habitat-Based Architecture**: All core components have been migrated to Habitat packages, providing improved dependency management, isolation, and cross-platform consistency
- **Enhanced Knife Integration**: Full Habitat packaging of Knife and associated drivers, enabling more reliable plugin management and execution
- **InSpec Integration**: InSpec compliance and security testing framework is now included, providing comprehensive infrastructure and application auditing capabilities
- **Unified Package Distribution**: Consolidated delivery mechanism through Habitat, simplifying installation and updates across enterprise environments
- **Improved Tool Accessibility**: All included tools are accessible through standardized wrapper scripts for a consistent user experience

This release builds upon the foundation established in Chef Workstation 26 RC2, with continued refinement of the Habitat-based packaging system and expanded tool support.

This release builds upon the foundation established in RC2, with continued refinement of the Habitat-based packaging system and expanded tool support.

## Included tools and components

Chef Workstation RC3 includes the following fully integrated tools:

### Core development tools

- **Chef CLI (**`chef-cli`): Primary command-line interface for Chef development workflows, providing unified access to common Chef operations
- **Chef Infra Client RC3**: Latest release candidate of the Chef Infra Client, enabling infrastructure automation and configuration management
- **Knife**: Essential tool for interacting with Chef Infra Server, managing nodes, cookbooks, roles, and other Chef objects
- **InSpec**: Latest release candidate of InSpec 7, enabling compliance and security testing.

### Testing and quality assurance

- **Chef Test Kitchen Enterprise**: Comprehensive testing framework for validating infrastructure code across multiple platforms and environments
- **InSpec**: Compliance and security testing framework for auditing infrastructure and applications against security standards and regulations
- **Cookstyle**: Ruby and Chef cookbook linting tool that enforces style guidelines and best practices
- **Fauxhai**: Mock Ohai data generator for testing purposes, enabling rapid cookbook testing without requiring actual systems

### Dependency and secret management

- **Berkshelf**: Cookbook dependency manager that streamlines the process of managing and retrieving cookbook dependencies
- **Chef Vault**: Secure data management tool for encrypting and managing secrets within Chef workflows
- **Ohai**: System profiling tool that detects and reports system attributes for use in Chef recipes

## Known limitations

### `chef` command deprecation

The legacy `chef` command is deprecated and isn't functional in this release. All users must transition to using `chef-cli` commands instead. This change aligns with Chef's strategic direction toward a more modular and maintainable command structure.

```sh
# Deprecated (will not work)
chef generate cookbook my_cookbook

# Correct usage
chef-cli generate cookbook my_cookbook
```

## Support and feedback

As this is a release candidate, we actively encourage feedback from the community:

- **Issues and Bugs**: Report issues through the official Chef GitHub repository
- **Feature Requests**: Submit enhancement requests via the Chef community forums
- **Documentation**: See the [Chef documentation](https://docs.chef.io) for comprehensive guides and tutorials
- **Community Support**: Join the [Chef Community Slack](https://community-slack.chef.io/) for real-time assistance

## Additional resources

- [Chef Workstation documentation](https://docs.chef.io/workstation/)
- [Chef Habitat documentation](https://docs.chef.io/habitat/)
- [Chef Infra Client documentation](https://docs.chef.io/chef_client_overview/)
- [Test Kitchen documentation](https://kitchen.ci/)
- [Cookstyle documentation](https://docs.chef.io/workstation/cookstyle/)
