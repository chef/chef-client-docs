+++
title = "Chef Infra resources"
linkTitle = "Resources"

[menu.agentless]
title = "Chef Infra resources"
identifier = "agentless/resources/overview"
parent = "agentless"
weight = 10
+++

This page lists Chef Infra resources that are supported for Agentless mode in Chef Infra Client 19 RC2.

## chef_data_bag

[chef_data_bag resource documentation](https://docs.chef.io/resources/chef_data_bag/)

Resource example:

```ruby
chef_data_bag 'data_bag' do
    action :create
end

chef_data_bag_item 'data_bag/id' do
    raw_data({
        "feature" => true
    })
end
```

Verified platforms:

- Ubuntu
- Linux

## chef_environment

[chef_environment resource documentation](https://docs.chef.io/resources/chef_environment/)

Resource example:

```ruby
chef_environment 'dev' do
    description 'Dev Environment'
    default_attributes({ "dev" => 1 })
end
```

Verified platforms:

- Ubuntu
- Linux

## cookbook_file

[cookbook_file resource documentation](https://docs.chef.io/resources/cookbook_file/)

Resource example:

```ruby
cookbook_file '/tmp/chef-repo/config.conf' do
    source 'config.conf'
    owner 'root'
    group 'root'
    mode '0644'
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## habitat_package

[habitat_package resource documentation](https://docs.chef.io/resources/habitat_package/)

Resource example:

```ruby
habitat_package 'core/httpd' do
    channel 'stable' # Channel from which to install
    version '2.4.51' # Optional: Specify version, or omit to install the latest version
    action :install # Action to install the package
end
```

Verified platforms:

- Ubuntu
- Linux

## habitat_service

[habitat_service resource documentation](https://docs.chef.io/resources/habitat_service/)

Resource example:

```ruby
habitat_service 'core/httpd' do
    action :unload # Stops and unloads the service
end
```

Verified platforms:

- Ubuntu
- Linux

## alternatives

[alternatives resource documentation](https://docs.chef.io/resources/alternatives/)

Resource example:

```ruby
alternatives 'python' do
    link '/usr/bin/python'
    action :remove
end
```

Verified platforms:

- Ubuntu
- Linux

## inspec_waiver

[inspec_waiver resource documentation](https://docs.chef.io/resources/inspec_waiver/)

Resource example:

```ruby
inspec_waiver 'web_server_security' do
    control 'security-123'
    expiration '2024-06-30'
    justification 'Waiver granted due to ongoing security patch deployment.'
    run_test true
    action :add
end
```

Verified platforms:

- Ubuntu
- Linux

## inspec_waiver_file_entry

[inspec_waiver_file_entry resource documentation](https://docs.chef.io/resources/inspec_waiver_file_entry/)

Resource example:

```ruby
inspec_waiver_file_entry 'web_server_security_waiver' do
    control 'security-123'
    expiration '2024-06-30'
    file_path '/etc/chef/inspec_waivers.yml'
    justification 'Waiver granted due to ongoing security patch deployment.'
    run_test true
    action :add
end
```
Verified platforms:

- Ubuntu
- Linux

## user

[user resource documentation](https://docs.chef.io/resources/user/)

Resource example:

```ruby
user 'ctest' do
    comment 'system guy'
    system true
    shell '/bin/false'
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_install

[selinux_install resource documentation](https://docs.chef.io/resources/selinux_install/)

Resource example:

```ruby
selinux_install 'selinux' do
    action :install
    packages %w(make policycoreutils selinux-policy selinux-policy-targeted libselinux-utils setools-console)
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_user

[selinux_user resource documentation](https://docs.chef.io/resources/selinux_user/)

Resource example:

```ruby
selinux_user 'ctest' do
    level 's0'
    range 's0'
    roles %w(sysadm_r staff_r)
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_login

[selinux_login resource documentation](https://docs.chef.io/resources/selinux_login/)

Resource example:

```ruby
selinux_login 'ctest' do
    user 'user_u'
    range 's0'
    action :manage
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_fcontext

[selinux_fcontext resource documentation](https://docs.chef.io/resources/selinux_fcontext/)

Resource example:

```ruby
selinux_fcontext '/tmp/foo.txt' do
    secontext 'samba_share_t'
    file_type 'a'
    action :add
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_permissive

[selinux_permissive resource documentation](https://docs.chef.io/resources/selinux_permissive/)

Resource example:

```ruby
selinux_permissive 'httpd_t' do
    action :add
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_module

[selinux_module resource documentation](https://docs.chef.io/resources/selinux_module/)

Resource example:

```ruby
selinux_module 'my_policy_module' do
    base_dir '/etc/selinux/local/'
    content <<-EOF
module custom_module 1.0;
echo 'Hello Test';
EOF
    action :remove
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_port

[selinux_port resource documentation](https://docs.chef.io/resources/selinux_port/)

Resource example:

```ruby
selinux_port '5678' do
    protocol 'tcp'
    secontext 'http_port_t'
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_state

[selinux_state resource documentation](https://docs.chef.io/resources/selinux_state/)

Resource example:

```ruby
selinux_state 'enforcing' do
    action :enforcing
end
```

Verified platforms:

- Ubuntu
- Linux

## selinux_boolean

[selinux_boolean resource documentation](https://docs.chef.io/resources/selinux_boolean/)

Resource example:

```ruby
selinux_boolean 'ssh_keysign' do
    value true
    persistent false # The change will not persist after a reboot
    action :set
end
```

Verified platforms:

- Ubuntu
- Linux

## rhsm_register

[rhsm_register resource documentation](https://docs.chef.io/resources/rhsm_register/)

Resource example:

```ruby
rhsm_register 'register_with_rhsm' do
    username 'chnadraredhat'
    password 'Dev@progress123'
    auto_attach true
    action :register
end
```

Verified platforms:

- Linux (redhat)

## rhsm_subscription

[rhsm_subscription resource documentation](https://docs.chef.io/resources/rhsm_subscription/)

Resource example:

```ruby
rhsm_subscription 'attach_subscription' do
    pool_id '2c94582e918fd1090191db3a9e083436'
    action :attach
end
```

Verified platforms:

- Linux (redhat)

## rhsm_repo

[rhsm_repo resource documentation](https://docs.chef.io/resources/rhsm_repo/)

Resource example:

```ruby
rhsm_repo 'rhel-9-server-rpms' do
    repo_name 'rhel-atomic-7-cdk-3.11-rpms'
    action :enable
end
```

Verified platforms:

- Linux (redhat)

## rhsm_errata

[rhsm_errata resource documentation](https://docs.chef.io/resources/rhsm_errata/)

Resource example:

```ruby
rhsm_errata 'apply_rhsa' do
    errata_id 'RHSA-2014:1293'
    action :install
end
```

Verified platforms:

- Linux (redhat)

## rhsm_errata_level

[rhsm_errata_level resource documentation](https://docs.chef.io/resources/rhsm_errata_level/)

Resource example:

```ruby
rhsm_errata_level 'RHSA-2014' do
    errata_level 'moderate'
    action :install
end
```

Verified platforms:

- Linux (redhat)

## ssh_known_hosts_entry

[ssh_known_hosts_entry resource documentation](https://docs.chef.io/resources/ssh_known_hosts_entry/)

Resource example:

```ruby
ssh_known_hosts_entry 'gitlab.com' do
    file_location '/etc/ssh/ssh_known_hosts'
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## swap_file

[swap_file resource documentation](https://docs.chef.io/resources/swap_file/)

Resource example:

```ruby
swap_file '/swapfile' do
    size 524 # Size in MB
    persist false
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## sysctl

[sysctl resource documentation](https://docs.chef.io/resources/sysctl/)

Resource example:

```ruby
sysctl 'net.ipv4.ip_forward' do
    value '1'
    action :apply
end
```

Verified platforms:

- Ubuntu
- Linux

## chef_container

[chef_container resource documentation](https://docs.chef.io/resources/chef_container/)

Resource example:

```ruby
chef_container 'my_container' do
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## notify_group

[notify_group resource documentation](https://docs.chef.io/resources/notify_group/)

Resource example:

```ruby
chef_sleep '10' do
    action :sleep
end

notify_group 'crude_stop_and_start' do
    notifies :sleep, 'chef_sleep[10]', :immediately
end
```

Verified platforms:

- Ubuntu
- Linux

## ohai

[ohai resource documentation](https://docs.chef.io/resources/ohai/)

Resource example:

```ruby
ohai 'reload' do
    plugin 'etc'
    action :reload
end
```

Verified platforms:

- Ubuntu
- Linux

## ohai_hint

[ohai_hint resource documentation](https://docs.chef.io/resources/ohai_hint/)

Resource example:

```ruby
ohai_hint 'ec2' do
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## package

[package resource documentation](https://docs.chef.io/resources/package/)

Resource example:

```ruby
package 'curl' do
    action :install
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

## reboot

[reboot resource documentation](https://docs.chef.io/resources/reboot/)

Resource example:

```ruby
reboot 'now' do
    action :reboot_now
    reason 'Cannot continue Chef run without a reboot.'
end
```

Verified platforms:

- Ubuntu
- Linux

## remote_file

[remote_file resource documentation](https://docs.chef.io/resources/remote_file/)

Resource example:

```ruby
remote_file '/etc/index.html' do
    mode '0755'
    action :create
    source 'https://www.google.com'
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

## ruby_block

[ruby_block resource documentation](https://docs.chef.io/resources/ruby_block/)

Resource example:

```ruby
ruby_block 'print_message' do
    block do
        puts 'This is a Ruby block in Chef!' # Custom Ruby code
    end
    action :run # Default action
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

## service

[service resource documentation](https://docs.chef.io/resources/service/)

Resource example:

```ruby
service 'cron' do
    action %i(enable start)
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

### Remarks

Use 'crond' for Linux.

## sudo

[sudo resource documentation](https://docs.chef.io/resources/sudo/)

Resource example:

```ruby
sudo 'webadmin_apache' do
    user 'root'
    commands ['/bin/systemctl restart httpd']
    nopasswd true
    action :create
end
```
Verified platforms:

- Ubuntu
- Linux
- Centos 9

## template

[template resource documentation](https://docs.chef.io/resources/template/)

Resource example:

```ruby
template '/tmp/ssh_knownn' do
    source '/Users/cprasad/.chef/chef-repo/cookbooks/cis_rhel_7_benchmark_v3.1.1/templates/default/ssh_known_hosts.erb' # 'index.html'
    mode '0644'
    local true
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

### Remarks

Require absolute path for source attribute.

## timezone

[timezone resource documentation](https://docs.chef.io/resources/timezone/)

Resource example:

```ruby
timezone 'UTC' do
    action :set
end
```

Verified platforms:

- Linux

## user_ulimit

[user_ulimit resource documentation](https://docs.chef.io/resources/user_ulimit/)

Resource example:

```ruby
user_ulimit 'tomcat' do
    filehandle_limit 8192
    filename 'tomcat_filehandle_limits.conf'
end
```

Verified platforms:

- Ubuntu
- Linux

## yum_repository

[yum_repository resource documentation](https://docs.chef.io/resources/yum_repository/)

Resource example:

```ruby
yum_repository 'rhel-repo' do
    reposdir '/tmp/'
    action :create
    make_cache false
end
```

Verified platforms:

- Linux

## owner

[owner resource documentation](https://docs.chef.io/resources/owner/)

Resource example:

```ruby
file '/etc/crontab' do
    mode '0600'
    owner 'root'
    group 'root'
end
```

Verified platforms:

- Ubuntu
- Linux

## perl

[perl resource documentation](https://docs.chef.io/resources/perl/)

Resource example:

```ruby
perl 'hello world' do
    code <<-EOH
print "Hello world! From Chef and Perl.";
EOH
end
```

Verified platforms:

- Ubuntu

## apt_package

[apt_package resource documentation](https://docs.chef.io/resources/apt_package/)

Resource example:

```ruby
apt_package 'tree' do
    action :install
end
```

Verified platforms:

- Ubuntu

## apt_preference

[apt_preference resource documentation](https://docs.chef.io/resources/apt_preference/)

Resource example:

```ruby
apt_preference 'curl' do
    pin 'version 7.68*'
    pin_priority 1001
end
```

Verified platforms:

- Ubuntu
- Linux

## apt_repository

[apt_repository resource documentation](https://docs.chef.io/resources/apt_repository/)

Resource example:

```ruby
apt_repository 'habitat' do
    uri 'https://bldr.habitat.sh/latest/debian/'
    components ['stable', 'main']
    distribution 'stable'
    key 'https://bldr.habitat.sh/gpg.pub'
    action :add
end
```

Verified platforms:

- Ubuntu
- Linux

## apt_update

[apt_update resource documentation](https://docs.chef.io/resources/apt_update/)

Resource example:

```ruby
# Ensure APT package cache is updated
apt_update 'update' do
    action :update
end

# Install a package using apt_package resource
apt_package 'nginx' do
    action :install
end
```

Verified platforms:

- Ubuntu
- Linux

## bash

[bash resource documentation](https://docs.chef.io/resources/bash/)

Resource example:

```ruby
bash 'Reload daemon' do
    code <<-EOH
systemctl daemon-reload
EOH
    action :nothing
end
```

Verified platforms:

- Ubuntu
- Linux

## breakpoint

[breakpoint resource documentation](https://docs.chef.io/resources/breakpoint/)

Resource example:

```ruby
breakpoint 'name' do
    action :break
end
```

Verified platforms:

- Ubuntu
- Linux

## chef_client_config

[chef_client_config resource documentation](https://docs.chef.io/resources/chef_client_config/)

Resource example:

```ruby
chef_client_config 'default' do
    # URL of your Chef Server
    chef_server_url 'https://your-chef-server/organizations/your-org'
    # Name of the node as recognized by the Chef Server
    node_name 'node-name'
    # Log file location
    log_location '/var/log/chef-client.log'
    # Log level for Chef Client
    log_level :info
    # Directory to store the configuration file
    config_directory '/etc/chef'
    action :nothing
end
```

Verified platforms:

- Ubuntu
- Linux

## chef_sleep

[chef_sleep resource documentation](https://docs.chef.io/resources/chef_sleep/)

Resource example:

```ruby
chef_sleep 'pause_for_30_seconds' do
    seconds 30
    action :sleep
end
```

Verified platforms:

- Ubuntu
- Linux

## cron

[cron resource documentation](https://docs.chef.io/resources/cron/)

Resource example:

```ruby
cron 'daily_script' do
    minute '0'
    hour '0'
    command '/tmp/local/bin/daily_script.sh'
    user 'root'
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## cron_access

[cron_access resource documentation](https://docs.chef.io/resources/cron_access/)

Resource example:

```ruby
cron_access 'allow_user' do
    user 'username' # Replace 'username' with the actual username
    action :allow # Default action is :allow, can be omitted if using default
end
```

Verified platforms:

- Ubuntu
- Linux

## cron_d

[cron_d resource documentation](https://docs.chef.io/resources/cron_d/)

Resource example:

```ruby
cron_d 'example_job' do
    minute '0'
    hour '2'
    day '*'
    month '*'
    weekday '*'
    command '/usr/bin/example_command'
    user 'root'
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## directory

[directory resource documentation](https://docs.chef.io/resources/directory/)

Resource example:

```ruby
directory '/tmp/chef-repo' do
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux

## execute

[execute resource documentation](https://docs.chef.io/resources/execute/)

Resource example:

```ruby
execute 'test_echo' do
    command 'echo "Target Mode Connected Successfully..!!"'
end
```

Verified platforms:

- Ubuntu
- Linux

## file

[file resource documentation](https://docs.chef.io/resources/file/)

Resource example:

```ruby
file '/etc/crontab' do
    mode '0600'
    owner 'root'
    group 'root'
end
```

Verified platforms:

- Ubuntu
- Linux

## git

[git resource documentation](https://docs.chef.io/resources/git/)

Resource example:

```ruby
git '/tmp/chef-repo' do
    repository 'https://github.com/chef/chef.git'
    revision 'main'
    action :sync
end
```

Verified platforms:

- Ubuntu
- Linux

## group

[group resource documentation](https://docs.chef.io/resources/group/)

Resource example:

```ruby
group 'developers' do
    action :remove
end
```

Verified platforms:

- Ubuntu
- Linux

## habitat_install

[habitat_install resource documentation](https://docs.chef.io/resources/habitat_install/)

Resource example:

```ruby
habitat_install 'install habitat' do
    bldr_url 'http://localhost'
    hab_version '1.5.50'
end
```

Verified platforms:

- Ubuntu
- Linux

## habitat_sup

[habitat_sup resource documentation](https://docs.chef.io/resources/habitat_sup/)

Resource example:

```ruby
# Configure and start the Habitat Supervisor
habitat_sup 'default' do
    action :run
    # Configuration options
    service 'default' # Specify the service name, which will be used for supervision
    ring 'default' # The name of the Habitat ring (cluster) to join
    topology 'leader' # Topology options: 'leader', 'standalone', or 'federation'
    gossip 'default' # The name of the gossip service
    # Set the configuration options (adjust as needed)
    config do
        {
            'peer' => 'default', # Example configuration option
            'listen' => '0.0.0.0:9631' # Example configuration option
        }
    end
end
```

Verified platforms:

- Ubuntu
- Linux

## hostname

[hostname resource documentation](https://docs.chef.io/resources/hostname/)

Resource example:

```ruby
hostname 'my-new-hostname' do
    action :set
end
```

Verified platforms:

- Ubuntu
- Linux

## http_request

[http_request resource documentation](https://docs.chef.io/resources/http_request/)

Resource example:

```ruby
# Make a GET request to fetch posts
http_request 'fetch_posts' do
    url 'https://jsonplaceholder.typicode.com/posts'
    action :get
    headers({
        'Accept' => 'application/json'
    })
    not_if { ::File.exist?('/tmp/posts_fetched') } # Only run if the file doesn't already exist
end

# Execute a command to create a file after fetching posts
execute 'create_post_fetch_file' do
    command 'touch /tmp/posts_fetched'
    action :run
    only_if 'curl -s https://jsonplaceholder.typicode.com/posts | grep "userId"'
end

# Make a POST request to create a new post
http_request 'create_post' do
    url 'https://jsonplaceholder.typicode.com/posts'
    action :post
    message({
        title: 'foo',
        body: 'bar',
        userId: 1
    }.to_json)
    headers({
        'Content-Type' => 'application/json',
        'Accept' => 'application/json'
    })
end
```

Verified platforms:

- Ubuntu
- Linux

## ifconfig

[ifconfig resource documentation](https://docs.chef.io/resources/ifconfig/)

Resource example:

```ruby
execute 'configure_network_interface' do
    command 'ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up'
    action :run
end
```

Verified platforms:

- Ubuntu
- Linux

## kernel_module

[kernel_module resource documentation](https://docs.chef.io/resources/kernel_module/)

Resource example:

```ruby
kernel_module 'udf' do
    load_dir '/etc/modprobe.d'
    action :disable
end
```

Verified platforms:

- Ubuntu
- Linux

## link

[link resource documentation](https://docs.chef.io/resources/link/)

Resource example:

```ruby
s_links = ['/usr/sbin/lsmod', '/usr/sbin/rmmod', '/usr/sbin/insmod', '/usr/sbin/modinfo', '/usr/sbin/modprobe', '/usr/sbin/depmod']
s_links.each do |files|
    link files.to_s do
        to '../bin/kmod'
    end
end
```

Verified platforms:

- Ubuntu
- Linux

## log

[log resource documentation](https://docs.chef.io/resources/log/)

Resource example:

```ruby
log "Testign Log Resources....!!!"
```

Verified platforms:

- Ubuntu
- Linux

## systemd_unit

[systemd_unit resource documentation](https://docs.chef.io/resources/systemd_unit/)

Resource example:

```ruby
systemd_unit 'my_custom_service.service' do
    content(
        {
            'Unit' => {
                'Description' => 'My Custom Service',
                'After' => 'network.target',
            },
            'Service' => {
                'ExecStart' => '/usr/bin/my_custom_script.sh',
                'Restart' => 'on-failure',
            },
            'Install' => {
                'WantedBy' => 'multi-user.target',
            },
        }
    )
    action [:create, :enable, :start]
end
```

Verified platforms:

- Ubuntu
- Linux

## locale

[locale resource documentation](https://docs.chef.io/resources/locale/)

Resource example:

```ruby
locale 'set system locale' do
    lang 'en_US.UTF-8'
end
```

Verified platforms:

- Ubuntu

## chef_acl

[chef_acl resource documentation](https://docs.chef.io/resources/chef_acl/)

Resource example:

```ruby
chef_acl '*/' do
    rights :all, :users => 'root'
    recursive true
    action :create
end
```

Verified platforms:

- Ubuntu
- Linux
- Centos 9

## script

[script resource documentation](https://docs.chef.io/resources/script/)

Resource example:

```ruby
script 'run_custom_script' do
    interpreter 'bash' # Specify a custom interpreter
    code "echo 'This is a custom script in Chef!'" # Custom script code
    action :run # Default action
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9.0

## subversion

[subversion resource documentation](https://docs.chef.io/resources/subversion/)

Resource example:

```ruby
subversion 'checkout_project_code' do
    repository "https://github.com/torvalds/linux.git"
    destination '/tmp/project'
    revision 'HEAD' # Check out revision 1234
    svn_info_args 'false'
    svn_arguments 'false'
    action :sync
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9
- CentOS 9

### Remarks

**Warning:** The subversion resource has known bugs and may not work as expected. For more information see Chef GitHub issues, particularly [#4050](https://github.com/chef/chef/issues/4050) and [#4257](https://github.com/chef/chef/issues/4257).

## chef_role

[chef_role resource documentation](https://docs.chef.io/resources/chef_role/)

Resource example:

```ruby
chef_role 'webserver' do
    description 'Role for web servers'
    default_attributes(
        'apache' => {
            'port' => 80
        }
    )
    env_run_lists(
        'default' => [
            'role[base]',
            'recipe[apache]'
        ]
    )
    ignore_failure true
    action :create
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## chef_client

[chef_client resource documentation](https://docs.chef.io/resources/chef_client/)

Resource example:

```ruby
chef_client 'example-client' do
    admin true # Optional: Make this client an API client
    complete true # Optional: Define the client completely
    ignore_failure false # Optional: Do not ignore failure by default
    source_key_path '/home/ubuntu/mohan.pub' # Path to the public key
    action :create # Default action, creates a client
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## habitat_config

[habitat_config resource documentation](https://docs.chef.io/resources/habitat_config/)

Resource example:

```ruby
# Step 1: Install Habitat
habitat_install 'install habitat' do
    bldr_url 'http://localhost'
    hab_version '1.5.50'
end

# Start the Habitat Supervisor if it's not running
execute 'start_habitat_supervisor' do
    command 'hab sup run'
    user 'root' # Make sure to run as root or as an appropriate user with permissions to start services
    environment({
        'PATH' => '/usr/local/bin:/usr/bin:/bin' # Set the PATH environment variable, if needed
    })
    action :run
    not_if 'pgrep -f hab-sup' # Prevent running the command if a Habitat Supervisor is already running
end

# Now apply the habitat config
habitat_config 'core.httpd' do
    config({
        worker_count: 4,
        http: {
            keepalive_timeout: 120
        }
    })
    remote_sup '127.0.0.1:9632' # Ensure the supervisor address is correct
    action :apply
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## chef_node

[chef_node resource documentation](https://docs.chef.io/resources/chef_node/)

Resource example:

```ruby
# Setting node attributes for a Chef run
node.override['example_attribute'] = 'example_value'

# You can use a chef_node resource after modifying the node attributes if needed.
chef_node 'example-node' do
    action :create
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## inspec_input

[inspec_input resource documentation](https://docs.chef.io/resources/inspec_input/)

Resource example:

```ruby
# Create the YAML file with content
file '/home/ubuntu/my_input_source.yaml' do
    content <<-EOH
key1: value1
key2: value2
EOH
    mode '0644'
    owner 'root'
    group 'root'
    action :create
    notifies :add, 'inspec_input[example_input]', :immediately
end

# Add the input to InSpec
inspec_input 'example_input' do
    input 'key1=value1,key2=value2'
    source '/home/ubuntu/my_input_source.yaml' # Path to the YAML file
    action :nothing # It will be triggered by the file resource
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## ksh

[ksh resource documentation](https://docs.chef.io/resources/ksh/)

Resource example:

```ruby
# Install ksh (KornShell)
package 'ksh' do
    action :install
end

# Now you can use the ksh resource
ksh 'hello world' do
    code <<-EOH
echo "Hello, world!"
echo "Current directory: " $PWD
EOH
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## csh

[csh resource documentation](https://docs.chef.io/resources/csh/)

Resource example:

```ruby
# Install csh package
package 'csh' do
    action :install
end

# Execute a C shell script
csh 'hello world' do
    code <<-EOH
echo "Hello from C shell!"
echo "Current directory: `pwd`"
EOH
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## python

[python resource documentation](https://docs.chef.io/resources/python/)

Resource example:

```ruby
# Ensure Python 3 is installed
package 'python3' do
    action :install
end

# Run a Python script using python3
python 'hello_world' do
    code <<-EOH
print("Hello, world! From Chef and Python.")
EOH
    action :run
    interpreter 'python3' # Specify python3 interpreter
end
```

Verified platforms:

- Ubuntu 24.04
- Linux Red Hat 9

## yum_package

[yum_package resource documentation](https://docs.chef.io/resources/yum_package/)

Resource example:

```ruby
yum_package 'httpd' do
    action :install
end
```

Verified platforms:

- Centos 9

### Remarks

supported on Linux platforms only

## yum_repository

[yum_repository resource documentation](https://docs.chef.io/resources/yum_repository/)

Resource example:

```ruby
yum_repository 'rhel-repo' do
    reposdir '/tmp/'
    action :create
    make_cache false
end
```

Verified platforms:

- Centos 9
- RHEL 8

### Remarks

supported on Linux platforms only

## snap_package

[snap_package resource documentation](https://docs.chef.io/resources/snap_package/)

Resource example:

```ruby
snap_package 'node' do
    version '16/stable'
    options 'classic'
    action :install
end
```

Verified platforms:

- Ubuntu 24.04

### Remarks

supported on Ubuntu platforms only

## freebsd_package

[freebsd_package resource documentation](https://docs.chef.io/resources/freebsd_package/)

Resource example:

```ruby
freebsd_package 'curl' do
    action :install
end
```

Verified platforms:

- FreeBSD 14

### Remarks

supported on FreeBSD platform only

## chef_group

[chef_group resource documentation](https://docs.chef.io/resources/chef_group/)

Resource example:

```ruby
# Create a group named 'developers' on the Ubuntu machine
chef_group 'developers' do
    action :create
end
```

Verified platforms:

- Ubuntu 24.04 and 18.04
- RHEL

## chef_organization

[chef_organization resource documentation](https://docs.chef.io/resources/chef_organization/)

Resource example:

```ruby
chef_organization 'organization_name' do
    full_name 'Organization Ltd.'
    action :create
end
```

Verified platforms:

- Ubuntu 24.04 and 18.04
- RHEL

## chef_user

[chef_user resource documentation](https://docs.chef.io/resources/chef_user/)

Resource example:

```ruby
chef_user 'john_doe' do
    display_name 'John Doe'
    admin true
    email 'john@example.com'
    password 'hashed_password_here'
    action :create
end
```

Verified platforms:

- Ubuntu 24.04 and 18.04
- RHEL
