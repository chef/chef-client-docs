+++
title = "About Knife"

[menu.workstation]
title = "Knife"
identifier = "workstation/knife/about"
parent = "workstation/knife"
weight = 10
+++

Knife 19, now integrated into Chef Workstation 26 RC3, represents a significant milestone in Chef's migration to Habitat-based packaging.
As the essential command-line interface for Chef Infra Server interactions, Knife 19 is completely repackaged as a Habitat package, providing enhanced dependency management, improved plugin architecture, and streamlined distribution across enterprise environments.

This release delivers critical functionality for node management, cookbook operations, and infrastructure bootstrapping while maintaining full compatibility with existing Chef Infra Server deployments.
Knife 19 serves as the primary interface for Chef practitioners to manage their infrastructure-as-code workflows efficiently.

## What's new in RC3

The RC3 release of Knife 19 introduces several architectural and functional enhancements:

### Habitat-based architecture

- Knife is packaged independently as a Habitat package for improved modularity and dependency isolation
- Clean separation of dependencies ensures consistent execution across different environments
- Ruby gem-based plugins integrate seamlessly within the Habitat package structure

### Chef Infra Client 19 bootstrap support

- Native support for Chef Infra Client 19 Enterprise Edition (`chef-ice`) as the default bootstrap product
- Purpose-built installation scripts optimized for RC3 pre-release deployment scenarios
- Secure package distribution through pre-signed URLs for controlled access to release candidate packages
- Unified bootstrap workflow supporting both Linux and Windows target nodes

### Plugin ecosystem enhancement

- Validated plugins for major cloud providers (AWS, GCP) and Windows environments
- Framework prepared for additional cloud provider plugins in upcoming releases
- Existing knife workflows remain fully functional with enhanced underlying infrastructure

## What's the difference between Knife and Knife 19?

Knife 19 is a major architectural update that migrates from traditional packaging to Habitat-based distribution.
This update focuses on improved dependency management and enhanced plugin architecture for enterprise environments.

Key changes in Knife 19:

- Knife 19 is released as a Habitat package for better modularity and dependency isolation
- Enhanced plugin management with better cloud provider support
- Optimized for enterprise deployment scenarios with improved security

The way you use Knife remains largely unchanged. Existing knife commands and workflows continue to work with the enhanced underlying infrastructure.

## Supported cloud provider plugins

Knife 19 includes plugins for major cloud providers to automate node provisioning and management:

### knife-ec2 (Amazon Web Services)

Manage EC2 instances directly from the knife command line:

- Create and bootstrap EC2 instances with Chef Infra Client
- Configure security groups and networking settings
- Apply AWS resource tags for compliance and cost tracking
- Support for multiple AWS regions and instance types

### knife-google (Google Cloud Platform)

Provision and manage Google Compute Engine instances:

- Create instances across GCP projects and zones
- Support for custom and public machine images
- Configure VPC networks and firewall rules
- Integrate with GCP resource hierarchies

### knife-windows (Windows Management)

Manage Windows nodes using WinRM protocol:

- Bootstrap Windows servers with Chef Infra Client
- Execute PowerShell commands remotely
- Manage Chef Infra Client service on Windows systems
- Support for Active Directory domain-joined systems

{{< note >}}

The `knife windows cert install` command has a known limitation where it may fail to import `.pfx` certificates with the error `CertUtil: The requested operation is not supported.`

{{< /note >}}

## Chef Infra Client 19 bootstrap architecture

### Default bootstrap configuration

Knife 19 implements a fundamental shift in bootstrap behavior, now defaulting to Chef Infra Client 19 Enterprise Edition (`chef-ice`) as the standard bootstrap product.
This change reflects Chef's strategic direction toward enterprise-focused solutions while maintaining backward compatibility for existing deployments.

Key configuration changes:

- **Default product**: `config[:bootstrap_product]` now defaults to `chef-ice`
- **URL requirement**: Pre-signed URLs are mandatory for Chef Infra Client 19 installations in this RC3 release

### Custom installation script architecture

Since Chef Infra Client 19 hasn't yet reached general availability (GA), standard distribution mechanisms (Omnitruck API, Download Portal) don't currently support this version.
The RC3 release provides custom installation scripts specifically engineered for pre-release deployment scenarios.

Installation script features:

- **Intelligent platform detection**: Automatic identification of target system architecture and operating system
- **Secure package retrieval**: Pre-signed URL-based package downloading with integrity verification
- **Optimized installation workflow**: Streamlined installation process designed specifically for RC3 packages
- **Cross-platform support**: Unified installation experience across Linux and Windows platforms
- **Error handling**: Comprehensive error detection and reporting for troubleshooting

### Pre-Signed URL Distribution

The RC3 release utilizes a secure distribution model through pre-signed URLs, ensuring controlled access to release candidate packages while maintaining security best practices.

#### Linux Installation Script

**URL**: `install.sh`

`https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=IDDVNrOTeKZnc%2Bxa9611MkK%2BZ2o%3D&Expires=1780533412`

#### Windows Installation Script

**URL**: `install.ps1`

`https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.ps1?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=4hQ0Ve5Rcd63oHZyTI7r%2FX9KltA%3D&Expires=1780533421?AWSAccessKeyId=AKIAW4FPVFT6C42N3U6R&Signature=pcqpblewgc5x%2FLxSHqlcQBhqpU0%3D&Expires=1778909040`

**Important**: These pre-signed URLs are specific to the RC3 release cycle and will be replaced by standard download portal URLs upon general availability release.

## Bootstrap Chef Infra Client

### Bootstrap Chef Infra Client 19

To bootstrap Chef Infra Client 19, run the following command:

```sh
knife bootstrap <IP_ADDRESS> \
  -U <USERNAME> \
  -p <PASSWORD> \
  -N <NODE_NAME> \
  --sudo \
  --bootstrap-url "<PRE_SIGNED_INSTALLATION_SCRIPT_URL>"
```

The `--bootstrap-url` parameter installs a prerelease version of Chef Infra CLient that's distributed through pre-signed URLs.

### Bootstrap Chef Infra Client 18

To bootstrap Chef Infra Client 18.x, run the following command:

```sh
knife bootstrap <IP_ADDRESS> \
  -U <USERNAME> \
  -p <PASSWORD> \
  -N <NODE_NAME> \
  --sudo \
  --bootstrap-product chef
```

The `--bootstrap-product chef` option directs knife to use Chef Infra Client 18.x from standard download channels.

### Create and bootstrap an AWS EC2 instance

The Knife EC2 plugin integrates with AWS EC2, allowing you to create and provision an EC2 instance.

To create an EC2 instance and bootstrap Infra Client onto it, run the following command:

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
  --aws-tag owner=<OWNER_EMAIL> \
  --aws-tag application=<APPLICATION_NAME> \
  --aws-tag environment=<ENVIRONMENT> \
  --aws-tag cost-center=<COST_CENTER> \
  --aws-tag expiration=<EXPIRATION_DATE> \
  --bootstrap-url "<BOOTSTRAP_URL>"
```

Options:

- `-I <AMI_ID>`: Amazon Machine Image (AMI) ID for the EC2 instance (for example, `ami-0c02fb55956c7d316`)
- `-f <INSTANCE_TYPE>`: Instance type specification (for example, `t3.medium`, `m5.xlarge`, `c5.4xlarge`)
- `-N <NODE_NAME>`: Chef node name for identification within Chef Infra Server
- `-U <SSH_USERNAME>`: SSH username appropriate for the selected AMI (for example, `ec2-user`, `ubuntu`, `centos`)
- `--ssh-identity-file <SSH_KEY_FILE>`: Path to SSH private key for secure authentication
- `-g <SECURITY_GROUP_ID>`: Security group ID for network access control (for example, `sg-0a1b2c3d4e5f67890`)
- `--region <AWS_REGION>`: AWS region for instance deployment (for example, `us-east-1`, `eu-west-1`)
- `--subnet <SUBNET_ID>`: VPC subnet ID for network placement (for example, `subnet-0123456789abcdef0`)
- `--aws-tag <KEY>=<VALUE>`: Resource tags for AWS compliance and management (repeatable)
- `--bootstrap-url <BOOTSTRAP_URL>`: RC3-specific installation script URL

### Create and bootstrap a GCP instance

The knife-google plugin integrates with GCP Compute Engine.

```sh
knife google server create <INSTANCE_NAME> \
  --gce-project <GCP_PROJECT_ID> \
  --gce-zone <GCP_ZONE> \
  --gce-machine-type <MACHINE_TYPE> \
  --gce-image <IMAGE_NAME> \
  --gce-image-project <IMAGE_PROJECT> \
  --image-os-type linux \
  --connection-user <SSH_USERNAME> \
  --ssh-identity-file ~/.ssh/<SSH_KEY_FILE> \
  --connection-port 22 \
  --connection-protocol ssh \
  --gce-network <VPC_NETWORK> \
  --gce-subnet <SUBNET_NAME> \
  --gce-tags <TAG1>,<TAG2>,<TAG3> \
  --bootstrap-url "<BOOTSTRAP_URL>"
```

Options:

- `--gce-project <GCP_PROJECT_ID>`: Google Cloud project ID for resource organization
- `--gce-zone <GCP_ZONE>`: GCP availability zone for instance placement (for example, `us-central1-a`, `europe-west1-b`)
- `--gce-machine-type <MACHINE_TYPE>`: Instance machine type and resource specification (for example, `e2-standard-4`, `n1-highmem-8`)
- `--gce-image <IMAGE_NAME>`: Operating system image name from GCP image repositories (for example, `ubuntu-2204-jammy-v20251102`)
- `--gce-image-project <IMAGE_PROJECT>`: Source project containing the OS image (for example, `ubuntu-os-cloud`, `centos-cloud`)
- `--image-os-type`: Operating system type classification (`linux` or `windows`)
- `--connection-user <SSH_USERNAME>`: SSH username for secure connection establishment
- `--ssh-identity-file <SSH_KEY_FILE>`: Path to SSH private key for authentication
- `--connection-protocol`: Communication protocol specification (`ssh` or `winrm`)
- `--gce-network <VPC_NETWORK>`: VPC network name for instance connectivity
- `--gce-subnet <SUBNET_NAME>`: Subnet specification within the designated VPC
- `--gce-tags <TAG1>,<TAG2>`: Instance tags for organization and firewall rules (comma-separated)
- `--bootstrap-url <BOOTSTRAP_URL>`: RC3 installation script URL

### Knife-Windows

The knife-windows plugin provides specialized capabilities for Windows-based infrastructure management through WinRM protocol integration.

#### Windows-specific requirements

- You must enable and configure Windows Remote Management on target systems
- Windows Firewall must allow WinRM traffic (ports 5985 for HTTP, 5986 for HTTPS)
- Bootstrap operations require administrative privileges on target Windows systems
- Execution policy must allow remote script execution

WinRM configuration commands (execute on target Windows systems):

```ps1
# Enable WinRM service
winrm quickconfig -q

# Configure WinRM for remote access
Enable-PSRemoting -Force

# Configure firewall rules
New-NetFirewallRule -DisplayName "WinRM HTTP" -Direction Inbound -Protocol TCP -LocalPort 5985 -Action Allow
```

## Bootstrap Chef Infra Client 19 in an air-gapped environment

To bootstrap Chef Infra Client 19 in an air-gapped environment, follow these steps:

1. On an internet-connected computer, download the Chef Infra Client 19 packages from the pre-signed URLs and save it to an internal repository that's  accessible to target nodes in the secure environment. For example:

    ```sh
    wget https://chef-hab-migration-tool-bucket.s3.amazonaws.com/Release-Candidate-3/workstation/install.sh?AWSAccessKeyId=AKIAW4FPVFT6PA6EXTHQ&Signature=IDDVNrOTeKZnc%2Bxa9611MkK%2BZ2o%3D&Expires=1780533412 \
      -O /var/www/internal-repo/chef/rc3/install.sh
    ```

1. Modify installation scripts to reference internal package locations and repositories.

    ```sh
    sed -i 's|https://chef-hab-migration-tool-bucket.s3.amazonaws.com|<INTERNAL_REPOSITORY>|g' \
      /var/www/internal-repo/chef/rc3/install.sh
    ```

    Replace `<INTERNAL_REPOSITORY>` with your air-gapped repository, for example: `https://internal-repo.example.com`.

1. Verify package integrity and implement internal signature validation processes.
1. Bootstrap Chef Infra Client 19 using the `--bootstrap-url` parameter to point to internal resources.

### Implementation example

```sh
# Step 1: Download packages to internal repository server


# Step 2: Customize installation script for internal package locations


# Step 3: Execute bootstrap with internal URL
knife bootstrap <IP_ADDRESS> \
  -U <USERNAME> \
  -p <PASSWORD> \
  -N <NODE_NAME> \
  --sudo \
  --bootstrap-url "https://internal-repo.example.com/chef/rc3/install.sh"
```

## Command compatibility and backward support

### Preserved functionality

All knife plugins maintain full backward compatibility with existing command structures and parameters:

- **No breaking changes**: All existing command syntax remains functional
- **Parameter compatibility**: Existing parameter flags and options work unchanged
- **Workflow preservation**: Current operational procedures require no modification
- **Script compatibility**: Existing automation scripts continue to function normally

### New requirements for Chef Infra Client 19

The only addition required for Chef Infra Client 19 deployments is the `--bootstrap-url` parameter:

- **Mandatory parameter**: Required only for Chef Infra Client 19 bootstrap operations
- **Legacy support**: Not required for Chef Infra Client 18.x and earlier versions
- **Plugin independence**: Each plugin handles the parameter appropriately for its platform

Plugin compatibility:

- **knife-ec2**: All existing AWS operations are preserved with enhanced Chef Infra Client 19 support
- **knife-google**: Complete GCP functionality is maintained with RC3 bootstrap integration
- **knife-windows**: Full Windows management capabilities are retained with improved PowerShell integration

Known limitations:

- `knife windows cert install` may fail to import `.pfx` certificates generated by `knife windows cert generate`, commonly because of the following error: `CertUtil: The requested operation is not supported.`
