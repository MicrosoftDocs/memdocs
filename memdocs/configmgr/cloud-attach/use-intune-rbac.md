---
title: Intune role-based access control for tenant-attached devices
titleSuffix: Configuration Manager
description: Enable Intune role-based access control for Configuration Manager tenant-attached clients
ms.date: 08/18/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
ms.collection: highpri
---

# Intune role-based access control for tenant-attached clients
<!--8126836, 6415648, 8348644, IN14996522-->
*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager version 2207, you can use Intune role-based access control (RBAC) when interacting with [tenant attached devices](../tenant-attach/client-details.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) from the Microsoft Endpoint Manager admin center. When using Intune as the role-based access control authority, a user with the [Help Desk Operator role](../../intune/fundamentals/role-based-access-control.md#built-in-roles) doesn't need an assigned security role or additional permissions from Configuration Manager. [Intune role-based access control](../../intune/fundamentals/create-custom-role.md) manages the permissions to all cloud-attached device pages in the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com), such as [device timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), [CMPivot](../tenant-attach/cmpivot-start.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), and [scripts](../tenant-attach/scripts.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json).  

The three high-level steps to configure Intune as the role-based access control authority for tenant-attached devices are:
<!--To enable Intune role-based access control as the authority, the following high-level steps -->

- From the Configuration Manager console, [disable enforcement of Configuration Manager role-based access control](#bkmk_disable-configmgr) for cloud-attached clients
- From Intune, [enable managing the user permissions](#bkmk_enable-intune) for cloud-attached devices
- From Intune, [verify role-based access control permissions](#bkmk_verify-intune-rbac) for cloud-attached devices


## <a name="bkmk_disable-configmgr"></a> Disable enforcement of Configuration Manager role-based access control for cloud-attached clients

To use Intune role-based access control for tenant attach rather than Configuration Manager role-based access control, use the instructions below:

1. From the Configuration Manager console, go to, **Administration** > **Cloud Services** > **Cloud Attach**.
1. The location of the role-based access control option varies depending on if your environment is already cloud-attached or not.
   - If your environment is already cloud-attached, open the properties for **CoMgmtSettingsProd**. If you don't have devices uploaded to the admin center, configure that option first. For more information, see [Enable cloud attach](enable.md).
   - If your environment isn't cloud-attached, select **Configure Cloud Attach** to open the **Cloud Attach Configuration wizard**. 
1. On the **Configure upload** tab, or page in the wizard, clear the checkbox for the following option under the **Role-based Access Control** heading:

   **Enforce Configuration Manager RBAC for cloud console requests that interact with Configuration Manager**

1. Choose **OK** to save the change to the **CoMgmtSettingsProd** properties, or continue on to complete the [cloud attach wizard](enable.md).

:::image type="content" source="media/14996522-configure-upload.png" alt-text="Screenshot of the CoMgmtSettingsProd properties in Configuration Manager. In the screenshot, the configure upload tab is displayed with a red box outlining the role-based access control section." lightbox="media/14996522-configure-upload.png":::

## <a name="bkmk_enable-intune"></a> Enable role-based access control from Intune

To enable Intune to manage user permissions for cloud-attached devices, use the following steps:  

1. Open the [Microsoft Endpoint admin center](https://endpoint.microsoft.com) and sign in.
1. Select **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**.
1. In the banner, select **You can also manage user permissions from Intune. Click here to learn more about this option.**
1. The **Use Intune RBAC** flyout appears.
1. Select **On** for the **Use Intune RBAC** option, then choose **Apply**.

:::image type="content" source="media/14996522-connectors-flyout.png" alt-text="Screenshot of the Microsoft Endpoint Configuration Manager connectors and tokens page in Microsoft Endpoint Manager admin center. The Use Intune RBAC flyout is displayed in the screenshot." lightbox="media/14996522-connectors-flyout.png":::

## <a name="bkmk_verify-intune-rbac"></a> Verify role-based access control permissions from Intune

Once Intune is set to the role-based access control authority, verify the permissions for your roles. If needed, you can add these permissions to [custom roles](../../intune/fundamentals/create-custom-role.md) you created in Intune.  

1. Open the [Microsoft Endpoint admin center](https://endpoint.microsoft.com) and sign in.
1. Select **Tenant administration** > **Roles**.
1. Select a role, such as **Help Desk Operator**, and review the permissions listed for **Cloud attached devices**. If needed, edit permissions for any [custom roles](../../intune/fundamentals/create-custom-role.md) you created in Intune.  

The following Intune permissions control access to the Configuration Manager cloud-attached devices: 

| Permission | Description |
| --- | --- |
| Cloud attached devices\View collections | Displays the **Collections** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View resource explorer | Displays the **Resource explorer** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View timeline | Displays the **Timeline** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View software updates | Displays the **Software updates** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View scripts | Displays the **Scripts** page for Configuration Manager cloud attached devices |
| Cloud attached devices\Run script | Displays the **Run script** action for Configuration Manager cloud attached devices |
| Cloud attached devices\Run CMPivot query | Displays the **CMPivot** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View client details | Displays the **Client details** page for Configuration Manager cloud attached devices |
| Cloud attached devices\View applications | Displays the **Applications** page for Configuration Manager cloud attached devices |
| Cloud attached devices\Take application actions | Displays application actions in the **Applications** page  for Configuration Manager cloud attached devices |

## <a name="bkmk_faq"></a> Frequently asked questions

### 
