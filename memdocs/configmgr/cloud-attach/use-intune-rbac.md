---
title: Intune role-based access control for tenant attach
titleSuffix: Configuration Manager
description: Enable Intune role-based access control for Configuration Manager tenant attached clients
ms.date: 08/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
ms.collection: highpri
---

# Intune role-based access control for tenant attached clients
<!--8126836, 6415648, 8348644, IN14996522-->
*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager version 2207, you can use Intune role-based access control (RBAC) when interacting with [tenant attached devices](../tenant-attach/client-details.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) from the Microsoft Endpoint Manager admin center. When using Intune as the RBAC authority, a user with the [Help Desk Operator role](../../../../../../intune/fundamentals/role-based-access-control.md#built-in-roles) doesn't need an assigned security role or additional permissions from Configuration Manager.

<!--To enable Intune role-based access control as the authority, the following high-level steps -->

- From the Configuration Manager console, disable enforcing Configuration Manager RBAC for cloud attached clients
- From Intune, enable managing user permissions for cloud attached devices
- From Intune, verify RBAC permissions for cloud attached devices


## Configure Intune as the RBAC authority from Configuration Manager

To use Intune role-based access control for tenant attach, use the instructions below:

1. From the Configuration Manager console, go to, **Administration** > **Cloud Services** > **Cloud Attach**.
1. If you already have tenant attach enabled, open the properties for **CoMgmtSettingsProd**. If you don't have tenant attach enabled, select **Configure Cloud Attach** to open the **Cloud Attach Configuration wizard**.
1. On the **Configure upload** tab (or page in the wizard), enable the following option under the **Role-based Access Control** heading:

   **Use Intune role-based access control (RBAC) when you view Configuration Manager devices and take action in Microsoft Endpoint Manager admin center**

1. Choose **OK** to save the change to the **CoMgmtSettingsProd** properties, or continue on to complete the cloud attach wizard.

Open the **Admin Center Preview** to verify the the Help Desk Operator can see **Client details**:

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace and select the **Devices** node.
1. Right-click on a device that's been uploaded to Microsoft Endpoint Manager.
1. In the right-click menu, select **Start** > **Admin Center Preview** to open the preview in your browser.
     - This launch is a preview experience. The final location will be in Microsoft Endpoint Manager admin center.
1. Sign into the Microsoft Endpoint Manager admin center as a user that has  the Help Desk Operator role.
1. Display the **Client details** page.


