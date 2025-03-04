+++
title = "Custom resource guide"

[menu]
  [menu.agentless]
    title = "Custom resource guide"
    identifier = "resources/custom"
    parent = "agentless"
    weight = 10
+++

To use custom resources in Agentless mode, you'll have to update the provider properties and IO class methods so that Chef Infra Client can run them.

## Providers

Providers determine whether Chef Infra Client can locally or remotely run a resource on a node.

To enable Infra Client to run a resource locally or remotely, use the `agent_mode` and `target_mode` properties to define the environments that the resource can run in.

`agent_mode`
: Whether Chef Infra Client can execute the resource locally on a node.

  Default value: `true`

`target_mode`
: Whether Chef Infra Client can execute the resource on a node from a remote connection.

  Default value: `false`

You can combine these properties to define whether Chef Infra Client can run a custom resource locally on a node, on a node from a remote connection, or both.

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

IO operations in Chef Infra resources fall into two different groups:

- Shell commands using `shell_out` or `shell_out!`.
- Native IO using `TargetIO` classes.

### shell_out

Any implementations using `shell_out` is automatically Agentless Mode-capable, as the execution target dynamically changes between local and remote invocations.

### TargetIO

Update custom resources that use Ruby's built-in IO classes and methods to run in Agentless Mode by prefixing each IO call with the `TargetIO` namespace.

For example, to update Ruby's `IO.read` class to run in Agentless Mode, modify this:

```ruby
contents = IO.read(filename)
```

to:

```ruby
contents = TargetIO::IO.read(filename)
```

In Agentless Mode, `TargetIO` translates native Ruby IO calls so they can be executed on a remote node. When run locally in Agent Mode, it automatically passes operations to Ruby's native IO classes.

The following classes run the most commonly used IO calls:

- `TargetIO::Dir`
- `TargetIO::Etc`
- `TargetIO::File`
- `TargetIO::FileUtils`
- `TargetIO::HTTP`
- `TargetIO::IO`
- `TargetIO::Shadow`

{{< note >}}

The `TargetIO::HTTP` class auto detects if `curl` or `wget` are installed on the target node and channels HTTP-related requests through either one if they're installed.

{{< /note >}}
