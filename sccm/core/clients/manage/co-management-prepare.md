---
title: Prepare Windows 10 for co-management
titleSuffix: Configuration Manager
description: Learn how to prepare your Windows 10 devices for co-management.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
---

# Prepare Windows 10 devices for co-management
You can enable co-management on Windows 10 devices that are joined to AD and Azure AD, and enrolled in Microsoft Intune and a client in Configuration Manager. For new Windows 10 devices, and for devices that are already enrolled in Intune, install the Configuration Manager client before they can be co-managed. For Windows 10 devices that are already Configuration Manager clients, you can enroll the devices with Intune and enable co-management in the Configuration Manager console.

> [!IMPORTANT]
> Windows 10 mobile devices do not support co-management.



## Prerequisites

You must have the following prerequisites in place before you can enable co-management. There are general prerequisites, and different prerequisites for devices with the Configuration Manager client and devices that don't have the client installed.


### General prerequisites

The following are general prerequisites for you to enable co-management:  

- Configuration Manager version 1710 or later  

    - Beginning in Configuration Manager version 1806, you can connect multiple Configuration Manager instances to a single Intune tenant. <!--1357944-->  

- [Site onboarded with Azure AD for cloud management](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- EMS or Intune license for all users  

- [Azure AD automatic enrollment](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) enabled  

- Intune subscription, and the MDM authority in Intune set to **Intune**.  

    - If you're using [mixed authority](/sccm/mdm/deploy-use/migrate-mixed-authority), first complete the migration to Intune standalone. Then set the MDM authority to Intune before setting up co-management.<!--SCCMDocs issue #797-->


> [!Note]  
> If you have a hybrid MDM environment (Intune integrated with Configuration Manager), you can't enable co-management. However, you can start migrating users to Intune standalone and then enable their associated Windows 10 devices for co-management. For more information about migrating to Intune standalone, see [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### Prerequisite Azure Resource Manager roles
<!--SCCMDocs issue #667-->
For more information about Azure roles, see [Understand the different roles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).
|Action|Role needed|
|----|----|
|Set up a cloud management gateway|Azure Subscription Manager|
|Set up a cloud distribution point|Azure Subscription Manager|
|Create Azure Active Directory apps from the Configuration Manager console|Azure Active Directory Global Administrator|
|Importing Azure client and server apps in the Configuration Manager console| Configuration Manager Administrator, no additional Azure roles needed.|
|Set up Co-management through the Co-management wizard| Azure Active Directory user rights  along with being a Configuration Manager Administrator with all scope rights. 


### Additional prerequisites for devices with the Configuration Manager client

- Windows 10, version 1709 or later  

- [Hybrid Azure AD-joined](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (joined to AD and Azure AD)  


### Additional prerequisites for devices without the Configuration Manager client

- Windows 10, version 1709 or later  

- [Cloud management gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (when you use Intune to install the Configuration Manager client)  


> [!IMPORTANT]
> Windows 10 mobile devices do not support Co-management.



## Command line to install Configuration Manager client

Create an app in Intune for Windows 10 devices that aren't already Configuration Manager clients. When you create the app in the next sections, use the following command line:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### Example command line
If you have the following values:

- **URL of cloud management gateway mutual auth endpoint**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!Note]    
   >Use the **MutualAuthPath** value in the **vProxy_Roles** SQL view for the **URL of cloud management gateway mutual auth endpoint** value.  

- **FQDN of management point (MP)**: `mp1.contoso.com`    
- **Sitecode**: `PS1`    
- **Azure AD tenant ID**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **Azure AD client app ID**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **AAD Resource ID URI**: `ConfigMgrServer`    

  > [!Note]    
  > Use the **IdentifierUri** value found in the **vSMS_AAD_Application_Ex** SQL view for the **AAD Resource ID URI** value.  

Then use the following command line:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215-->
Starting in version 1806, fewer command-line properties are now required.  

- The following command-line properties are required in all scenarios:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- The following properties are required when using Azure AD for client authentication instead of PKI-based client authentication certificates:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- The following property is required if the client will roam back to the intranet:  
    - SMSMP  

The following example includes all of the above properties:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).


> [!Tip]
> Find the command-line parameters for your site by using the following steps:     
> 
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node.  
> 
> 2. In the ribbon, select **Configure co-management** to open the Co-management Onboarding Wizard. (If you've already set up co-management, select **Properties**. Then skip to step 4.)    
> 
> 3. On the Subscription page, select **Sign In**. Sign in to your Intune tenant, and then click **Next**.    
> 
> 4. On the Enablement page, select **Copy** to copy the command line to the clipboard. Then save the command line to use in the procedure to create the app.  
> 
> 5. Click **Cancel** to exit the wizard.  

> [!Important]    
> If you customize the command line to install the Configuration Manager client, make sure the command line doesn't exceed 1024 characters. When the command line is greater than 1024 characters, the client installation fails.



## New Windows 10 devices

For new Windows 10 devices, you can use the Autopilot service to configure the out of box experience, which includes joining the device to AD and Azure AD, as well as enrolling the device in Intune. Then, create an app in Intune to deploy the Configuration Manager client.  

1. Enable AutoPilot for the new Windows 10 devices. For details, see [Overview of Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > Starting in version 1802, use Configuration Manager to collect and report the device information required by the Microsoft Store for Business and Education. This information includes the device serial number, Windows product identifier, and a hardware identifier. In the Configuration Manager console, **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node. Run the new report, **Windows AutoPilot Device Information** and view the results. In the report viewer click the **Export** icon, and select the **CSV (comma delimited)** option. After saving the file, upload the data to the Microsoft Store for Business and Education. For more information, see [add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configure automatic enrollment in Azure AD for your devices to be automatically enrolled into Intune. For details, see [Enroll Windows devices for Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

3. Create an app in Intune with the Configuration Manager client package and deploy the app to Windows 10 devices that you want to co-manage. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   



## Windows 10 devices not enrolled in Intune or a Configuration Manager client

For Windows 10 devices that aren't enrolled in Intune or have the Configuration Manager client, you can use automatic enrollment to enroll the device in Intune. Then, create an app in Intune to deploy the Configuration Manager client.

1. Configure automatic enrollment in Azure AD for your devices to be automatically enrolled into Intune. For details, see [Enroll Windows devices for Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

2. Create an app in Intune with the Configuration Manager client package and deploy the app to Windows 10 devices that you want to co-manage. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).



## Windows 10 devices enrolled in Intune

For Windows 10 devices that are already enrolled in Intune, create an app in Intune to deploy the Configuration Manager client. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  



## Next steps

[Switch Configuration Manager workloads to Intune](co-management-switch-workloads.md)
