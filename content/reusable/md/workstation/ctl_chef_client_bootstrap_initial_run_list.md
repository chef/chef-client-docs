A node's initial run-list is specified using a JSON file on the host
system. When running Chef Infra Client as an executable, use the `-j`
option to tell Chef Infra Client which JSON file to use. For example:

```bash
chef-client -j /etc/chef/file.json --environment _default
```

Where:

- `_default` is the name of the environment assigned to the node.
- `file.json` is similar to the following:

```json
{
  "resolver": {
    "nameservers": [ "10.0.0.1" ],
    "search":"int.example.com"
  },
  "run_list": [ "recipe[resolver]" ]
}
```

{{< warning >}}

You can use this approach to update [normal](/cookbooks/attributes/attribute_types/) attributes, but don't use it to update any other attribute type.
Chef Infra Client treats all attributes set with this option as `normal` attributes.

{{< /warning >}}
