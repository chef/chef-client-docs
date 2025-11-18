+++
title = "Chef Infra Client 19 RC3 release notes"

[menu.release_notes]
title = "Release notes"
+++

<!-- cspell:words Trixie leklund fretb tmccombs -->

## Improvements

- We changed the credentials file used to define target SSH connection settings in Chef Agentless from `~/.chef/credentials` to `~/.chef/target_credentials`.
- In the target credentials file used by Chef Agentless, we added `sudo = true` when logging in
to a target with a user that isn't root and you need to escalate privileges.
- In the Chef Infra Client migration tool, we replaced the `--preserve` flag with `--preserve-omnibus` when you want to install Chef Infra Client 19 RC3 and preserve an existing Omnibus-based Infra Client installation.

## Bug fixes

- We made several updates to the apt_repository resource:

  - Added support for Debian 13/Trixie where APT uses `sqv` to verify the keys. [#15220](https://github.com/chef/chef/pull/15220)

  - The apt_repository resource now correctly creates a GPG file when importing a key from keyserver. Thanks [leklund](https://github.com/leklund)! [#15008](https://github.com/chef/chef/pull/15008)

  - The apt_repository resource now handles a key that's defined as an array of multiple URLs and `signed_by` is `true`. Previously, each key would overwrite the previous one, leaving a keyring with only one key. Thanks [tmccombs](https://github.com/tmccombs)! [#15209](https://github.com/chef/chef/pull/15209)

  - The apt_repository resource now correctly doesn't set a value for `signed_by` if you don't specify a key and `signed_by` is `true`. Thanks [tmccombs](https://github.com/tmccombs)! [#15207](https://github.com/chef/chef/pull/15207)

  - The apt_repository resource can now handle multiple APT repositories with same key URL. Thanks [fretb](https://github.com/fretb)! [#15218](https://github.com/chef/chef/pull/15218)

- We removed the osx_profile resource. In 2020, Apple dropped support for non-interactively installing configuration profiles. We also removed the uuidtools gem because it was only used by the osx_profile resource. [#15184](https://github.com/chef/chef/pull/15184) [#15351](https://github.com/chef/chef/pull/15351)

- We fixed a bug in the group resource when multiple members with the same name are added to the same group. The group resource now removes duplicate members. [#14987](https://github.com/chef/chef/pull/14987)

- We made several knife code fixes. [#15195](https://github.com/chef/chef/pull/15195)
- We improved the handling of frozen_string_literals. [#15363](https://github.com/chef/chef/pull/15363)

## Security

- Updated uri to address CVE-2023-36617. [#15138](https://github.com/chef/chef/pull/15138)
- Updated webrick to address CVE-2025-6442. [#14698](https://github.com/chef/chef/pull/14698)

## Updated dependencies

We updated the following dependencies:

- Updated Ruby to 3.4.2. [#15379](https://github.com/chef/chef/pull/15379)
- Updated chef-powershell gem to 18.6.6 [#15426](https://github.com/chef/chef/pull/15426)
- Updated openssl gem to 3.3.0. [#15193](https://github.com/chef/chef/pull/15193)
- Updated Chef Inspec to the latest released version (7.0.95). [#15432](https://github.com/chef/chef/pull/15432)
- Updated Ohai to latest version (19.1.14). [#15406](https://github.com/chef/chef/pull/15406)
- Updated rest-client and chef-zero to remove activesupport. [#15419](https://github.com/chef/chef/pull/15419)
- We removed old .NET version 5 DLL files from the build. We now use .NET 8 and these files now come directly from the chef-powershell gem. [#15215](https://github.com/chef/chef/pull/15215)
