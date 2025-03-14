+++
title = "Run Test Kitchen"
linkTitle = "Using Test Kitchen"

[menu.kitchen]
title = "Run Test Kitchen"
identifier = "kitchen/using_test_kitchen"
parent = "kitchen"
weight = 40
+++

For the Chef Infra Client RC1 release, Chef Test Kitchen Enterprise supports only the kitchen-dokken driver.
This driver allows you to create containers with different operating systems using Podman or Docker Desktop and configure Chef Infra Client 19 for converge and verify operations.
By default, kitchen-dokken uses the `chef/chef-hab` container volume from Docker Hub to attach Chef Infra Client 19 and Chef InSpec 6 (the default verifier) to the test container.

## Prerequisites

To use kitchen-dokken, you must have Docker running on the same system that's running Chef Test Kitchen Enterprise.

## Example `kitchen.yaml` for Chef Infra Client 19

The following `kitchen.yaml` file example defines tests that run in Chef Infra Client 19:

```yaml
---
driver:
  name: dokken
  privileged: true
  chef_version: unstable

provisioner:
  name: dokken

transport:
  name: dokken

verifier:
  name: inspec

platforms:
  - name: ubuntu-20.04
  - name: centos-8

suites:
  - name: default
    run_list:
      - "cookbook"
    verifier:
      inspec_tests:
        - test/integration/default
```

## Provision earlier versions of Chef Infra Client

To provision containers to use Chef Infra Client version 18 or earlier, modify the driver configuration in the `kitchen.yml` file as shown below.
Set `chef_image` to `chef/chef` and set the version of Infra Client in `chef_version`.

```yaml
driver:
  name: dokken
  privileged: true
  chef_version: 18.3.0
  chef_image: "chef/chef"
```

## Run converge and verify tests

The [Test Kitchen documentation](https://kitchen.ci/docs/getting-started/creating-cookbook/) describes the process for creating converge and verify tests. The Dokken driver documentation is in the [kitchen-dokken GitHub repository](https://github.com/chef/kitchen-dokken).

## Habitat-based changes

The Chef Infra Client 19 will be accessible using Habitat instead of the public Omnitruck APIs. Consequently, we've updated the provisioner to facilitate the installation of the Habitat-based Chef Infra Client, including passing through the license required from `kitchen.yml` file.
