+++
title = "Chef Infra Client 19 RC2 release notes"

[menu.release_notes]
title = "Release notes"
+++

Progress Chef has introduced a [Long Term Support (LTS) model](https://www.chef.io/blog/long-term-support-progress-chef-providing-stability) to ensure enterprise stability.
Chef Infra Client 19 serves as the first LTS version for infrastructure management and compliance mode.
This release---Release Candidate 2 (RC2)---offers a preview for a limited audience to gather feedback on Chef Infra Client, the new Infra Client migration tool, native installers, Chef Workstation, and its component applications.
This feedback will help ensure a smooth transition when Chef Infra Client 19 reaches General Availability (GA).

This release enables you to:

- Test the migration tool's ability to upgrade your infrastructure to Chef Infra Client 19.
- Test the native installers.
- Familiarize yourself with Habitat-based builds.
- Install and test Chef Workstation and its components.
- Experiment with Chef Agentless.
- Prepare for new licensing requirements.

## Supported environments

Use the Chef Infra Client RC2 release exclusively for testing in non-production environments. It's supported on Linux x86-64 systems.

## Installers

Install or upgrade Chef Infra Client using a native installer or the Chef migration tool. For instructions, see the [install documentation]({{< relref "/install" >}}).

## Chef Target Mode/Agentless

We've rebranded Target Mode as Chef Agentless.

Chef Agentless, introduced in Chef Infra Client 15 as Target Mode, allows you to execute Chef resources on remote systems without installing Chef Infra Client. This simplifies managing the desired state of remote systems, edge devices, and cloud targets.

You can manage any system, target, or device's desired state without relying on specific platform support. Use compatible native resources or custom resources to manage devices. Once you create an agentless-compatible recipe, you can remotely manage the node from any server, workstation, container, or pipeline. Chef Agentless integrates seamlessly with systems, even those lacking native Chef Infra Client builds.

The host system connects to the target system using Train, a unified transport interface. Train protocols ensure the target system remains manageable and in the desired state from the host system.

For more information, see the [Agentless documentation]({{< relref "/agentless" >}}).

<!--

## Chef Ruby gem server

Chef's Ruby gem server now distributes Chef's commercial and licensed Ruby gems. Access the service at <https://rubygems.chef.io/>. This release includes a few test gems for you to try.

-->

## Chef Workstation

### Workstation tools

We've modularized Chef Workstation to enhance user experience and simplify interactions with its components.
This modular approach divides Chef Workstation into independent parts, allowing you to install, upgrade, and manage specific components individually using Chef Habitat.
This reduces the complexity of maintaining the entire package.

You can install and manage Chef Workstation and its components together or handle each application separately.

#### Excluded applications

This release excludes the Knife and InSpec applications from Chef Workstation.

### Chef Test Kitchen Enterprise

Test Kitchen Enterprise, initially available for testing during the Chef Infra Client 19 RC1 release, is now fully integrated into the Chef Workstation package. This integration ensures you can access the latest features and security updates without waiting for full workstation releases, improving productivity and minimizing downtime.

For this release, only the kitchen-dokken driver is supported.

### chef and chef-cli CLIs

The `chef` CLI isn't available in the RC2 release and is replaced by the `chef-cli` command.
Use `chef-cli` to execute all commands previously run with the `chef` command.

For example, replace:

```sh
chef generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

with:

```sh
chef-cli generate cookbook COOKBOOK_PATH/COOKBOOK_NAME (options)
```

{{< note >}}

For this release, the chef-cli `--help` option returns usage instructions for the chef CLI.

For example:

```sh
$ chef-cli generate --help

Usage: chef generate GENERATOR [options]
```

{{< /note >}}

#### Supported commands

The following commands are unavailable in the RC2 release:

- `chef-cli capture`
- `chef-cli report`
- `chef-cli supermarket`

Additionally, the `chef {-v|--version}` command is replaced by `chef-workstation {-v|--version}`.

For command syntax and usage, see the [`chef` reference documentation](https://docs.chef.io/workstation/ctl_chef/).

### chef-workstation CLI

This release introduces the new `chef-workstation` CLI, which only supports the `--version` (`-v`) option.

```sh
$ chef-workstation -v

Product Name: Chef Workstation
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
```
