---
title: Tutorial&#58; Co-management path 1
titleSuffix: Configuration Manager
description: Configure co-management with Microsoft Intune when you already manage Windows 10 devices with Configuration Manager.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
---

# Tutorial: Enable co-management for existing Configuration Manager clients
With co-management, you can retain your well-established processes for using Configuration Manager to manage PCs in your organization. At the same time, you're investing in the cloud through use of Intune for security and modern provisioning.  

In this tutorial, you set up co-management of your Windows 10 devices that are already enrolled in Configuration Manager. This tutorial begins with the premise that you already use Configuration Manager to manage your Windows 10 devices.

Use this tutorial when:  

- You have an on-premises Active Directory that you can connect to Azure Active Directory (Azure AD) in a hybrid Azure AD configuration
- You have existing Configuration Manager clients that you want to cloud-attach


**In this tutorial you will:**  
> [!div class="checklist"]  
> * Review prerequisites for Azure and your on-premises environment  
> * Set up hybrid Azure AD  
> * Configure Configuration Manager client agents to register with Azure AD  
> * Configure Intune to auto-enroll devices  
> * Assign Intune licenses to users  
> * Enable co-management in Configuration Manager  


## Prerequisites  

### Azure services and environment
- Azure Subscription ([free trial](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune subscription
  > [!TIP]  
  > An Enterprise Mobility + Security (EMS) Subscription includes both Azure Active Directory Premium and Microsoft Intune. EMS Subscription ([free trial](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

If not already present in your environment, during this tutorial you'll:
- Assign users a license for *Intune* and for *Azure Active Directory Premium*
- Configure [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) between your on-premises Active Directory and your Azure Active Directory (AD) tenant


### On-premises infrastructure
- A [supported version](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) of System Center Configuration Manager current branch
- The [MDM Authority](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) must be set to Intune  


### Permissions
Throughout this tutorial, use the following permissions to complete tasks:  
- An account that is a *global administrator* in Azure  
- An account that is a *domain admin* on your on-premises infrastructure  
- An account that is a *full administrator* for *all* scopes in Configuration Manager   

## Set up hybrid Azure AD
When you set up a hybrid Azure AD, you're really setting up integration of an on-premises AD with Azure AD using Azure AD Connect and Active Directory Federated Services (ADFS). With successful configuration, your workers can seamlessly sign in to external systems using their on-premises AD credentials.

> [!IMPORTANT]  
> This tutorial details a bare-bones process to set up hybrid Azure AD for a managed domain. We recommend you be familiar with the process and not rely on this tutorial as your guide to understanding and deploying hybrid Azure AD.
>
> For more information about hybrid Azure AD, start with the following articles in the Azure Active Directory documentation:
> - [Plan your Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Plan your hybrid Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Control the hybrid Azure AD join of your devices](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configure hybrid Azure AD join for federated domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### Set up Azure AD Connect  
Hybrid Azure AD requires configuration of Azure AD Connect to keep computer accounts in your on-premises Active Directory (AD) and the device object in Azure AD in sync.

Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join. Use of that wizard simplifies the configuration process.  

To configure Azure AD Connect, you need credentials of a global administrator for your Azure AD tenant.  

> [!TIP]  
> The following procedure should not be considered authoritative for set up of Azure AD Connect but is provided here to help streamline configuration of co-management between Intune and Configuration Manager. For the authoritative content on this and related procedures for set up of Azure AD, see [Configure hybrid Azure AD join for managed domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) in the Azure AD documentation.  


#### Configure a hybrid Azure AD join using Azure AD Connect

1. Get and install the [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 or higher).  
2. Launch Azure AD Connect, and then select **Configure**.
3. On the **Additional tasks** page, select **Configure device options**, and then select **Next**.
4. On the **Overview** page, select **Next**.
5. On the **Connect to Azure AD** page, enter the credentials of a global administrator for your Azure AD tenant.
6. On the **Device options** page, select **Configure Hybrid Azure AD join**, and then select **Next**.
7. On the **SCP** page, for each on-premises forest you want Azure AD Connect to configure the service connection point (SCP), do the following steps, and then select **Next**:  
   1. Select the forest.  
   2. Select the authentication service.  If you have a federated domain, select AD FS server unless your organization has exclusively Windows 10 clients and you have configured computer/device sync or your organization is using [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Click **Add** to enter the enterprise administrator credentials.  
8. On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then select **Next**.  

   You can select the option to support Windows downlevel domain-joined devices, but keep in mind that co-management of devices is only supported for Windows 10.

9. If you have a managed domain, skip this step.  

   On the **Federation configuration** page, enter the credentials of your AD FS administrator, and then select **Next**.
10. On the **Ready to configure** page, select **Configure**.
11. On the **Configuration complete** page, select **Exit**.

If you experience issues with completing hybrid Azure AD join for domain joined Windows devices, see [Troubleshooting hybrid Azure AD join for Windows current devices](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## Configure Client Settings to direct clients register with Azure AD  
Use Client Settings to configure Configuration Manager clients to automatically register with Azure AD.  

1. Open the **Configuration Manager console** > **Administration** > **Overview** > **Client Settings**, and then edit the **Default Client Settings**.  

2. Select **Cloud Services**.  

3. On the **Default Settings** page, set **Automatically register new Windows 10 domain joined devices with Azure Active Directory** to = **Yes**.  

4. Select **OK** to save this configuration.  

## Configure auto-enrollment of devices to Intune   
Next, we’ll set up auto-enrollment of devices with Intune. With automatic enrollment, devices you manage with Configuration Manager automatically enroll with Intune.

Automatic enrollment also lets users enroll their Windows 10 devices to Intune. Devices enroll when a user adds their work account to their personally owned device, or when a corporate-owned device is joined to Azure Active Directory.  

1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Azure Active Directory** > **Mobility (MDM and MAM)** > **Microsoft Intune**.  

2. Configure **MDM user scope**. Specify one of the following to configure which users’ devices are managed by Microsoft Intune and accept the defaults for the URL values.  

   - **Some** - Select the **Groups** that can automatically enroll their Windows 10 devices  

   - **All** - All users can automatically enroll their Windows 10 devices
when set to **None**, Mobile Device Management (MDM) automatic enrollment is disabled

   > [!IMPORTANT]  
   > If both **MAM user scope** and automatic MDM enrollment (**MDM user scope**) are enabled for a group, only MAM is enabled. Only Mobile Application Management (MAM) is added for users in that group when they workplace join personal device. Devices are not automatically MDM  enrolled.  

3. Select **Save** to complete configuration of automatic enrollment.  

4. Return to **Mobility (MDM and MAM)** and then select **Microsoft Intune Enrollment**.  

5. For MDM user scope, select **All**, and then **Save**.  


## Assign Intune licenses to users   
A commonly overlooked but critical action is to assign an Intune license to each user who will use a device that is co-managed.  

To assign licenses to groups of users, use Azure Active Directory.  

1. Sign in to the [Azure portal](https://portal.azure.com/) with an Administrator account. To manage licenses, the account must be a global administrator role or user account administrator.  

2. Select **All services** in the left navigation pane, and then select **Azure Active Directory**.  

3. On the **Azure Active Directory** pane, select **Licenses** to open a pane where you can see and manage all licensable products in the tenant.  

4. Under **All products**, select your product option that includes the Intune license, and then select **Assign** at the top of the pane.  

   For example, you might select **Enterprise Mobility + Security E5** if that is how you obtain Intune.  

5. On the **Assign license** pane, click **Users and groups** to open the **Users and groups** pane. Select the groups, and individual users to whom you want to assign a license.  Then, click **Select** at the bottom of the pane to confirm that selection.  

6. On the **Assign license** pane, click **Assignment options** to display all service plans included in the product you selected previously. If you selected a single product like Intune, then only that product is shown.  
   - Set **Microsoft Intune** to **On**.  
   - Assign each user a license for **Azure Active Directory Premium**.  

   When the applicable licenses are assigned, select **OK**.  

7. To complete the assignment, on the **Assign license** pane, click **Assign** at the bottom of the pane.

8. A notification is displayed in the upper-right corner that shows the status and outcome of the process. If the assignment to the group couldn't be completed (for example, because of pre-existing licenses in the group), click the notification to view details of the failure.

For more information about assigning licenses for Intune to users, see [Assign licenses](https://docs.microsoft.com/intune/licenses-assign).


## Enable co-management in Configuration Manager
With hybrid Azure AD set up, Configuration Manager client configurations in place, and product licenses assigned to users, you're ready to flip the switch and enable co-management of your Windows 10 devices.  

> [!TIP]  
>  In step six of the following procedure, you'll assign a collection as a *Pilot group* for co-management. This is a group that contains a small number of clients to test your co-management configurations. We recommend you create a suitable collection before you start the procedure. Then you can select that collection without exiting the procedure to do so.  

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.

2. On the Home tab, in the Manage group, select **Configure co-management** to open the Co-management Configuration Wizard.

3. On the Subscription page, select **Sign In** and sign in to your Intune tenant, and then select **Next**.

4. On the Enablement page, from the *Automatic enrollment in Intune* dropdown list, select one of the following options:  

   - **Pilot**  - *(Recommended)* Members of the collection you specify are automatically enrolled into Intune and can then be co-managed. You specify the pilot collection on the *Staging* page of this wizard. This option allows you to test co-management on a subset of clients. You can then roll out co-management to additional clients using a phased approach.  

   - **All** - Co-management is enabled for all clients.  

5. On the Workloads page you can switch workloads from **Configuration Manager** to one of the following, and then when ready to continue, select **Next**.  

   - **Pilot Intune** - Switches a workload only for the devices in the Pilot group. You’ll assign a collection as the Pilot group on the next page of the wizard.  

   - **Intune** - Switches the associated workload for all co-managed Windows 10 devices.  

   You don't need to switch any workloads at the time you enable co-management. You can revisit this configuration from the Configuration Manager console later, after co-management is configured.  

   Before you switch a workload, make sure the corresponding workload in Intune is configured and deployed. Doing so keeps the workloads managed.  

6. On the Staging page, specify a collection to use for the **Pilot collection**, and then click **Next**. The collection you specify is used as part of your phased rollout of co-management. You can change the collections in the pilot group at any time from the co-management properties.  

7. On the Summary page, select **Next**, and then **Close** to complete the Wizard.  


## Next steps
- Review the status of co-managed devices with the [Co-management dashboard](/sccm/comanage/how-to-monitor)
- Start getting [immediate value](quickstarts.md#immediate-value) from co-management
- Use [conditional access](quickstart-conditional-access.md) and Intune compliance rules to manage user access to corporate resources
