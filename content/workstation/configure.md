+++
title = "Configure Chef Workstation and its components"

[menu.workstation]
title = "Configure"
identifier = "workstation/config"
parent = "workstation"
weight = 30
+++

This page describes how to configure Chef Workstation and Knife to connect to Chef Infra Server.

## Configure Chef Workstation

To configure Chef Workstation for your environment:

```sh
chef-cli config
```

## Configure Knife

Knife requires configuration to connect to Chef Infra Server.
You can configure Knife automatically or manually.

### Configure Knife automatically

To configure Knife to connect to Chef Infra Server:

```sh
knife configure
```

This command prompts you for your Chef Infra Server credentials and creates the necessary configuration files.

### Configure Knife manually

To manually configure Knife to connect to Chef Infra Server:

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
   client_key = "~/.chef/certificate_file.pem"
   ```

   Replace the following:

   - `https://chef-server.example.com/organizations/org-name`: Your Chef Infra Server URL and organization name
   - `username`: Your Chef Infra Server username
   - `~/.chef/certificate_file.pem`: Path to your client certificate file

## Configure self-signed certificates

If you've configured Chef Infra Server with self-signed certificates, fetch and verify them:

1. Fetch the Chef Infra Server SSL certificates:

   ```sh
   knife ssl fetch
   ```

1. Verify the certificates:

   ```sh
   knife ssl check
   ```

## Next step

- [Add a Chef license](license)

## More information

- [Knife setup documentation](https://docs.chef.io/workstation/knife_setup/)
- [`knife ssl fetch` documentation](https://docs.chef.io/workstation/knife_ssl_fetch/)
- [`knife ssl check` documentation](https://docs.chef.io/workstation/knife_ssl_check/)
