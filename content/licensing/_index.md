+++
title = "Chef Infra Client licensing"
linkTitle = "Licensing"

[menu.licensing]
title = "Overview"
identifier = "licensing/overview"
parent = "licensing"
weight = 10
+++

This document provides a comprehensive guide on the three types of licenses available for Infra Client: free, trial, and commercial. The content covers details about:

- The license types
- Steps to obtain a license
- Terms of use
- Limitations
- User experience across different license statuses
- Product messaging
- Enforcement rules
- Troubleshooting details

## License types

Infra Client offers three main types of licenses. These are described in the following sections.

### Free license

- **Description:** A no-cost license with access to essential features. This is intended for smaller environments.
- **Limitations:** Restricted by the number of allowed nodes (10).
- **Support:** Community support channels only. There is no access to dedicated or premium support.

### Trial license

- **Description:** A full-featured, temporary license for evaluating the product.
- **Limitations:** Valid for 30 days with unrestricted features.
- **Support:** Limited support during the trial period; access to online resources but no premium support.

### Commercial license

- **Description:** A paid license for production use, offering full access to features and premium support.
- **Limitations:** Bound by purchased duration and node count.
- **Support:** Includes dedicated support with Service Level Agreements (SLAs), security updates, and ongoing maintenance.

## Terms of use

Each license type includes specific terms governing its usage and scope:

- **Free license:** Non-commercial use with a node limit. This is suitable for small-scale or personal setups.
- **Trial license:** Full-feature access for evaluation. The trial is valid for 30 days.
- **Commercial license:** Full production use, with restrictions based on the purchased node count and duration.

## Limitations of each license

| License type       | Limitations                                       |
|--------------------|---------------------------------------------------|
| Free license       | Limited by node count. For non-commercial use.        |
| Trial license      | 30-day usage limit. Full feature access for evaluation. |
| Commercial license | Limited by purchased duration and node count.     |

## User experience based on license status

For details on the different user experience based on the license status, refer to the following sections.

### Normal usage

- All features operate without restrictions.
- Users have access to full functionality according to their license type.

### When a license is about to expire

- Expiration warnings appear in the Command Line Interface (CLI), reminding the user of the impending expiration.
- **Trial and commercial license:** Warnings appear one week before the expiration date, with a countdown of the days left and encouraging renewal/upgrade to a commercial license.

### When a license expires

- **Trial license:** Full access is disabled. Users are prompted to upgrade to a commercial license.
- **Commercial license:** Users are required to renew to maintain full functionality.

### When the license node limit is exhausted

- A warning appears in the CLI indicating that the node limit has been reached.
- **Free license:** Users cannot proceed with additional nodes beyond the allowed limit.
- **Commercial license:** An exhausted node warning appears, but users can continue usage.

## Product messaging and behavior exposure

For details on the different product messaging and behavior exposure based on the license status, refer to the following sections.

### Free license

- No expiration messages unless approaching the node limit.
- Node limit warning appears when the user exceeds the node limit.

### Trial license

- Expiration warnings begin one week before the trial end date, with a countdown of the number of days left.
- Node limit warnings may appear if the trial license encounters a node restriction.

### Commercial license

- Expiration warnings appear one month before the license expiration date to ensure timely renewal.
- A node limit warning appears when the user exceeds the node limit.

## Enforcement rules and impact on users

Each license enforces specific rules:

- **Free license:** Enforces node count limitations. Errors appear if an attempt is made to exceed the limit and additional nodes are not recognized.
- **Trial license:** All features are accessible but restricted to 30 days. Upon expiration, users are prompted to upgrade to a commercial license.
- **Commercial license:** Validates node limits and duration (as purchased). Renewal is required upon expiration to avoid any restrictions.
