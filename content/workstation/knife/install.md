+++
title = "Install Knife 19"

[menu.workstation]
title = "Install"
identifier = "workstation/knife/install"
parent = "workstation/knife"
weight = 20
+++

Knife 19 is included as a component of Chef Workstation 26 RC3, but you can also install it as a standalone package.
The Knife standalone installation doesn't include the Knife cloud provider plugins (knife-ec2, knife-google, knife-windows).
For that reason, Progress Chef recommends installing Chef Workstation, which includes the cloud provider plugins.

If you want to install Knife 19 as a standalone component, follow the steps below.

## Requirements

Knife 19 has the following requirements:

- Supported on Linux (Ubuntu 18.04+, CentOS 7+, RHEL 7+), macOS 10.15+, or Windows 10/Server 2016+
- Chef Habitat 1.6.0 or later installed
- Internet connectivity for package download and bootstrapping remote nodes
- SSH or WinRM to manage remote nodes

## Install Knife

To install the Knife 19 standalone package, follow these steps:

1. Install Knife 19:

    ```sh
    sudo hab pkg install chef/knife --channel unstable --binlink --force
    ```

1. Optional: After installation, verify Knife 19 is working correctly:

    ```sh
    # Check Knife version
    knife --version
    ```

## Configure Knife

### Initial setup

To configure Knife to connect to Chef Infra Server, run the following command:

```sh
# Generate knife configuration
knife configure
```

You can also manually configure this connection:

1. Create the `~/.chef/credentials` file:

    ```sh
    mkdir -p ~/.chef
    touch ~/.chef/credentials
    ```

1. Add your Chef Infra Server credentials to the `~/.chef/credentials` file:

    ```toml
    [default]
    chef_server_url = "https://chef-server.example.com/organizations/org-name"
    client_name = "username"
    client_key = "~/.chef/user-key.pem"
    ```

For more information, see the [Knife setup documentation](https://docs.chef.io/workstation/knife_setup/).

### Configure self-signed certificates

To use self-signed certificates, fetch and verify the Chef Infra Server certificates:

1. Fetch the Chef Infra Server SSL certificates:

    ```sh
    knife ssl fetch
    ```

1. Verify the certificate:

    ```sh
    knife ssl check
    ```

For more information, see the following:

- [`knife ssl fetch`](https://docs.chef.io/workstation/knife_ssl_fetch/)
- [`knife ssl check`](https://docs.chef.io/workstation/knife_ssl_check/)

## Troubleshooting

### Permission errors during installation

Change the ownership of Habitat directories to your user account:

```sh
sudo chown -R $(whoami) /hab
```

### Missing plugins after standalone installation

The standalone Knife installation doesn't include the Knife plugins.
To get the Knife plugins, install Chef Workstation, which includes Knife and the Knife plugins.

### SSL certificate errors

If you get SSL certificate errors:

- In a development environment, you can skip SSL verification:

  ```sh
  echo "ssl_verify_mode :verify_none" >> ~/.chef/knife.rb
  ```

- Fetch and verify the Chef Infra Server certificates:

  ```sh
  knife ssl fetch && knife ssl check
  ```

## More information

- [Knife setup documentation](https://docs.chef.io/workstation/knife_setup/)
- [`knife ssl fetch` documentation](https://docs.chef.io/workstation/knife_ssl_fetch/)
- [`knife ssl check` documentation](https://docs.chef.io/workstation/knife_ssl_check/)
