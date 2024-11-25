+++
title = "Test Kitchen"
linkTitle = "Test Kitchen"

[menu.kitchen]
title = "Overview"
identifier = "kitchen/overview"
parent = "kitchen"
weight = 10
+++

To install the new Chef Test Kitchen Enterprise, first ensure you have the latest Habitat installer. For details on how to do this, refer to the following section: [Hab-based builds]({{< relref "hab_builds" >}}).

Then use the Habitat installer to get the latest package from the Habitat Builder site:

```sh
hab pkg install chef/test-kitchen/3.7.1
```

To test that Test Kitchen Enterprise is installed, check the version with:

```sh
kitchen --version
```

If you see the following output, Test Kitchen Enterprise is installed:

```sh
Test Kitchen version 3.6.0
```

{{< note >}}
There is a bug in the output above - the folder is called 3.7.1 but the version command prints out a static string.
{{< /note >}}

{{< note >}}
Windows is currently unsupported.
{{< /note >}}
