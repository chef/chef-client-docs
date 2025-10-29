# Chef Agentless (Target Mode) with Habitat — Complete End-to-End Guide

A single, self-contained guide that shows **where** to run each command, how to get and export the Habitat auth token, how to obtain and apply the free Chef license key (string), how to create `target_credentials`, and how to execute an example test recipe (`apply.rb`) via **Habitat** using **Target Mode (agentless)**. This document reflects your workflow: **you always run Chef through** `hab pkg exec chef/chef-infra-client` (you do not invoke `chef-client` directly).

# 1. Overview & assumptions

* Host: the machine where you run commands (workstation, management server, CI runner). This is where **Habitat** and the Chef Habitat package run.
* Target: the remote system that Chef will configure over SSH (no Chef client required on target).
* You use the Habitat package: `chef/chef-infra-client` and **always** run Chef with `hab pkg exec chef/chef-infra-client chef-client -z -t <Target> <recipe>`.

# 2. Quick summary — where to run what

* Install Habitat → **run on host**
* Get HAB_AUTH_TOKEN → **retrieve from**  `https://bldr.habitat.sh/#/profile` and **export on host** (before installing packages and before the first run)
* Install Chef package via `hab pkg install` → **run on host**
* Obtain Chef license key (string) → **get from**  `https://licensing.chef.io` and **store on host**
* Create `~/.chef/target_credentials` and `~/.chef/licenses.yaml` and `~/.chef/apply.rb` → **on host**
* Execute recipe via Habitat → **on host**

# 3. Pre-flight checklist

Before you start, ensure:

* Host is Linux x86-64 (Ubuntu/RHEL/Amazon Linux recommended).
* Host has internet access (to bldr.habitat.sh and `http://licensing.chef.io`) OR appropriate packages/artifacts available offline.
* You have SSH access (network and credentials) to targets.
* You have (or can generate) a Habitat auth token and a Chef free license key string.

# 4. Step 1 — Install Habitat (`hab`) (on host)

Run once on the host:
`curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash`

Verify:
`hab --version`
Expected example output:
`hab 1.x.x/xxxx`

# 5. Step 2 — Get & `export HAB_AUTH_TOKEN` (on host)
* You need an auth token to pull packages from Habitat Builder.

* 1. Open: https://bldr.habitat.sh/#/profile
* 2. Sign in (Chef/Progress account or GitHub).
* 3. In **Profile → Personal Access Tokens** generate a token and copy it.

Export it in your shell **before** installing the Chef package and before the first run:
```
export HAB_AUTH_TOKEN="paste-your-token-here"
# persist it for future sessions (optional)
echo 'export HAB_AUTH_TOKEN="paste-your-token-here"' >> ~/.bashrc
source ~/.bashrc
```

Verify:
`echo "$HAB_AUTH_TOKEN"`

* Important: Export HAB_AUTH_TOKEN before hab pkg install if the package is private or the builder requires auth. You should also ensure it’s present before executing a first hab pkg exec run that may fetch artifacts.

# 6. Step 3 — Install Chef Infra Client via Habitat (on host)
Install the Chef Habitat package and create binlinks if you want convenience:


`sudo hab pkg install chef/chef-infra-client --binlink --force --channel unstable`
* --channel unstable uses latest unstable builds (adjust to your channel policy).
* --binlink creates symlinks for convenience (you still must run via hab pkg exec per your workflow; binlink is optional).
* --force overwrites previous links.

Verify package exists:
`hab pkg list | grep chef-infra-client`

# 7. Step 4 — Obtain & apply free Chef license key (on host)
Chef 19+ requires license acceptance via a license key string (you will receive a key string — there is no `license.pem` by default in your flow).

1. Get a free license key: https://licensing.chef.io/ → “Get a Free License”

2. You’ll receive a license **key string** by email (example: `abcd-1234-efgh-5678`).

Store it in `~/.chef/licenses.yaml`:

`# ~/.chef/licenses.yaml`
`license_key: "abcd-1234-efgh-5678"`

Alternatively you can set an environment variable (temporary):
`export CHEF_LICENSE_KEY="abcd-1234-efgh-5678"`

**Chef infra client must see that license key (or accept license) before running.** Using `licenses.yaml` in `~/.chef` is recommended for reproducibility.

# 8. Step 5 — Create target_credentials (on host)
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

* Use exact target names in square-bracket sections (e.g., `['Ubuntu']`) — **the name used with** `-t` **must match**.

* `sudo = true` is necessary if the user is non-root and you need privilege escalation (your test touches `/etc/crontab` so root required).

* `key_files` can be a path or quoted path. Ensure key file permissions (600) on host.

# 9. Step 6 — Prepare apply.rb test recipe (on host)
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

# 10. Step 7 — Run Chef Agentless (Target Mode) via Habitat (on host)
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

# 11. Verification & expected output
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

# 12. Troubleshooting & common fixes
* `hab: command not found` → Habitat not installed on host. Re-run install script.

* `No HAB_AUTH_TOKEN set` → Export `HAB_AUTH_TOKEN` before installing packages or executing runs.
* `Package not found` or `permission denied` → Ensure HAB_AUTH_TOKEN is correct and you have access to builder or use public packages.
* `License required `→ Add `~/.chef/licenses.yaml` with `license_key` entry or export `CHEF_LICENSE_KEY`.
* `SSH authentication failed` → Verify `host`, `user`, `key_files`, key permissions, and network reachability.
* `Target not found` → The name in `-t <Target>` must exactly match the `['Name']` section in `target_credentials`.
* `Permission denied (sudo)` → Ensure `sudo = true `in credentials for non-root user or use `user = 'root'`.
* `Recipe file not found` → Use absolute path to `apply.rb` or run command from the directory containing `apply.rb`.

# 13. Safety & alternative safe-test recipe
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

# 14. Appendix — full `apply.rb` content (copy/paste)

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

**Final quick reference — essential commands**
```
# 1. Install Habitat (host)
curl https://raw.githubusercontent.com/habitat-sh/habitat/main/components/hab/install.sh | sudo bash
# 2. Export HAB_AUTH_TOKEN (host) — BEFORE install or first run
export HAB_AUTH_TOKEN="your_token_here"
echo 'export HAB_AUTH_TOKEN="your_token_here"' >> ~/.bashrc
# 3. Install Chef Infra Client via Habitat (host)
sudo hab pkg install chef/chef-infra-client --binlink --force --channel unstable
# 4. Place license key (host) ~/.chef/licenses.yaml
# Example content:
# license_key: "abcd-1234-efgh-5678"
# 5. Create target_credentials (host) ~/.chef/target_credentials
# Example:
# ['Ubuntu']
# host = '192.168.0.251'
# user = 'ubuntu'
# sudo = true
# key_files = '~/.ssh/key-pair.pem'
# 6. Run recipe via Habitat (host)
cd ~/.chef
hab pkg exec chef/chef-infra-client chef-client -z -t Ubuntu apply.rb
```
