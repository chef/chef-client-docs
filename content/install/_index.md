+++
title = "Download and Install Chef Infra Client"
linkTitle = "Download and install"

[menu.install]
title = "Overview"
identifier = "install/overview"
parent = "install"
weight = 10
+++

Chef Infra Client will be primarily downloaded and installed using the migration tool. For instructions relating to the migration tool, refer to the migration tool specific download instructions.

For RC1, Chef infra Client and the migration tool will be available through pre-signed URLs for S3 buckets where a Chef Infra Client tarball and migration tool utility is available for download.

## Prerequisites

Before you begin using Chef Infra 19 with its integrated licensing, follow these general instructions:

1. You can choose to work with either the "acceptance" or "production" environment for the licensing server.
    - If you opt for the "acceptance" environment, you must set an environment variable. Regular customers do not need to perform this step.
1. If any other version of Chef Infra is already installed on your system,  uninstall it before continuing.
1. Install the Chef Infra 19 package. The installation process is the same as the existing and older versions of Chef Infra.
1. Use one of the provided test license keys (when prompted) while running Chef Infra commands.

If you encounter any difficulties, feel free to comment on this page for support.

## Installation steps

Chef Infra Client 19 RC1 can be installed as a fresh install or as a migration from an existing version of Chef Infra Client using the migration tool. After the migration tool has been installed, use the following command to download and install Chef Infra Client RC1:

```sh
/chef-migrate --version
```

Lastly, run the migration using the online flags, as follows:

- `--download.url` with the location provided by Chef to download the Chef 19 RC1 Client. If the location is not supplied, this is the default Chef download API.
- `--license.key` with the license key for the download URL.
- `--fresh_install` (optional) to re-install a previous installation or when no previous Chef client install exists.
