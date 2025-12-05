+++
title = "About Knife"
linkTitle = "Knife"

[menu.workstation]
title = "About Knife"
identifier = "workstation/knife/about"
parent = "workstation/knife"
weight = 10
+++

Knife 19, now integrated into Chef Workstation 26 RC3, represents a significant milestone in Chef's migration to Habitat-based packaging.
As the essential command-line interface for Chef Infra Server interactions, Knife 19 is completely repackaged as a Habitat package, providing enhanced dependency management, improved plugin architecture, and streamlined distribution across enterprise environments.

This release delivers critical functionality for node management, cookbook operations, and infrastructure bootstrapping while maintaining full compatibility with existing Chef Infra Server deployments.
Knife 19 serves as the primary interface for Chef practitioners to manage their infrastructure-as-code workflows efficiently.

## What's new in RC3

The RC3 release of Knife 19 introduces several architectural and functional enhancements:

### Habitat-based architecture

- Knife is packaged independently as a Habitat package for improved modularity and dependency isolation
- Clean separation of dependencies ensures consistent execution across different environments
- Ruby gem-based plugins integrate seamlessly within the Habitat package structure

### Chef Infra Client 19 bootstrap support

- Native support for Chef Infra Client 19 Enterprise Edition (`chef-ice`) as the default bootstrap product
- Purpose-built installation scripts optimized for RC3 pre-release deployment scenarios
- Secure package distribution through pre-signed URLs for controlled access to release candidate packages
- Unified bootstrap workflow supporting both Linux and Windows target nodes

### Plugin ecosystem enhancement

- Validated plugins for major cloud providers (AWS, GCP) and Windows environments
- Framework prepared for additional cloud provider plugins in upcoming releases
- Existing knife workflows remain fully functional with enhanced underlying infrastructure

## What's the difference between Knife and Knife 19?

Knife 19 is a major architectural update that migrates from traditional packaging to Habitat-based distribution.
This update focuses on improved dependency management and enhanced plugin architecture for enterprise environments.

Key changes in Knife 19:

- Knife 19 is released as a Habitat package for better modularity and dependency isolation
- Enhanced plugin management with better cloud provider support
- Optimized for enterprise deployment scenarios with improved security

The way you use Knife remains largely unchanged. Existing knife commands and workflows continue to work with the enhanced underlying infrastructure.

## Knife commands reference

Knife 19 supports all the standard knife subcommands for managing Chef infrastructure.

For bootstrapping nodes with Knife 19 and Chef Infra Client 19 RC3, see the [Knife 19 bootstrap documentation](bootstrap).

For a complete reference of all available knife subcommands, syntax, and options, see the [Chef Workstation Knife documentation](https://docs.chef.io/workstation/knife/#knife-subcommands)

## Supported cloud provider plugins

Knife 19 includes plugins for major cloud providers to automate node provisioning and management:

### knife-ec2 (Amazon Web Services)

Manage EC2 instances directly from the knife command line:

- Create and bootstrap EC2 instances with Chef Infra Client
- Configure security groups and networking settings
- Apply AWS resource tags for compliance and cost tracking
- Support for multiple AWS regions and instance types

### knife-google (Google Cloud Platform)

Provision and manage Google Compute Engine instances:

- Create instances across GCP projects and zones
- Support for custom and public machine images
- Configure VPC networks and firewall rules
- Integrate with GCP resource hierarchies

### knife-windows (Windows Management)

Manage Windows nodes using WinRM protocol:

- Bootstrap Windows servers with Chef Infra Client
- Execute PowerShell commands remotely
- Manage Chef Infra Client service on Windows systems
- Support for Active Directory domain-joined systems

{{< note >}}

The `knife windows cert install` command has a known limitation where it may fail to import `.pfx` certificates with the error `CertUtil: The requested operation is not supported.`

{{< /note >}}

## More information

- [Knife 19 RC3 bootstrap documentation](bootstrap)
- [Chef Infra Client 18.x bootstrap documentation](https://docs.chef.io/install_bootstrap/)
- [Knife CLI documentation](https://docs.chef.io/workstation/knife/)
