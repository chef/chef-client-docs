+++
title = "Chef Infra Client 19 RC2 release notes"

[menu.release_notes]
title = "Release notes"
+++

To provide enterprise stability, Progress Chef has created a [Long Term Support (LTS) model](https://www.chef.io/blog/long-term-support-progress-chef-providing-stability) for products.
Chef Infra Client 19 is the first LTS version for infrastructure management and compliance mode.
This release---Release Candidate 2 (RC2)---is a preview for a limited audience to provide candid feedback of Chef Infra Client,
the new Infra Client migration tool, and updated Test Kitchen developer tools to ensure a seamless transition at the time of general availability (GA).

## Supported environments

The Chef Infra Client RC2 release is for testing in non-production environments only and is supported on Linux x86-64 systems.

This release allows you to determine if the migration tool can successfully upgrade your infrastructure to Chef Infra Client 19, to gain familiarity with Habitat-based builds, to install and test Chef Workstation and its component applications, to test Chef Agentless, and prepare for new licensing requirements.

## Installers

With this release, you can install and upgrade Chef Infra Client using a native installer or the Chef migration tool. For more information, see the [install documentation]({{< relref "/install" >}}).

## Chef Target Mode/Agentless

We've rebranded Target Mode as Chef Agentless.

Chef Agentless was introduced in Chef Infra Client 15. It allows you to execute Chef resources on remote systems without requiring Chef Infra Client installation. This simplifies managing the desired state of remote systems, edge devices, and cloud targets without installing a client or agent.

You can manage any system, target, or device's desired state without relying on specific platform support. Devices can be managed using compatible native resources or custom resources. Once you create an agentless-compatible recipe, you can remotely manage the node from any server, workstation, container, or pipeline. Chef Agentless works seamlessly with systems, even those lacking native Chef Infra Client builds.

The host system connects to the target system using Train, a unified transport interface. Train protocols ensure the target system is manageable and in the desired state from the host system.

For more information, see the [Agentless documentation]({{< relref "/agentless" >}}).

## Chef Ruby gem server

We're releasing Chef's Ruby gem server to distribute Chef's commercial and license Ruby gems. The service is available at <https://rubygems.chef.io/>. For this release, we've added a few test gems that you can try installing. For more information, see the [gem server documentation]({{< relref "/ruby_gem_server" >}}).

## Chef Workstation

### Workstation tools

We've modularized Chef Workstation to improve user experience and simplify interactions with its components.
This divides Chef Workstation into independent parts, enabling users to install, upgrade, and manage specific components individually using Chef Habitat.
This approach reduces the complexity of maintaining the entire package.

You can install and manage Chef Workstation and its components together or you install and manage each application separately.

#### Excluded applications

We aren't including the Knife and InSpec applications in Chef Workstation for this release.

### Chef Test Kitchen Enterprise

Test Kitchen Enterprise, initially available for testing during the Chef Infra Client 19 RC1 release, is now fully integrated into the Chef Workstation package. This integration ensures users can access the latest features and security updates without waiting for full workstation releases, improving productivity and minimizing downtime.

### chef and chef-cli CLIs

The `chef` CLI is deprecated and replaced by the `chef-cli` command. Use `chef-cli` to execute all commands that ran with the `chef` command.

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

For the RC2 release, the following commands aren't available:

- `chef-cli capture`
- `chef-cli report`
- `chef-cli supermarket`

In addition, the `chef {-v|--version}` command is replaced by `chef-workstation {-v|--version}`.

For information on command syntax and usage, see the [`chef` reference documentation](https://docs.chef.io/workstation/ctl_chef/).

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
