---
title: Cloud PKI CA Expiration
description: Learn how to renew a certificate authority (CA) in Microsoft Cloud PKI to maintain continuous certificate issuance.
ms.date: 01/31/2026
ms.topic: how-to
---

# Microsoft Cloud PKI CA expiration

When a Certificate Authority (CA) in Cloud PKI approaches its expiration date, take action to ensure continued certificate issuance and avoid service disruptions. This article explains how to renew your CA and update SCEP certificate profiles in Microsoft Intune. Follow these steps to maintain secure device connectivity and uninterrupted access to corporate resources.

Renewing a CA is a customer-specific action. Microsoft can't automatically update your CA or SCEP profiles.

If you need assistance, contact Microsoft support or your account representative.

## Action required: Cloud PKI Certificate Authority expiring soon - Create new issuing CA and update SCEP profiles to prevent service disruption

### User impact

If you don't take action, SCEP certificate profiles that use the expiring Certificate Authority (CA) can't issue new certificates after the CA's expiration date. This condition might result in device connectivity loss, inability to access corporate resources, or failed certificate-based authentication for affected users.

## Action needed

To avoid service disruption, Intune administrators must create a new issuing CA and update all SCEP certificate profiles that reference the expiring CA.

- Use the same *Root CA Source* as the expiring CA.
- Ensure all CA properties match the expiring CA, especially Extended Key Usages and Key Sizes.

### Update SCEP Certificate Profiles

1. After creating the new Issuing CA, copy the SCEP URI from its properties.
1. For each SCEP certificate profile using the soon‑to‑expire CA, update the profile to reference the new Issuing CA's SCEP URI.
1. Replace the existing (expiring) Issuing CA SCEP URI with the new SCEP URI copied in step 1.

> [!NOTE] 
> - Don't add an additional SCEP URI. Cloud PKI doesn't support multiple SCEP URIs within a single SCEP certificate profile.
> - Updating the SCEP URI on a profile will not trigger a cert re-issuance.

## Additional Diagnostics

Review all SCEP certificate profiles to confirm they reference the new CA.

For more information on managing CAs and SCEP profiles, refer to the Intune documentation.

## Coming Soon

Cloud PKI will soon provide the ability to renew an existing CA. Be sure to look for this upcoming feature at https://aka.ms/IntuneWhatsNew.
