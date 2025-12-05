+++
title = "Bootstrap nodes with Knife"

[menu.workstation]
title = "Bootstrap nodes"
identifier = "workstation/knife/bootstrap"
parent = "workstation/knife"
weight = 40
+++

Bootstrapping installs Chef Infra Client on a target system and configures it to communicate with a Chef Infra Server.

## Prerequisites

Before bootstrapping nodes:

- [Configure Knife 19](/workstation/config/#configure-knife)
- For Chef Infra Client 18 or earlier, [configure your Progress Chef license with Knife](license)

Chef Infra Client 19 RC3 doesn't require a license.

Before bootstrapping Windows nodes:

- Enable and configure Windows Remote Management (WinRM):

  ```powershell
  winrm quickconfig -q
  ```

- Set the execution policy to allow remote script execution:

  ```powershell
  Enable-PSRemoting -Force
  ```

- Configure Windows Firewall to allow WinRM traffic on port 5985 (HTTP) or 5986 (HTTPS)

## Bootstrap Chef Infra Client 19 RC3 on Linux

To bootstrap Chef Infra Client 19, run the following command:

```sh
knife bootstrap <IP_ADDRESS> \
  -U <USERNAME> \
  -p <PASSWORD> \
  -N <NODE_NAME> \
  --sudo \
  --bootstrap-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=IDDVNrOTeKZnc%2Bxa9611MkK%2BZ2o%3D&Expires=1780533412"
```

Replace the following:

- `<IP_ADDRESS>` with the node's IP address
- `<USERNAME>` with the SSH username
- `<PASSWORD>` with the SSH password
- `<NODE_NAME>` with a unique node name

The `--bootstrap-url` parameter installs a prerelease version of Chef Infra Client that's distributed through pre-signed URLs.

## Bootstrap Chef Infra Client 19 RC3 on Windows

To bootstrap a Windows node, run the following command:

```powershell
knife bootstrap <IP_ADDRESS> \
  -o winrm \
  -U <USERNAME> \
  -P <PASSWORD> \
  -N <NODE_NAME> \
  --winrm-port <PORT_NUMBER> \
  --bootstrap-url "https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.ps1?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=4hQ0Ve5Rcd63oHZyTI7r%2FX9KltA%3D&Expires=1780533421"
```

Replace the following:

- `<IP_ADDRESS>` with the IP address of the Windows node
- `<USERNAME>` with the WinRM username
- `<PASSWORD>` with the WinRM password
- `<NODE_NAME>` with the Chef node name
- `<PORT_NUMBER>` with the WinRM communication port (default: `5985`)

To use HTTPS for WinRM on port 5986, use the `--winrm-ssl` option.

## Bootstrap Chef Infra Client 18

To bootstrap Chef Infra Client 18.x, run the following command:

```sh
knife bootstrap <IP_ADDRESS> \
  -U <USERNAME> \
  -p <PASSWORD> \
  -N <NODE_NAME> \
  --sudo \
  --bootstrap-product chef
```

Replace the following:

- `<IP_ADDRESS>` with the node's IP address
- `<USERNAME>` with the SSH username
- `<PASSWORD>` with the SSH password
- `<NODE_NAME>` with a unique node name

The `--bootstrap-product chef` option directs Knife to use Chef Infra Client 18.x from standard download channels.

## Bootstrap an AWS EC2 instance

The Knife EC2 plugin integrates with AWS EC2 to create and provision EC2 instances.

To create an EC2 instance and bootstrap Chef Infra Client, run the following command:

```sh
knife ec2 server create \
  --sudo \
  -I <AMI_ID> \
  --ssh-key <SSH_KEY_NAME> \
  -f <INSTANCE_TYPE> \
  -N <NODE_NAME> \
  -U <SSH_USERNAME> \
  --ssh-identity-file ~/.ssh/<SSH_KEY_FILE> \
  -g <SECURITY_GROUP_ID> \
  --region <AWS_REGION> \
  --subnet <SUBNET_ID> \
  --aws-tag <TAG_KEY>=<TAG_VALUE>
  --bootstrap-url "<BOOTSTRAP_URL>"
```

Replace the following:

- `<AMI_ID>` with the Amazon Machine Image ID for the EC2 instance, for example, `ami-0c02fb55956c7d316`
- `<SSH_KEY_NAME>` with the Name of your AWS SSH key pair
- `<INSTANCE_TYPE>` with the Instance type specification, for example, `t3.medium`, `m5.xlarge`, or `c5.4xlarge`
- `<NODE_NAME>` with the Chef Infra node name for identification within Chef Infra Server
- `<SSH_USERNAME>` with the SSH username for the selected AMI, for example, `ec2-user`, `ubuntu`, or `centos`
- `<SSH_KEY_FILE>` with the Path to SSH private key for authentication
- `<SECURITY_GROUP_ID>` with the Security group ID for network access control, for example, `sg-0a1b2c3d4e5f67890`
- `<AWS_REGION>` with the AWS region for instance deployment, for example, `us-east-1` or `eu-west-1`
- `<SUBNET_ID>` with the VPC subnet ID for network placement, for example, `subnet-0123456789abcdef0`
- `<TAG_KEY>=<TAG_VALUE>` with the Resource tags for AWS compliance and management (repeatable). For example, `environment=production`
- `<BOOTSTRAP_URL>` with the Installation script URL for RC3:

  For Windows nodes:

  ```text
  https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.ps1?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=4hQ0Ve5Rcd63oHZyTI7r%2FX9KltA%3D&Expires=1780533421
  ```

  For Linux nodes:

  ```text
  https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=IDDVNrOTeKZnc%2Bxa9611MkK%2BZ2o%3D&Expires=1780533412
  ```

## Bootstrap a GCP Compute Engine instance

The knife-google plugin integrates with GCP Compute Engine to create and provision GCP instances.

To create a GCP instance and bootstrap Chef Infra Client:

```sh
knife google server create <INSTANCE_NAME> \
  --gce-project <GCP_PROJECT_ID> \
  --gce-zone <GCP_ZONE> \
  --gce-machine-type <MACHINE_TYPE> \
  --gce-image <IMAGE_NAME> \
  --gce-image-project <IMAGE_PROJECT> \
  --image-os-type <OPERATING_SYSTEM> \
  --connection-user <SSH_USERNAME> \
  --ssh-identity-file ~/.ssh/<SSH_KEY_FILE> \
  --connection-port 22 \
  --connection-protocol <PROTOCOL> \
  --gce-network <VPC_NETWORK> \
  --gce-subnet <SUBNET_NAME> \
  --gce-tags <TAG1>,<TAG2>,<TAG3> \
  --bootstrap-url "<BOOTSTRAP_URL>"
```

Replace the following:

- `<INSTANCE_NAME>` with the Name for the GCP instance
- `<GCP_PROJECT_ID>` with the Google Cloud project ID
- `<GCP_ZONE>` with the GCP availability zone, for example, `us-central1-a` or `europe-west1-b`
- `<MACHINE_TYPE>` with the Instance machine type, for example, `e2-standard-4` or `n1-highmem-8`
- `<IMAGE_NAME>` with the Operating system image name, for example, `ubuntu-2204-jammy-v20251102`
- `<IMAGE_PROJECT>` with the Source project containing the OS image, for example, `ubuntu-os-cloud` or `centos-cloud`
- `<OPERATING_SYSTEM>` with the Operating system type: `linux` or `windows`
- `<SSH_USERNAME>` with the SSH username
- `<SSH_KEY_FILE>` with the Filename of your SSH private key
- `<PROTOCOL>` with the Communication protocol: `ssh` or `winrm`
- `<VPC_NETWORK>` with the VPC network name
- `<SUBNET_NAME>` with the Subnet name within the VPC
- `<TAG1>,<TAG2>,<TAG3>` with the Comma-separated instance tags for organization and firewall rules (optional)
- `<BOOTSTRAP_URL>` with the Installation script URL:

  For Windows nodes:

  ```text
  https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.ps1?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=4hQ0Ve5Rcd63oHZyTI7r%2FX9KltA%3D&Expires=1780533421
  ```

  For Linux nodes:

  ```text
  https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=IDDVNrOTeKZnc%2Bxa9611MkK%2BZ2o%3D&Expires=1780533412
  ```

## Bootstrap Chef Infra Client 19 in an air-gapped environment

You can bootstrap Chef Infra Client 19 in an air-gapped environment.
The following are example steps for configuring the install scripts in an air-gapped environemnt.

1. On an internet-connected computer, download the Chef Infra Client 19 installation scripts and save them to an internal repository that's accessible to your target nodes. For example:

   ```sh
   wget https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh \
     -O /var/www/internal-repo/chef/rc3/install.sh

   wget https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.ps1 \
     -O /var/www/internal-repo/chef/rc3/install.ps1
   ```

1. Modify the installation scripts to reference your internal package locations. For example:

   ```sh
   sed -i 's|https://chef-hab-migration-tool-bucket.s3.amazonaws.com|<INTERNAL_REPOSITORY>|g' \
     /var/www/internal-repo/chef/rc3/install.sh

   sed -i 's|https://chef-hab-migration-tool-bucket.s3.amazonaws.com|<INTERNAL_REPOSITORY>|g' \
     /var/www/internal-repo/chef/rc3/install.ps1
   ```

   Replace `<INTERNAL_REPOSITORY>` with your internal repository URL, for example, `https://internal-repo.example.com`.

1. Bootstrap Chef Infra Client 19 using the `--bootstrap-url` parameter to point to your internal resources:

   ```sh
   knife bootstrap <IP_ADDRESS> \
     -U <USERNAME> \
     -p <PASSWORD> \
     -N <NODE_NAME> \
     --sudo \
     --bootstrap-url "https://internal-repo.example.com/chef/rc3/install.sh"
   ```

## More information

- [Chef Infra Client 18.x bootstrap documentation](https://docs.chef.io/install_bootstrap/)
- [Knife CLI documentation](https://docs.chef.io/workstation/knife/)
