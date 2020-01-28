---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Integrate Upgrade Readiness with Configuration Manager to access Windows 10 upgrade compatibility data and target devices for upgrade or remediation.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
---

# Integrate Upgrade Readiness with Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!Important]  
> The Windows Analytics service is retired as of January 31, 2020.
>
> [Desktop Analytics](/sccm/desktop-analytics/overview) is the evolution of Windows Analytics. Existing Windows Analytics customers can [migrate data to Desktop Analytics](/sccm/desktop-analytics/faq#existing-windows-analytics-customers).
>
> For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

If your Configuration Manager site had a connection to Upgrade Readiness, you need to remove it and reconfigure clients.

## <a name="bkmk_remove"></a> Remove Upgrade Readiness connection

1. Open the Configuration Manager console as a user with the **Full administrator** role.

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.

1. Delete the Windows Analytics service.

## Reconfigure clients

### Unenroll devices

On enrolled devices, remove the CommercialID value from the following Windows Registry keys:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### Windows diagnostic data configuration

If you don't want your devices to continue sending diagnostic data:

- Windows 10: set the diagnostic data level to **Security**
- Windows 7 SP1 or 8.1: disable the **Commercial Data Opt-in Key**

Set these values using one of the following methods:

- Group policy, in **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**
- Mobile device management (MDM), such as [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> When you apply these changes, devices immediately stop sending diagnostic data. It may take 24-48 hours for Microsoft to stop processing insights for your workspace. Microsoft deletes this data from its cloud services within 30 days or less.

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](/sccm/core/servers/deploy/configure/azure-services-wizard) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
