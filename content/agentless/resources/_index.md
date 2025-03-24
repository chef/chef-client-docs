+++
title = "Supported Chef Infra resources in Agentless Mode"
linkTitle = "Resources"

[menu.agentless]
title = "Supported resources"
identifier = "agentless/resources/overview"
parent = "agentless"
weight = 10
+++

The following Chef Infra resources are supported in Agentless Mode.

| **Resources Name** | **Verified Platforms** | **Remarks** |
|---|---|---|
| [alternatives](https://docs.chef.io/resources/alternatives/) | Ubuntu, Linux | |
| [apt_package](https://docs.chef.io/resources/apt_package/) | Ubuntu | |
| [apt_preference](https://docs.chef.io/resources/apt_preference/) | Ubuntu, Linux | |
| [apt_repository](https://docs.chef.io/resources/apt_repository/) | Ubuntu, Linux | |
| [apt_update](https://docs.chef.io/resources/apt_update/) | Ubuntu, Linux | |
| [bash](https://docs.chef.io/resources/bash/) | Ubuntu, Linux | |
| [breakpoint](https://docs.chef.io/resources/breakpoint/) | Ubuntu, Linux | |
| [chef_acl](https://docs.chef.io/resources/chef_acl/) | Ubuntu, Linux, Centos 9 | |
| [chef_client](https://docs.chef.io/resources/chef_client/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [chef_client_config](https://docs.chef.io/resources/chef_client_config/) | Ubuntu, Linux | |
| [chef_container](https://docs.chef.io/resources/chef_container/) | Ubuntu, Linux | |
| [chef_data_bag](https://docs.chef.io/resources/chef_data_bag/) | Ubuntu, Linux | |
| [chef_environment](https://docs.chef.io/resources/chef_environment/) | Ubuntu, Linux | |
| [chef_group](https://docs.chef.io/resources/chef_group/) | Ubuntu 24.04 and 18.04, RHEL | |
| [chef_node](https://docs.chef.io/resources/chef_node/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [chef_organization](https://docs.chef.io/resources/chef_organization/) | Ubuntu 24.04 and 18.04, RHEL | |
| [chef_role](https://docs.chef.io/resources/chef_role/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [chef_sleep](https://docs.chef.io/resources/chef_sleep/) | Ubuntu, Linux | |
| [chef_user](https://docs.chef.io/resources/chef_user/) | Ubuntu 24.04 and 18.04, RHEL | |
| [cookbook_file](https://docs.chef.io/resources/cookbook_file/) | Ubuntu, Linux | |
| [cron](https://docs.chef.io/resources/cron/) | Ubuntu, Linux | |
| [cron_access](https://docs.chef.io/resources/cron_access/) | Ubuntu, Linux | |
| [cron_d](https://docs.chef.io/resources/cron_d/) | Ubuntu, Linux | |
| [csh](https://docs.chef.io/resources/csh/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [directory](https://docs.chef.io/resources/directory/) | Ubuntu, Linux | |
| [execute](https://docs.chef.io/resources/execute/) | Ubuntu, Linux | |
| [file](https://docs.chef.io/resources/file/) | Ubuntu, Linux | |
| [freebsd_package](https://docs.chef.io/resources/freebsd_package/) | FreeBSD 14 | Only supported on FreeBSD. |
| [git](https://docs.chef.io/resources/git/) | Ubuntu, Linux | |
| [group](https://docs.chef.io/resources/group/) | Ubuntu, Linux | |
| [habitat_config](https://docs.chef.io/resources/habitat_config/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [habitat_install](https://docs.chef.io/resources/habitat_install/) | Ubuntu, Linux | |
| [habitat_package](https://docs.chef.io/resources/habitat_package/) | Ubuntu, Linux | |
| [habitat_service](https://docs.chef.io/resources/habitat_service/) | Ubuntu, Linux | |
| [habitat_sup](https://docs.chef.io/resources/habitat_sup/) | Ubuntu, Linux | |
| [hostname](https://docs.chef.io/resources/hostname/) | Ubuntu, Linux | |
| [http_request](https://docs.chef.io/resources/http_request/) | Ubuntu, Linux | |
| [ifconfig](https://docs.chef.io/resources/ifconfig/) | Ubuntu, Linux | |
| [inspec_input](https://docs.chef.io/resources/inspec_input/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [inspec_waiver](https://docs.chef.io/resources/inspec_waiver/) | Ubuntu, Linux | |
| [inspec_waiver_file_entry](https://docs.chef.io/resources/inspec_waiver_file_entry/) | Ubuntu, Linux | |
| [kernel_module](https://docs.chef.io/resources/kernel_module/) | Ubuntu, Linux | |
| [ksh](https://docs.chef.io/resources/ksh/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [link](https://docs.chef.io/resources/link/) | Ubuntu, Linux | |
| [locale](https://docs.chef.io/resources/locale/) | Ubuntu | |
| [log](https://docs.chef.io/resources/log/) | Ubuntu, Linux | |
| [mount](https://docs.chef.io/resources/mount/) | Ubuntu 24.04 / Centos 9 | |
| [notify_group](https://docs.chef.io/resources/notify_group/) | Ubuntu, Linux | |
| [ohai](https://docs.chef.io/resources/ohai/) | Ubuntu, Linux | |
| [ohai_hint](https://docs.chef.io/resources/ohai_hint/) | Ubuntu, Linux | |
| [owner](https://docs.chef.io/resources/owner/) | Ubuntu, Linux | |
| [package](https://docs.chef.io/resources/package/) | Ubuntu, Linux, Centos 9 | |
| [perl](https://docs.chef.io/resources/perl/) | Ubuntu | |
| [python](https://docs.chef.io/resources/python/) | Ubuntu 24.04, Linux Red Hat 9 | |
| [reboot](https://docs.chef.io/resources/reboot/) | Ubuntu, Linux | |
| [remote_file](https://docs.chef.io/resources/remote_file/) | Ubuntu, Linux, Centos 9 | |
| [rhsm_errata](https://docs.chef.io/resources/rhsm_errata/) | Linux (redhat) | |
| [rhsm_errata_level](https://docs.chef.io/resources/rhsm_errata_level/) | Linux (redhat) | |
| [rhsm_register](https://docs.chef.io/resources/rhsm_register/) | Linux (redhat) | |
| [rhsm_repo](https://docs.chef.io/resources/rhsm_repo/) | Linux (redhat) | |
| [rhsm_subscription](https://docs.chef.io/resources/rhsm_subscription/) | Linux (redhat) | |
| [route](https://docs.chef.io/resources/route/) | Ubuntu 24.04 / Centos 9 | |
| [rpm_package](https://docs.chef.io/resources/rpm_package/) | Centos 9 | The RPM package must be locally available on the remote system. |
| [ruby_block](https://docs.chef.io/resources/ruby_block/) | Ubuntu, Linux, Centos 9 | |
| [script](https://docs.chef.io/resources/script/) | Ubuntu 24.04, Linux Red Hat 9,0 | |
| [selinux_boolean](https://docs.chef.io/resources/selinux_boolean/) | Ubuntu, Linux | |
| [selinux_fcontext](https://docs.chef.io/resources/selinux_fcontext/) | Ubuntu, Linux | |
| [selinux_install](https://docs.chef.io/resources/selinux_install/) | Ubuntu, Linux | |
| [selinux_login](https://docs.chef.io/resources/selinux_login/) | Ubuntu, Linux | |
| [selinux_module](https://docs.chef.io/resources/selinux_module/) | Ubuntu, Linux | |
| [selinux_permissive](https://docs.chef.io/resources/selinux_permissive/) | Ubuntu, Linux | |
| [selinux_port](https://docs.chef.io/resources/selinux_port/) | Ubuntu, Linux | |
| [selinux_state](https://docs.chef.io/resources/selinux_state/) | Ubuntu, Linux | |
| [selinux_user](https://docs.chef.io/resources/selinux_user/) | Ubuntu, Linux | |
| [service](https://docs.chef.io/resources/service/) | Ubuntu, Linux, Centos 9 | `crond` for Linux |
| [snap_package](https://docs.chef.io/resources/snap_package/) | Ubuntu 24.04 | Only supported on Linux. |
| [ssh_known_hosts_entry](https://docs.chef.io/resources/ssh_known_hosts_entry/) | Ubuntu, Linux | |
| [subversion](https://docs.chef.io/resources/subversion/) | Ubuntu 24.04, Linux Red Hat 9, centOS 9 | The subversion resource has known bugs and may not work as expected. For more information, see the Chef GitHub issues, particularly [#4050](https://github.com/chef/chef/issues/4050) and [#4257](https://github.com/chef/chef/issues/4257). |
| [sudo](https://docs.chef.io/resources/sudo/) | Ubuntu, Linux, Centos 9 | |
| [swap_file](https://docs.chef.io/resources/swap_file/) | Ubuntu, Linux | |
| [sysctl](https://docs.chef.io/resources/sysctl/) | Ubuntu, Linux | |
| [systemd_unit](https://docs.chef.io/resources/systemd_unit/) | Ubuntu, Linux | |
| [template](https://docs.chef.io/resources/template/) | Ubuntu, Linux, Centos 9 | Require absolute path for source attribute. |
| [timezone](https://docs.chef.io/resources/timezone/) | Linux | |
| [user](https://docs.chef.io/resources/user/) | Ubuntu, Linux | |
| [user_ulimit](https://docs.chef.io/resources/user_ulimit/) | Ubuntu, Linux | |
| [yum_package](https://docs.chef.io/resources/yum_package/) | Centos 9 | Only supported on Linux. |
| [yum_repository](https://docs.chef.io/resources/yum_repository/) | Linux | |
| [yum_repository](https://docs.chef.io/resources/yum_repository/) | Centos 9, RHEL 8 | Only supported on Linux. |
| [zypper_package](https://docs.chef.io/resources/zypper_package/) | SUSE Linux 15 | |
