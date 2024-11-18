+++
title = "Download and Install Chef Infra Client"
linkTitle = "Download and install"

[menu.install]
title = "Overview"
identifier = "install/overview"
parent = "install"
weight = 10
+++

Refer to the following sections for details on prerequisites and installation steps.

## Prerequisites

Before you begin using Chef Infra 19 with its integrated licensing, follow these general instructions:

1. You can choose to work with either the "acceptance" or "production" environment for the licensing server.
    - If you opt for the "acceptance" environment, you must set an environment variable. Regular customers do not need to perform this step.
1. If any other version of Chef Infra is already installed on your system,  uninstall it before continuing.
1. Install the Chef Infra 19 package. The installation process is the same as the existing and older versions of Chef Infra.
1. Use one of the provided test license keys (when prompted) while running Chef Infra commands.

If you encounter any difficulties, feel free to comment on this page for support.

## Installation steps

The installation steps for the Chef Infra Client is unchanged from the current process:

1. Download the Chef Infra Client Installer for your operating system.
1. Run the installer.
1. Follow the on-screen instructions to complete the installation.
1. Verify the installation. After installation, open your terminal (macOS) or command prompt (Windows) and run:

```sh
chef-client --version
```
