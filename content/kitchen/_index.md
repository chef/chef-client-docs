+++
title = "Installing Test Kitchen Enterprise"
linkTitle = "Installing Test Kitchen Enterprise"

[menu.kitchen]
title = "Installing Test Kitchen Enterprise"
identifier = "kitchen/overview"
parent = "kitchen"
weight = 10
+++

To install the new Chef Test Kitchen Enterprise, first ensure you have the latest Habitat installer. For details on how to do this, refer to the following section: [Hab-based builds]({{< relref "hab_builds" >}}).

Then use the Habitat installer to get the latest package from the Habitat Builder site:

```sh
sudo hab pkg install --binlink --force chef/chef-test-kitchen-enterprise --channel unstable
```

To test that Test Kitchen Enterprise is installed, check the version with:

```sh
kitchen --version
```

{{< note >}}
Windows is currently unsupported.
{{< /note >}}
