---
title: Intune role-based access control for tenant-attached devices
titleSuffix: Configuration Manager
description: Enable Intune role-based access control for Configuration Manager tenant-attached clients
ms.date: 08/24/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: high
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Intune role-based access control for tenant-attached clients
<!--8126836, 6415648, 8348644, IN14996522, 13058986-->
*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager version 2207, you can use Intune role-based access control (RBAC) when interacting with [tenant attached devices](../tenant-attach/client-details.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) from the Microsoft Intune admin center. For example, when using Intune as the role-based access control authority, a user with the [Help Desk Operator role](../../intune/fundamentals/role-based-access-control.md#built-in-roles) doesn't need an assigned security role or additional permissions from Configuration Manager. [Intune role-based access control](../../intune/fundamentals/create-custom-role.md) manages the permissions to all cloud-attached device pages in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), such as [device timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), [CMPivot](../tenant-attach/cmpivot-start.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), and [scripts](../tenant-attach/scripts.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json).  

> [!IMPORTANT]
> Currently, any enforcement of Intune role-based access control for displaying and taking actions on tenant-attached devices from the Microsoft Intune admin center is optional. We recommend all admins with cloud-connected Configuration Manager environments begin [verifying the role-based access control permissions from Intune](#bkmk_verify-intune-rbac).

The three high-level steps to configure Intune as the role-based access control authority for tenant-attached devices are:
<!--To enable Intune role-based access control as the authority, the following high-level steps -->

- From the Configuration Manager console, [disable enforcement of Configuration Manager role-based access control](#bkmk_disable-configmgr) for cloud-attached clients
- From Intune, [enable managing the user permissions](#bkmk_enable-intune) for cloud-attached devices
- From Intune, [verify role-based access control permissions](#bkmk_verify-intune-rbac) for cloud-attached devices

## Prerequisites

- Configuration Manager version 2207 or later
- [Tenant attached devices](../tenant-attach/client-details.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)

## Limitations

- Currently [scoping](../../intune/fundamentals/scope-tags.md) isn't supported when using only Intune role-based access control for for displaying and taking actions on tenant-attached devices from the Microsoft Intune admin center.
- Currently, the [**Software updates** page](../tenant-attach/software-updates.md) isn't available for cloud-only users when using the early update ring of Configuration Manager version 2207.  <!--15287859-->

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

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and sign in as a user that has the **Roles/Update** permission. For more information about the permission, see [custom role permissions in Intune](../../intune/fundamentals/create-custom-role.md).
1. Select **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**.
1. In the banner, select **You can also manage user permissions from Intune. Click here to learn more about this option.**
1. The **Use Intune RBAC** flyout appears.
1. Select **On** for the **Use Intune RBAC** option, then choose **Apply**.
1. The change may take about 10 minutes to take effect.

:::image type="content" source="media/14996522-connectors-flyout.png" alt-text="Screenshot of the Microsoft Configuration Manager connectors and tokens page in Microsoft Intune admin center. The Use Intune RBAC flyout is displayed in the screenshot." lightbox="media/14996522-connectors-flyout.png":::

## <a name="bkmk_verify-intune-rbac"></a> Verify role-based access control permissions from Intune

Once Intune is set to the role-based access control authority, verify the permissions for your roles. If needed, you can add these permissions to [custom roles](../../intune/fundamentals/create-custom-role.md) you created in Intune.  

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and sign in.
1. Select **Tenant administration** > **Roles**.
1. Select a role, such as **Application Manager**, and review the permissions listed for **Cloud attached devices**. If needed, edit permissions for any [custom roles](../../intune/fundamentals/create-custom-role.md) you created in Intune.  

The following Intune permissions control access to the Configuration Manager cloud-attached devices:

| Permission | Description | Intune built-in roles with the permission |
|---|---|---|
| Cloud attached devices\View collections | Displays the **Collections** page for Configuration Manager cloud attached devices | Application Manager, Endpoint Security Manager, Read Only Operator, School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\View resource explorer | Displays the **Resource explorer** page for Configuration Manager cloud attached devices |  Application Manager, Endpoint Security Manager, Read Only Operator, School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\View timeline | Displays the **Timeline** page for Configuration Manager cloud attached devices |  Application Manager, Endpoint Security Manager, Read Only Operator, School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\View software updates | Displays the **Software updates** page for Configuration Manager cloud attached devices |  Application Manager, Endpoint Security Manager, Read Only Operator, School Administrator, Help Desk Operator |
| Cloud attached devices\View scripts | Displays the **Scripts** page for Configuration Manager cloud attached devices |  Endpoint Security Manager, Read Only Operator, School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\Run script | Displays the **Run script** action and allows the user to run scripts on Configuration Manager cloud attached devices |  School Administrator, Help Desk Operator |
| Cloud attached devices\Run CMPivot query | Displays the **CMPivot** page for Configuration Manager cloud attached devices |  Endpoint Security Manager, School Administrator, Help Desk Operator |
| Cloud attached devices\View client details | Displays the **Client details** page for Configuration Manager cloud attached devices |  Application Manager, Endpoint Security Manager, Read Only Operator,School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\View applications | Displays the **Applications** page for Configuration Manager cloud attached devices |  Application Manager, Read Only Operator, School Administrator, Policy Profile Manager, Help Desk Operator |
| Cloud attached devices\Take application actions | Displays application actions in the **Applications** page and allows the user to take application actions on Configuration Manager cloud attached devices |  Application Manager, School Administrator, Help Desk Operator |
| Remote tasks/Rotate BitLockerKeys (preview) | Initiates a key rotation for BitLocker Recovery Passwords on the device. Displays the *Recovery keys* page for Configuration Manager cloud attached devices. |  Endpoint Security Manager, Help Desk Operator |

## <a name="bkmk_faq"></a> Frequently asked questions

### I have cloud-only users that need access to tenant-attached devices in Intune, will this give them access?

Yes. When a user is cloud only, in this scenario meaning they are in Azure Active Directory (Azure AD) and can access Intune, using Intune RBAC will give them access to tenant-attached devices.

### What if I have multiple Configuration Manager hierarchies connected to my tenant?

The **Use Intune RBAC** setting in the Microsoft Intune admin center applies to all of the Configuration Manager hierarchies listed in the tenant.

### What happens if the Configuration Manager and Intune settings are mismatched?

If the **Use Intune RBAC** toggle in Intune is set to **Off**, then Configuration Manager role-based access will be enforced, even if the **Enforce Configuration Manager RBAC for cloud console requests that interact with Configuration Manager** checkbox is cleared. Disabling the **Enforce Configuration Manager RBAC for cloud console requests that interact with Configuration Manager** option doesn't have any effect until the **Use Intune RBAC** toggle in Intune is set to **On**.

### What happens if my test hierarchy is configured to use Intune RBAC, but my production hierarchy isn't and they are in the same tenant?

The **Use Intune RBAC** setting applies to all of the Configuration Manager hierarchies listed in the tenant. Cloud-only users can access tenant-attached devices that are uploaded from the test hierarchy because you've also cleared the checkbox to enforce Configuration Manager RBAC. If a cloud-only user tries to access a tenant-attached device uploaded from the production environment, they'll receive an error since production devices are enforcing Configuration Manager RBAC. The cloud-only user will receive an error similar to the following message: 
`Unable to get device information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.`


## Next steps

- Review the [timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) for a cloud-attached device
- Run a [CMPivot](../tenant-attach/cmpivot-start.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) query on a cloud attached device
