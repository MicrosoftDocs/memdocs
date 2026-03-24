---
title: Cloud PKI CA Expiration
description: Learn how to renew a certificate authority (CA) in Microsoft Cloud PKI to maintain continuous certificate issuance.
ms.date: 01/31/2026
ms.topic: how-to
---

# Microsoft Cloud PKI CA expiration

When a Cloud PKI issuing certification authority (CA) approaches its expiration date, Microsoft Intune administrators must take action to maintain certificate issuance and avoid service disruption. This article describes the steps to create a new issuing CA and update SCEP certificate profiles.

> [!IMPORTANT]  
> Renewing or replacing a CA is a customer-managed action. Microsoft can't automatically update your Cloud PKI CA or associated SCEP certificate profiles.

If you need assistance, contact Microsoft Support or your account representative.

## User impact

If you take no action, SCEP certificate profiles that reference the expiring CA stop issuing new certificates after the CA expires. Devices and users might experience:

- Loss of Wi‑Fi, VPN, or email connectivity  
- Inability to access corporate resources  
- Failed certificate‑based authentication  

These impacts are consistent with known Cloud PKI expiring CA behavior.

## Action needed

To avoid service disruption, create a new Cloud PKI issuing CA and update all SCEP certificate profiles that reference the expiring CA.

### 1. Create a new issuing CA

When you create the replacement issuing CA:

- Use the same *Root CA Source* as the expiring CA.  
- Make sure all CA properties match the existing CA, including:
  - Extended Key Usages (EKUs)  
  - Key sizes  

### 2. Update SCEP certificate profiles

After you create the new issuing CA:

1. Copy the **SCEP URI** from the CA properties.  
1. Replace the old SCEP URI with the new one for each SCEP certificate profile that references the expiring CA.

> [!NOTE]
> - Don't add more SCEP URIs. Cloud PKI doesn't support multiple SCEP URIs in a single SCEP certificate profile.  
> - Updating the SCEP URI doesn't trigger certificate re‑issuance.

## More diagnostics

To confirm configuration:

- Review all SCEP certificate profiles to verify they reference the new issuing CA.  
- For Cloud PKI and SCEP guidance, see [Overview of Microsoft Cloud PKI for Microsoft Intune](index.md).

## Coming soon

Cloud PKI will soon support **renewing an existing CA** directly. For updates, see [What's new in Microsoft Intune](../intune-service/fundamentals/whats-new.md).
