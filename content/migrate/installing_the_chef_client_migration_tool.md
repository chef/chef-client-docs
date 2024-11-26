+++
title = "Installing the Chef Client Migration Tool"
linkTitle = "Installing the Chef Client Migration Tool"

[menu.migrate]
title = "Installing the Chef Client Migration Tool"
identifier = "migrate/installing_the_chef_client_migration_tool"
parent = "migrate"
weight = 11
+++

To install the migration tool, first download the package from the URL provided by Chef using `wget` or `curl`. On Linux:

```sh
wget -O chef-migration-tool.v1.tar.gz "https://bucket.s3.amazonaws.com/BUCKETNAME/FILENAME.tar.gz?Signature=SIGNATURESTRING&AWSAccessKeyId=IFTHEREISONE"
```

Or:

```sh
curl $args -s -f -H Date:"${date}" -H Authorization:"${authorization}" https://s3.amazonaws.com"${path/to/file}"
```

Then, extract the zipped file to a temporary folder:

```sh
tar -xvf chef-migration-tool.v1.tar.gz -C /path/to/folder
```

Lastly, run the migration using the online flags listed below:

- `--download.url` with the location given by Chef to download the Chef 19 RC1 Client. If this is not supplied, this is the default Chef download API.
- `--license.key` with the license key for the download URL.
- `--fresh_install` (optional) to re-install a previous installation or when no previous Chef Client install exists.

```sh
./chef-migrate apply online --download.url <URL> --license.key <KEY>
./chef-migrate apply online --license.key f5567204-f2d2-43b2-82a8-6359acfa3fb8 --fresh_install
```

Optionally, you can verify that the `\opt` directory (formerly the Omnibus installation directory) has symbolic links to the new, actual RC1 Infra Client in `\hab\pkgs\chef\chef-infra-client\19.0.6`.

Verify that the system path is set to point to the RC1 client:

```sh
echo $PATH (Linux)
Get-ChildItem Env: (Windows)
```

## Using Docker Desktop to test the download

Because the migration tool is only being released initially for the Linux x86_64 architecture, we are providing steps for you to use Docker Desktop (or a similar local container host) to practice using the migration tool with different combinations so that the desired flags can be automated.

First, pull a container like `ubuntu:latest` from Docker Hub and run it from a command shell with:

```sh
docker run -it ubuntu:latest
```

This presents you with a command prompt on the container (typically like `sh#`).  In another shell, copy your TAR file into the container with:

```sh
docker cp .\migration-tools_Linux_x86_64.tar.gz loving_jennings:/tmp
```

In the original shell window, go to where the `.tar.gz` folder was copied (`/tmp`), and extract it as above.
