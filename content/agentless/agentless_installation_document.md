# Chef Agentless (Target Mode) with Habitat Complete End-to-End Guide

# This document provides a simplified, end-to-end guide to configure and `run Chef Infra Client 19 RC2 in Agentless` (Target Mode) using`Habitat (hab)` for managing`remote systems`.

## 1. Step 1 Install Chef Infra Client (on Host)

Before starting, ensure **`Chef Infra Client 19 RC2`** is installed on your host system.
Follow the official installation guide provided by Chef:

**Official Installation Guide:**
[Install Chef Infra Client RC2 using a native installer](https://docs.chef.io/client/rc2/install/installer)

Once installation is complete, continue with the following steps

## 2. Step 2 Create target_credentials (on host)

Create `~/.chef/target_credentials` (this is the inventory of agentless targets). Example:
```
['Ubuntu']
host = '192.168.0.251'
user = 'ubuntu'
sudo = true
key_files = '~/.ssh/key-pair.pem'
['RHEL']
host = '192.168.0.252'
user = 'root'
password = 'rootpass'
```

Notes:

* Use exact target names in square bracket sections (e.g., `['Ubuntu']`) **the name used with** `-t` **must match**.

* `sudo = true` is necessary if the user is non-root and you need privilege escalation (your test touches `/etc/crontab` so root required).

* `key_files` can be a path or quoted path. Ensure key file permissions (600) on host.

# 3. Step 3 Prepare apply.rb test recipe (on host)
Create `~/.chef/apply.rb` with the test resources below. This recipe will:

* create `/tmp/chef-repo`

* run a simple echo to confirm connectivity

* ensure `/etc/crontab` ownership/permissions (requires root)

**File:** `~/.chef/apply.rb`

```
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
 **WARNING:** Changing `/etc/crontab` permissions can affect cron system behavior. For cautious testing, see the safe-test alternative in section 13.

# 4. Step 4 Run Chef Agentless (Target Mode) via Habitat (on host)
From your .chef directory, with `HAB_AUTH_TOKEN` exported and the license key available:

```
cd ~/.chef
hab pkg exec chef/chef-infra-client chef-client -z -t Ubuntu apply.rb
```
Replace `Ubuntu` with the target name you defined in `target_credentials`.

**What this does:**

* `hab pkg exec chef/chef-infra-client` runs Chef inside the Habitat package environment.
* `chef-client -z` runs in Chef-Zero/local mode.
* `-t Ubuntu` tells Chef to use the `['Ubuntu']` entry in` ~/.chef/target_credentials`.
* `apply.rb` is the recipe executed on the remote target over SSH.

# 5. Step 5 Verification & expected output
A successful run should show something like:
```
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
Check remote target for artifacts:

```
# on host, to confirm via ssh example:
ssh -i ~/.ssh/key-pair.pem ubuntu@192.168.0.251 'ls -ld /tmp/chef-repo && echo "crontab perms:" && stat -c "%a %U %G" /etc/crontab'
```

# 6. Troubleshooting & common fixes
* `SSH authentication failed`  Verify `host`, `user`, `key_files`, key permissions, and network reachability.
* `Target not found`  The name in `-t <Target>` must exactly match the `['Name']` section in `target_credentials`.
* `Permission denied (sudo)` Ensure `sudo = true `in credentials for non-root user or use `user = 'root'`.
* `Recipe file not found`  Use absolute path to `apply.rb` or run command from the directory containing `apply.rb`.

# 7. Safety & alternative safe-test recipe
**Safety:** The included `apply.rb` modifies `/etc/crontab` permissions. If you prefer a non-invasive test (safe for CI and production-like systems), use this alternate `apply_safe.rb` that avoids touching system files:
```
# ~/.chef/apply_safe.rb

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

Run it the same way:

```hab pkg exec chef/chef-infra-client chef-client -z -t Ubuntu apply_safe.rb```

# 8. Appendix full `apply.rb` content (copy/paste)

```
# ~/.chef/apply.rb
# Simple test recipe for Chef Target Mode (Agentless).
# Resources:
#  - create a test directory under /tmp
#  - run a simple echo command to confirm Target Mode connectivity
#  - tighten permissions on /etc/crontab (requires sudo/root)
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
  # Do not change content; this resource only ensures permissions/ownership.
  # Warning: Changing crontab permissions may affect cron behavior on the target.
end
```

# 9. Final quick reference essential commands**
```
# 1. Create target_credentials (host) ~/.chef/target_credentials
# Example:
# ['Ubuntu']
# host = '192.168.0.251'
# user = 'ubuntu'
# sudo = true
# key_files = '~/.ssh/key-pair.pem'
# 2. Run recipe via Habitat (host)
cd ~/.chef
hab pkg exec chef/chef-infra-client chef-client -z -t Ubuntu apply.rb
```
