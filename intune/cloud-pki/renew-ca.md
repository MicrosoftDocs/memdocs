---
title: Cloud PKI CA Expiration
description: Learn how to renew a certificate authority (CA) in Microsoft Cloud PKI to maintain continuous certificate issuance.
ms.date: 01/31/2026
ms.topic: how-to
---

# Microsoft Cloud PKI CA expiration

When a Microsoft Cloud PKI issuing certification authority (CA) approaches its expiration date, Intune administrators must take action to maintain certificate issuance and avoid service disruption. This article describes the steps to create a new issuing CA and update SCEP certificate profiles.

> [!IMPORTANT]  
> Renewing or replacing a CA is a customer‑managed action. Microsoft can't automatically update your Cloud PKI CA or associated SCEP certificate profiles.

If you need assistance, contact Microsoft Support or your account representative.

## User impact

If no action is taken, SCEP certificate profiles that reference the expiring CA will stop issuing new certificates after the CA expires. Devices and users may experience:

- Loss of Wi‑Fi, VPN, or email connectivity  
- Inability to access corporate resources  
- Failed certificate‑based authentication  

These impacts are consistent with known Cloud PKI expiring CA behavior.

## Action needed

To avoid service disruption, create a new Cloud PKI issuing CA and update all SCEP certificate profiles that reference the expiring CA.

### 1. Create a new issuing CA

When creating the replacement issuing CA:

- Use the same *Root CA Source* as the expiring CA.  
- Ensure all CA properties match the existing CA, including:
  - Extended Key Usages (EKUs)  
  - Key sizes  

### 2. Update SCEP certificate profiles

After you create the new issuing CA:

1. In the CA properties, copy the **SCEP URI**.  
2. For each SCEP certificate profile referencing the expiring CA, replace the old SCEP URI with the new one.

> [!NOTE]
> - Don't add more SCEP URIs. Cloud PKI doesn't support multiple SCEP URIs in a single SCEP certificate profile.  
> - Updating the SCEP URI doesn't trigger certificate re‑issuance.

## More diagnostics

To confirm configuration:

- Review all SCEP certificate profiles to verify they reference the new issuing CA.  
- For Cloud PKI and SCEP guidance, see [Overview of Microsoft Cloud PKI for Microsoft Intune](index.md).

## Coming soon

Cloud PKI will soon support **renewing an existing CA** directly. Watch for updates at:  [What's new in Microsoft Intune](../intune-service/fundamentals/whats-new.md).
