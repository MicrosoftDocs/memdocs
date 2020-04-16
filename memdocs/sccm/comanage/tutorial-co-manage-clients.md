---
title: Tutorial&#58; Enable co-management for existing clients
titleSuffix: Configuration Manager
description: Configure co-management with Microsoft Intune when you already manage Windows 10 devices with Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
---

# Tutorial: Enable co-management for existing Configuration Manager clients

With co-management, you can keep your well-established processes for using Configuration Manager to manage PCs in your organization. At the same time, you're investing in the cloud through use of Intune for security and modern provisioning.  

In this tutorial, you set up co-management of your Windows 10 devices that are already enrolled in Configuration Manager. This tutorial begins with the premise that you already use Configuration Manager to manage your Windows 10 devices.

Use this tutorial when:  

- You have an on-premises Active Directory that you can connect to Azure Active Directory (Azure AD) in a hybrid Azure AD configuration.

  If you can't deploy a hybrid Azure Active Directory (AD) that joins your on-premises AD with Azure AD, we recommend following our companion tutorial, [Enable co-management for new internet-based Windows 10 devices](/sccm/comanage/tutorial-co-manage-new-devices).
- You have existing Configuration Manager clients that you want to cloud-attach.

**In this tutorial you will:**  
> [!div class="checklist"]
> * Review prerequisites for Azure and your on-premises environment
> * Set up hybrid Azure AD  
> * Configure Configuration Manager client agents to register with Azure AD  
> * Configure Intune to auto-enroll devices  
> * Enable co-management in Configuration Manager  

## Prerequisites  

### Azure services and environment

- Azure Subscription ([free trial](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune subscription
  > [!TIP]  
  > An Enterprise Mobility + Security (EMS) Subscription includes both Azure Active Directory Premium and Microsoft Intune. EMS Subscription ([free trial](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

If not already present in your environment, during this tutorial you'll:

- Configure [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) between your on-premises Active Directory and your Azure Active Directory (AD) tenant.

> [!TIP]
> You no longer need to purchase and assign individual Intune or EMS licenses to your users. For more information, see the [Product and licensing FAQ](/configmgr/core/understand/product-and-licensing-faq#bkmk_mem).

### On-premises infrastructure

- A [supported version](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) of Configuration Manager current branch
- The mobile device management (MDM) authority must be set to Intune.  

### Permissions

Throughout this tutorial, use the following permissions to complete tasks:

- An account that is a *global administrator* in Azure Active Directory (Azure AD) 
- An account that is a *domain admin* on your on-premises infrastructure  
- An account that is a *full administrator* for *all* scopes in Configuration Manager

## Set up hybrid Azure AD

When you set up a hybrid Azure AD, you're really setting up integration of an on-premises AD with Azure AD using Azure AD Connect and Active Directory Federated Services (ADFS). With successful configuration, your workers can seamlessly sign in to external systems using their on-premises AD credentials.

> [!IMPORTANT]  
> This tutorial details a bare-bones process to set up hybrid Azure AD for a managed domain. We recommend you be familiar with the process and not rely on this tutorial as your guide to understanding and deploying hybrid Azure AD.
>
> For more information about hybrid Azure AD, start with the following articles in the Azure Active Directory documentation:
>
> - [Plan your Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Plan your hybrid Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Control the hybrid Azure AD join of your devices](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Configure hybrid Azure AD join for federated domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### Set up Azure AD Connect

Hybrid Azure AD requires configuration of Azure AD Connect to keep computer accounts in your on-premises Active Directory (AD) and the device object in Azure AD in sync.

Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join. Use of that wizard simplifies the configuration process.  

To configure Azure AD Connect, you need credentials of a global administrator for Azure AD.  

> [!TIP]  
> The following procedure should not be considered authoritative for set up of Azure AD Connect but is provided here to help streamline configuration of co-management between Intune and Configuration Manager. For the authoritative content on this and related procedures for set up of Azure AD, see [Configure hybrid Azure AD join for managed domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) in the Azure AD documentation.  

#### Configure a hybrid Azure AD join using Azure AD Connect

1. Get and install the [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 or higher).  
2. Launch Azure AD Connect, and then select **Configure**.
3. On the **Additional tasks** page, select **Configure device options**, and then select **Next**.
4. On the **Overview** page, select **Next**.
5. On the **Connect to Azure AD** page, enter the credentials of a global administrator for Azure AD.
6. On the **Device options** page, select **Configure Hybrid Azure AD join**, and then select **Next**.
7. On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then select **Next**.  

   You can select the option to support Windows downlevel domain-joined devices, but keep in mind that co-management of devices is only supported for Windows 10.
8. On the **SCP** page, for each on-premises forest you want Azure AD Connect to configure the service connection point (SCP), do the following steps, and then select **Next**:  
   1. Select the forest.  
   2. Select the authentication service.  If you have a federated domain, select AD FS server unless your organization has exclusively Windows 10 clients and you have configured computer/device sync or your organization is using [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Click **Add** to enter the enterprise administrator credentials.  
9. If you have a managed domain, skip this step.  

   On the **Federation configuration** page, enter the credentials of your AD FS administrator, and then select **Next**.
10. On the **Ready to configure** page, select **Configure**.
11. On the **Configuration complete** page, select **Exit**.

If you experience issues with completing hybrid Azure AD join for domain joined Windows devices, see [Troubleshooting hybrid Azure AD join for Windows current devices](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## Configure Client Settings to direct clients to register with Azure AD

Use Client Settings to configure Configuration Manager clients to automatically register with Azure AD.  

1. Open the **Configuration Manager console** > **Administration** > **Overview** > **Client Settings**, and then edit the **Default Client Settings**.  

2. Select **Cloud Services**.  

3. On the **Default Settings** page, set **Automatically register new Windows 10 domain joined devices with Azure Active Directory** to = **Yes**.  

4. Select **OK** to save this configuration.  

## Configure auto-enrollment of devices to Intune

Next, we'll set up auto-enrollment of devices with Intune. With automatic enrollment, devices you manage with Configuration Manager automatically enroll with Intune.

Automatic enrollment also lets users enroll their Windows 10 devices to Intune. Devices enroll when a user adds their work account to their personally owned device, or when a corporate-owned device is joined to Azure Active Directory.  

1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Azure Active Directory** > **Mobility (MDM and MAM)** > **Microsoft Intune**.  

2. Configure **MDM user scope**. Specify one of the following to configure which users' devices are managed by Microsoft Intune and accept the defaults for the URL values.  

   - **Some**: Select the **Groups** that can automatically enroll their Windows 10 devices  

   - **All**: All users can automatically enroll their Windows 10 devices

   - **None**: Disable MDM automatic enrollment

   > [!IMPORTANT]  
   > If both **MAM user scope** and automatic MDM enrollment (**MDM user scope**) are enabled for a group, only MAM is enabled. Only Mobile Application Management (MAM) is added for users in that group when they workplace join personal device. Devices aren't automatically MDM-enrolled.  

3. Select **Save** to complete configuration of automatic enrollment.  

4. Return to **Mobility (MDM and MAM)** and then select **Microsoft Intune Enrollment**.  

    > [!NOTE]
    > Some tenants may not have these options to configure.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** is how you configure the MDM app for Azure AD. **Microsoft Intune Enrollment** is a specific Azure AD app that's created when you apply multi-factor authentication policies for iOS and Android enrollment. For more information, see [Require multi-factor authentication for Intune device enrollments](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication).

5. For MDM user scope, select **All**, and then **Save**.  

## Enable co-management in Configuration Manager

With hybrid Azure AD set-up and Configuration Manager client configurations in place, you're ready to flip the switch and enable co-management of your Windows 10 devices.  

> [!TIP]
> - When you enable co-management, you'll assign a collection as a *Pilot group*. This is a group that contains a small number of clients to test your co-management configurations. We recommend you create a suitable collection before you start the procedure. Then you can select that collection without exiting the procedure to do so.
> - Starting in Configuration Manager version 1906, you may need multiple collections since you can assign a different *Pilot group* for each workload.

### Enable co-management starting in version 1906

To enable co-management starting in Configuration Manager version 1906, follow the instructions below:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### Enable co-management in version 1902 and earlier

To enable co-management for Configuration Manager version 1902 and earlier, follow the instructions below:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## Next steps

- Review the status of co-managed devices with the [Co-management dashboard](/sccm/comanage/how-to-monitor)
- Start getting [immediate value](quickstarts.md#immediate-value) from co-management
- Use [conditional access](quickstart-conditional-access.md) and Intune compliance rules to manage user access to corporate resources
