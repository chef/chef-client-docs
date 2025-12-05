+++
title = "Configure Chef Workstation and its components"

[menu.workstation]
title = "Configure Workstation"
identifier = "workstation/config"
parent = "workstation"
weight = 30
+++

## Configure Chef Workstation

Configure Chef Workstation for your environment:

```sh
chef-cli config
```

## Configure Knife

To configure Knife to connect to Chef Infra Server, run the following command:

```sh
knife configure
```

### Manually configure Knife

You can also manually configure this connection:

1. Create the `~/.chef/credentials` file:

    ```sh
    mkdir -p ~/.chef
    touch ~/.chef/credentials
    ```

1. Add your Chef Infra Server credentials to the `~/.chef/credentials` file. For example:

    ```toml
    [default]
    chef_server_url = "https://chef-server.example.com/organizations/org-name"
    client_name = "node_name"
    client_key = "~/.chef/ceriticate_file.pem"
    ```

## Configure self-signed certificates

To use self-signed certificates, fetch and verify the Chef Infra Server certificates:

1. Fetch the Chef Infra Server SSL certificates:

    ```sh
    knife ssl fetch
    ```

1. Verify the certificates:

    ```sh
    knife ssl check
    ```

## More information

- [Knife setup documentation](https://docs.chef.io/workstation/knife_setup/)
- [`knife ssl fetch` documentation](https://docs.chef.io/workstation/knife_ssl_fetch/)
- [`knife ssl check` documentation](https://docs.chef.io/workstation/knife_ssl_check/)
