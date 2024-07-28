---
title: Troubleshooting the device timeline
titleSuffix: Configuration Manager
description: Troubleshooting the device timeline for Intune tenant attach
ms.date: 07/11/2022
ms.topic: troubleshooting
ms.subservice: core-infra
ms.service: configuration-manager
manager: apoorvseth
author: Banreet
ms.author: banreetkaur
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_timeline"></a> Troubleshoot the timeline for devices uploaded to the admin center
<!--CM7141381, IN7552762 pubpreview Sept8, 2020, GA 2201 -->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot the device timeline in the Microsoft Intune admin center:

## <a name="bkmk_common"></a> Common errors from the Microsoft Intune admin center

When viewing or synching the timeline from the Microsoft Intune admin center, you may run across one of these errors.  

### <a name="bkmk_401"></a> The necessary configuration is missing in Microsoft Entra ID

**Error message:** The necessary configuration is missing in Microsoft Entra ID. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Microsoft Entra ID.

**Possible causes:**

- Make sure [Microsoft Entra user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) and [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) are configured and the user account accessing tenant attach features from the Microsoft Intune admin center is discovered by both.
- The user account might need an [Intune role](../../intune-service/fundamentals/role-based-access-control.md) assigned. <!--7980141-->

### <a name="bkmk_403"></a> Unable to get timeline information

**Error message:** Unable to get timeline information. Make sure the Microsoft Entra ID and AD user discovery are configured and the user is discovered by both. Verify the user has the proper permissions in Configuration Manager.

**Possible causes:**

Verify the account has the following permissions:
- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read Resource** permission under **Collection** in Configuration Manager.
- The **Notify Resource** permission under **Collection** in Configuration Manager.
   - This permission is needed to be able to sync the latest events.

### <a name="bkmk_404"></a> Unable to get timeline information

**Error message:** The device information hasn't yet synchronized from Configuration Manager to Microsoft Intune admin center. Wait up to 15 minutes after you attach the site to your Azure tenant.

**Possible resolution:** Wait for approximately 15 minutes and the issue should be resolved automatically.

### <a name="bkmk_500"></a> Unexpected error occurred

**Error message:** Unexpected error occurred

**Possible causes:**

- Verify you have a supported version of Configuration Manager and the corresponding version of the console installed.
- If there are a large number of events (more than 10,000, approximately), and multiple searches are requested rapidly, then it's possible to receive an unexpected error. You may also see your search results [timeout](#bkmk_timeout).

### <a name="bkmk_timeout"></a> Getting results timed out

**Error message:** Getting results timed out. Make sure that the Configuration Manager service connection point is operational and has a connection to the cloud.

**Possible cause:** If there are a large number of events (more than 10,000, approximately), and multiple searches are requested rapidly, then it's possible to see a timeout. You may also see an [unexpected error](#bkmk_500).

## Known issues

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)
