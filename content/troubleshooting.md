+++
title = "Troubleshooting"

[menu.troubleshooting]
title = "Troubleshooting"
+++

How to list the gems with habitat builds?

sudo hab pkg exec chef/chef-infra-client gem list

How to list all the gems with habitat builds?

sudo hab pkg exec chef/chef-infra-client gem list--all

How to find the install path ?

sudo hab pkg exec chef/chef-infra-client gem env

How to find ruby version?

/hab/bin/hab pkg exec core/ruby3_1 ruby -v
