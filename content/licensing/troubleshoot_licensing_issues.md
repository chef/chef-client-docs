+++
title = "Troubleshoot Licensing Issues"
linkTitle = "Troubleshoot Licensing Issues"

[menu.licensing]
title = "Troubleshoot Licensing Issues"
identifier = "licensing/troubleshoot"
parent = "licensing"
weight = 12
+++

Refer to the following sections for details on troubleshooting licensing issues.

## License is Not Entitled to Use Infra

This error occurs when the license key set with Chef Infra is not entitled to use Chef Infra. Each license key is associated with one or more Chef products.

To troubleshoot:
- Run the `chef-client license list` command to view the products your key is entitled to.
- If Chef Infra is not listed, set a license key that is entitled to Chef Infra.

Refer to the Chef Licensing documentation for more information on setting appropriate entitlements.

## Unable to Connect to the Licensing Server

Chef Infra requires communication with the Chef licensing service or a user-deployed Chef Local License Service to validate the license key. If it cannot connect, check the following possible causes:

- **Network connectivity:** Verify that the machine running Chef Infra has proper network connectivity and can reach the Chef licensing service or the Chef Local License Service. Ensure that firewalls and network settings are not blocking access.
- **Service availability:** If you are using a user-deployed Chef Local License Service, confirm that it is properly configured and operational. Any misconfigurations in the local license service can lead to connection issues.
- **URL configuration:** If using a Chef Local License Service, confirm that the server URL is correctly configured:
  - If it is configured via the `CHEF_LICENSE_SERVER` environment variable, verify the URL set in the environment variable.
  - If it is configured using the `--chef-license-server` CLI option, reset the URL with the same option, if needed.
- **Logs and debugging:** Use the `--log-level` debug option in Chef Infra to check the detailed logs. Check the URL that Chef Infra is attempting to connect to for troubleshooting clues.

If the issue persists, contact the Chef Customer Success or Support Team for assistance.

## Invalid File Format Version

Chef licensing data is stored in the `$HOME/.chef/licenses.yaml` file. This error may indicate an unsupported or invalid file format version in the `licenses.yaml` file.

To resolve:

- Restore the `licenses.yaml` file to its original state or ensure it has the latest supported file format version.

## License File Contents are Corrupted

Corruption of the `$HOME/.chef/licenses.yaml` file (where Chef licensing data is stored) can result in errors.

To troubleshoot:

- Restore the contents of the `licenses.yaml` file to the original state to correct any corruption.

## Support Contact

For any licensing issues, contact [chef-sales@progress.com](mailto:chef-sales@progress.com) with your license details, error logs, and a description of the issue.
