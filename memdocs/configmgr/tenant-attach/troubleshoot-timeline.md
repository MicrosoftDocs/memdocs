---
title: Troubleshooting the device timeline
titleSuffix: Configuration Manager
description: "Troubleshooting the device timeline for Configuration Manager tenant attach"
ms.date: 09/8/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 54a58548-45f3-4f75-93d6-d2fd96227e6a
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_timeline"></a> Troubleshoot the timeline for devices uploaded to the admin center (preview)
<!--CM7141381, IN7552762 pubpreview Sept8, 2020 -->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot the device timeline in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.


## <a name="bkmk_common"></a> Common errors from the Microsoft Endpoint Manager admin center

When viewing or synching the timeline from the Microsoft Endpoint Manager admin center, you may run across one of these errors.  

### <a name="bkmk_401"></a> The necessary configuration is missing in Azure Active Directory

**Error code**: 401

**Error message:** The necessary configuration is missing in Azure Active Directory. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Azure AD.

**Possible causes:**

- Make sure [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) and [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) are configured and the user is discovered by both.
- The user account might be missing the **Admin User** role for the Configuration Manager Microservice application in Azure AD. Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium. Changes to this permission can take up to an hour to take effect.

### <a name="bkmk_403"></a> Unable to get timeline information

**Error code**: 403

**Error message:** Unable to get timeline information. Make sure the Azure AD and AD user discovery are configured and the user is discovered by both. Verify the user has the proper permissions in Configuration Manager.

**Possible causes:**

Verify the account has the following permissions:
- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read Resource** permission under **Collection** in Configuration Manager.
- The **Notify Resource** permission under **Collection** in Configuration Manager.
   - This permission is needed to be able to sync the latest events.

### <a name="bkmk_404"></a> Unable to get timeline information

**Error code**: 404

**Error message:** The device information hasn't yet synchronized from Configuration Manager to Microsoft Endpoint Manager admin center. Wait up to 15 minutes after you attach the site to your Azure tenant.

**Possible resolution:** Wait for approximately 15 minutes and the issue should be resolved automatically.

## Known issues

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)