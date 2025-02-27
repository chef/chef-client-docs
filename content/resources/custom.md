+++
title = "Custom resource guide"

[menu]
  [menu.infra]
    title = "Custom resource guide"
    identifier = "chef_infra/resources/custom_resources/custom_resources.md custom resources"
    parent = "chef_infra/resources/custom_resources"
    weight = 10
+++

## Providers

The following custom resource providers determine whether Chef Infra Client can run a resource on a node locally or remotely:

`agent_mode`
: Whether Chef Infra Client can execute the resource locally on a node.

  Default value: `true`

`target_mode`
: Whether Chef Infra Client can execute the resource on a node from a remote connection.

  Default value: `false`

You can combine these providers to define whether Chef Infra Client runs a custom resource locally on a node, on a node from a remote connection, or both.

For example:

- Chef Infra Client only executes this resource locally on a node, as `target_mode` is set to `false` and `agent_mode` defaults to `true`:

  ```ruby
  provides :<RESOURCE_NAME>, target_mode: false
  ```

- Chef Infra Client executes this resource from a remote connection, but not locally:

  ```ruby
  provides :<RESOURCE_NAME>, target_mode: true, agent_mode: false
  ```

- Chef Infra Client executes this resource from a remote connection and also locally:

  ```ruby
  provides :<RESOURCE_NAME>, target_mode: true, agent_mode: true`
  ```

## Input/output operations in Agentless Mode

Agentless Mode includes an input/output (IO) abstraction layer.

IO operations within Chef fall into two different groups:

- Shell commands using `shell_out` or `shell_out!`.
- Native IO using `TargetIO` classes.

### shell_out

Any implementations using `shell_out` is automatically Agentless Mode-capable, as the execution target dynamically changes between local and remote invocations.

### TargetIO

When running resources in Agentless Mode, use `TargetIO` to translate native IO calls into scripting commands.

{{< note >}}

If `TargetIO` is used in Agent Mode, it automatically passes operations to Ruby's native APIs.

{{< /note >}}

The following classes run the most commonly used IO calls:

- `TargetIO::Etc`
- `TargetIO::Dir`
- `TargetIO::File`
- `TargetIO::FileUtils`
- `TargetIO::HTTP`
- `TargetIO::IO`
- `TargetIO::Shadow`

If your resources use the re-implemented IO methods, you just need to prefix normal IO calls with the `TargetIO` namespace.

For example, change:

```ruby
contents = IO.read(filename)
```

to:

```ruby
contents = TargetIO::IO.read(filename)
```

{{< note >}}

The `TargetIO::HTTP` class auto detects if `curl` or `wget` are installed on the target node and channels HTTP-related requests through either one if they're installed.

{{< /note >}}
