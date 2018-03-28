---
# required metadata

title: Prepare Windows 10 for co-management
titleSuffix: Configuration Manager
description: Learn how to prepare your Windows 10 devices for co-management.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624


---

# Prepare Windows 10 devices for co-management
You can enable co-management on Windows 10 devices that are joined to AD and Azure AD, and enrolled in Microsoft Intune and a client in Configuration Manager. For new Windows 10 devices, and for devices that are already enrolled in Intune, install the Configuration Manager client before they can be co-managed. For Windows 10 devices that are already Configuration Manager clients, you can enroll the devices with Intune and enable co-management in the Configuration Manager console.

> [!IMPORTANT]
> Windows 10 mobile devices do not support co-management.



## Command line to install Configuration Manager client
Create an app in Intune for Windows 10 devices that are not already Configuration Manager clients. When you create the app in the next sections, use the following command line:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

For example, if you had the following values:

- **URL of cloud management gateway mutual auth endpoint**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >Use the **MutualAuthPath** value in the **vProxy_Roles** SQL view for the **URL of cloud management gateway mutual auth endpoint** value.

- **FQDN of management point (MP)**: mp1.contoso.com    
- **Sitecode**: PS1    
- **Azure AD tenant ID**: daf4a1c2-3a0c-401b-966f-0b855d3abd1a    
- **Azure AD client app ID**: 7506ee10-f7ec-415a-b415-cd3d58790d97     
- **AAD Resource ID URI**: ConfigMgrServer    

  > [!Note]    
  > Use the **IdentifierUri** value found in the **vSMS_AAD_Application_Ex** SQL view for the **AAD Resource ID URI** value.

You would use the following command line:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://ConfigMgrServer"`

> [!Tip]
> You can find the command-line parameters for your site by using the following steps:     
> 1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
> 2. On the Home tab, in the Manage group, choose **Configure co-management** to open the Co-management Onboarding Wizard.    
> 3. On the Subscription page, click **Sign In** and sign in to your Intune tenant, and then click **Next**.    
> 4. On the Enablement page, click **Copy** in the **Devices enrolled in Intune** section to copy the command line to the clipboard, and then save the command line to use in the procedure to create the app.  
> 5. Click **Cancel** to exit the wizard.

> [!Important]    
> If you customize the command line to install the Configuration Manager client, make sure the command line does not exceed 1024 characters. When the command line is greater than 1024 characters, the client installation fails.


## New Windows 10 devices
For new Windows 10 devices, you can use the Autopilot service to configure the out of box experience, which includes joining the device to AD and Azure AD, as well as enrolling the device in Intune. Then, create an app in Intune to deploy the Configuration Manager client.  
1. Enable AutoPilot for the new Windows 10 devices. For details, see [Overview of Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > Starting in version 1802, use Configuration Manager to collect and report the device information required by the Microsoft Store for Business and Education. This information includes the device serial number, Windows product identifier, and a hardware identifier. In the Configuration Manager console, **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node. Run the new report, **Windows AutoPilot Device Information** and view the results. In the report viewer click the **Export** icon, and select the **CSV (comma delimited)** option. After saving the file, upload the data to the Microsoft Store for Business and Education. For more information, see [add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configure automatic enrollment in Azure AD for your devices to be automatically enrolled into Intune. For details, see [Enroll Windows devices for Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Create an app in Intune with the Configuration Manager client package and deploy the app to Windows 10 devices that you want to co-manage. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## Windows 10 devices not enrolled in Intune or a Configuration Manager client
For Windows 10 devices that are not enrolled in Intune or have the Configuration Manager client, you can use automatic enrollment to enroll the device in Intune. Then, create an app in Intune to deploy the Configuration Manager client.
1. Configure automatic enrollment in Azure AD for your devices to be automatically enrolled into Intune. For details, see [Enroll Windows devices for Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Create an app in Intune with the Configuration Manager client package and deploy the app to Windows 10 devices that you want to co-manage. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## Windows 10 devices enrolled in Intune
For Windows 10 devices that are already enrolled in Intune, create an app in Intune to deploy the Configuration Manager client. Use the [command line to install Configuration Manager client](#command-line-to-install-configuration-manager-client) when you go through the steps to [install clients from the Internet using Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## Next steps
[Switch Configuration Manager workloads to Intune](co-management-switch-workloads.md)