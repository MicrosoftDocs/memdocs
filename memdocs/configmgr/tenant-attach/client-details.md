---
title: Tenant attach - ConfigMgr client details in the admin center
titleSuffix: Configuration Manager
description: View client details for Configuration Manager devices from the admin center.
ms.date: 07/11/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---


# <a name="bkmk_mem"></a> Tenant attach: ConfigMgr client details in the admin center
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020, GA 2201-->
*Applies to: Configuration Manager (current branch)*

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. You can see ConfigMgr client details including collections, boundary group membership, and real-time client information for a specific device in the admin center.

## Prerequisites

- All of the prerequisites for [Microsoft Endpoint Manager tenant attach](device-sync-actions.md) and a tenant attached environment.
- One of the following browsers:
  - Microsoft Edge, version 77 and later
  - Google Chrome
- The user accounts triggering device actions have the following prerequisites:
   - The user account needs to be a synced user object in Azure AD (hybrid identity). This means that the user is synced to Azure Active Directory from Active Directory.
     - For Configuration Manager version 2103, and later: </br>
   Has been discovered with either [Azure Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) or [Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). <!--9089764-->
     - Staring in Configuration Manager version 2207, you can choose to implement [Intune role-based access control for tenant-attached clients](../cloud-attach/use-intune-rbac.md) to allow cloud-only users access to tenant attached clients

## Permissions

The user account accessing tenant attach features within the Microsoft Endpoint Manager admin center needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- An [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned to the user <!--7980141-->

## View ConfigMgr client details

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select the **Client details**.
   - The primary site updates the following fields once an hour:
      - **Last policy request**
      - **Last active time**
      - **Last management point**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Client details in Microsoft Endpoint Manager admin center" lightbox="media/6024387-device-details.png":::

1. Select the **Collections** to list the client's collections. <!--6024390-->

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Client collections in Microsoft Endpoint Manager admin center" lightbox="media/6024387-device-collections.png":::

## <a name="bkmk_list"></a> List a user’s devices based on usage in the troubleshooting portal
<!--6974300-->

The troubleshooting portal in [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/) allows you to search for a user and view their associated devices. Tenant attached devices that are assigned [user device affinity automatically based on usage](../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md#set-up-the-site-to-automatically-create-user-device-affinities) will now be returned when searching for a user.
### Prerequisites for listing a user's device in the troubleshooting portal

- An environment that's tenant attached with uploaded devices
- Install the latest version of the Configuration Manager client
- Target clients with **User and Device Affinity** [client settings](../core/clients/deploy/about-client-settings.md#user-and-device-affinity) to automatically create the affinities
   - For more information, see [Create user device affinity automatically based on usage](../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md#set-up-the-site-to-automatically-create-user-device-affinities).
   - 
### View a user's devices

1. Go to the  [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
1. Select **Troubleshooting + support**.
1. On the **Troubleshoot** page, select **Change user** then search for a user.
1. The **Devices** chart lists the ConfigMgr devices associated with the user.  
   - Devices that previously reported affinity will resend their affinity to reflect in the admin center.
   - Devices that aren't already associated with a user will be updated once the affinity threshold has been met and reported.


## Next steps

[Troubleshoot client details](troubleshoot-client-details.md)
