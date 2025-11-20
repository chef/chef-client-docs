+++
title = "Chef Infra Agentless Mode example"

[menu.agentless]
title = "Agentless Mode example"
identifier = "agentless/example"
parent = "agentless"
weight = 20
+++

This document provides a simplified, end-to-end guide to configure and run
Chef Infra Client 19 RC3 in Agentless (Target Mode) using Habitat (`hab`)
for managing remote systems.

## Prerequisites

- [Chef Infra Client is installed](/install/)
- Your `HAB_AUTH_TOKEN` is exported
- a valid Progress Chef license key

## Create a target credentials file

Create a target credentials file (`~/.chef/target_credentials`) that defines connection settings for each node.

For example:

```toml
['TARGET_NODE_1']
host = '<IP_ADDRESS_OR_FQDN>'
user = '<USERNAME>'
sudo = true
key_files = '~/.ssh/key-pair.pem'

['TARGET_NODE_2']
host = '<IP_ADDRESS_OR_FQDN>'
user = 'root'
password = '<PASSWORD>'
```

For more information, see the [target credentials file documentation](/agentless/).

## Retrieve Secrets from a Hashicorp Vault

You may want to set and retrieve secrets from your Vault. You can update your target_credentials file to enable that

```toml
default_secrets_provider = {
  name = 'hashicorp-vault',
  endpoint = 'http://127.0.0.1:8200',
  token = 'hvs.some_token_goes_here'
}

['Ubuntu']
host = '<IP_ADDRESS_OR_FQDN>'
user = '<USERNAME>'
sudo = true
password = { secret = 'myapp', field = 'password' }
# key_files = '~/.ssh/key-pair.pem'

```

## Create the test recipe

On the host, create a test recipe file (`~/.chef/apply.rb`) with the test resources below.

{{< foundation_tabs tabs-id="test-agentless-mode-recipe" >}}
  {{< foundation_tab active="true" panel-link="apply-recipe" tab-text="Test recipe">}}
  {{< foundation_tab panel-link="apply-safe-recipe" tab-text="Safe test recipe" >}}
{{< /foundation_tabs >}}

{{< foundation_tabs_panels tabs-id="test-agentless-mode-recipe" >}}
{{< foundation_tabs_panel active="true" panel-id="apply-recipe" >}}

This recipe:

- creates the `/tmp/chef-repo` directory
- executes `echo` to confirm connectivity
- sets `/etc/crontab` ownership and permissions. This requires root privileges.

**WARNING:** Changing `/etc/crontab` permissions can affect cron system behavior.
For a safer alternative, run the [safe test recipe](#apply-safe-recipe).

```ruby
# ~/.chef/apply.rb
# Simple test recipe for Chef Target Mode (Agentless).

directory '/tmp/chef-repo' do
  action :create
end

execute 'test_echo' do
  # Use single quotes inside echo to avoid shell quoting issues
  command "echo 'Target Mode Connected Successfully..!!'"
end

file '/etc/crontab' do
  mode '0600'
  owner 'root'
  group 'root'
  # Note: This resource only enforces ownership/permissions, not content.
end
```

{{< /foundation_tabs_panel >}}

{{< foundation_tabs_panel panel-id="apply-safe-recipe" >}}

This alternate `apply.rb` that avoids touching system files.

This recipe:

- creates the `/tmp/chef-repo` directory
- executes `echo` and saves the output to a text file
- sets ownership and permissions in a temp file.

```ruby
# ~/.chef/apply.rb

directory '/tmp/chef-repo' do
  action :create
end

execute 'test_echo' do
  command "echo 'Target Mode Connected Successfully..!!' > /tmp/target_mode_test.txt"
  creates '/tmp/target_mode_test.txt'
end

file '/tmp/target_mode_marker' do
  content "Target Mode ran at #{Time.now}\n"
  mode '0644'
  owner 'root'
  group 'root'
end
```

{{< /foundation_tabs_panel >}}
{{< /foundation_tabs_panels >}}

## Run Agentless using Local Mode

Sometimes you just want to connect to your node and have it execute a single recipe or a whole cookbook.

Ensure you have your target_credentials configured for your target node

```toml
['Ubuntu_2404']
host = '<IP_ADDRESS_OR_FQDN>'
user = '<USERNAME>'
sudo = true
key_files = '~/.ssh/key-pair.pem'
```

Now you can call into your node and pass it your recipe to execute

```sh
chef-client -z -t Ubuntu_2404 /chef-repo/my-cookbooks/cookbook1.rb
```

## Verify the output from Local Mode

You should see output similar to this:

```sh
Converging 1 resources
Recipe: @recipe_files::/root/.chef/chef-repo/cookbooks/cis_rhel_7_benchmark_v3.1.1/recipes/test2.rb
  * subversion[checkout_project_code] action sync (up to date)
Running handlers:
Running handlers complete
Infra Phase complete, 0/1 resources updated in 20 seconds
```

## Run Chef Agentless using Habitat

From your `.chef` directory, with `HAB_AUTH_TOKEN` exported and the license key available:

```sh
cd ~/.chef
hab pkg exec chef/chef-infra-client chef-client -z -t <TARGET_NODE> apply.rb
```

Replace `<TARGET_NODE>` with the target name defined in the `target_credentials` file. For example, `TARGET_NODE_1`.

Chef Infra Client executes the `apply.rb` recipe in local mode (`chef-client -z`) against the remote target (`-t <TARGET_NODE>`) over SSH using the credentials defined in `~/.chef/target_credentials`.

## Verify the output

A successful Infra Client run returns something like this:

```sh
Starting Chef Infra Client, version 19.x.x
[Target Mode] Connecting to target: Ubuntu (192.168.0.251)
Converging 3 resources
Recipe: /root/.chef/apply.rb
  * directory[/tmp/chef-repo] action create (up to date)
  * execute[test_echo] action run
    - execute echo 'Target Mode Connected Successfully..!!'
  * file[/etc/crontab] action create (up to date)
Running handlers:
Running handlers complete
Infra Phase complete, 0/3 resources updated in 12 seconds
```

You can SSH into the remote target from the host and get details about the directory and file permissions. For example:

```sh
# on host, to confirm through ssh example:
ssh -i ~/.ssh/key-pair.pem ubuntu@192.168.0.251 'ls -ld /tmp/chef-repo && echo "crontab perms:" && stat -c "%a %U %G" /etc/crontab'
```

## Run Chef Agentless using a Chef Server

In a number of instances, you'll want to use your existing investments in cookbooks already loaded on your Chef Server.
Here we take a different approach and update your credentials file, NOT the target_credentials file.

You'll note that we're mixing chef-client and knife here. We do this for a couple of reasons. First,
it makes it much easier to have only one settings file that both clients can use. Secondly, when we
call a `knife.rb` file, the client automatically discovers and uses the credentials file which can happily
now contain our target node details.

```sh
# nano ~/.chef/credentials

[default]
client_name       = 'foo'
client_key        = '/root/.chef/foo.pem'
chef_server_url   = 'https://nodes.example.com/organizations/chef-org'

['Ubuntu_2404']
host = '<IP_ADDRESS_OR_FQDN>'
user = '<USERNAME>'
sudo = true
key_files = '~/.ssh/key-pair.pem'

transport_protocol = 'ssh'
```

Now you need to update your `knife.rb` file so both knife and Chef Infra Client can use it.

```sh
# Path to your Chef repository
current_dir = File.dirname(__FILE__)

# Logging
log_level                :info
log_location             STDOUT

# User credentials
node_name                "my_spiffy_computer"   # Your Chef node
client_key               "#{current_dir}/my_spiffy_computer.pem"  # Path to your private key

# Chef Server URL
chef_server_url          "https://chef.example.com/organizations/myorg"

# Cookbook path
cookbook_path            ["#{current_dir}/../cookbooks"]

# SSL verification (optional, often disabled in test setups)
ssl_verify_mode          :verify_none
```

The next step is to use knife to verify your node is listed and update cookbooks as necessary

```ssh
knife node list
knife cookbook upload **your_cookbook**
knife node run_list add **node_name 'recipe[your_cookbook]'**
```

Finally, you can run your chef-client in target mode and have it run the cookbooks you just uploaded

```sh
# using Hab
hab pkg exec chef/chef-infra-client chef-client -c ~/.chef/knife.rb -t Ubuntu_2404

# using Chef-client directly
chef-client -c ~/.chef/knife.rb -t Ubuntu_2404
```

## Troubleshooting

- `SSH authentication failed`

  Verify `host`, `user`, and `key_files` properties in the target credentials file, and verify key permissions and network availability.

- `Target not found`

  The name in `-t <TARGET>` must exactly match a target defined in the `target_credentials` file.

- `Permission denied (sudo)`

  For a non-root user, set `sudo = true` in the target credentials file, or use `user = 'root'`.

- `Recipe file not found`

  Use absolute path to `apply.rb` or run command from the directory containing `apply.rb`.
