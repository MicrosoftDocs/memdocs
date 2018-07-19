---
title: Microsoft Store for Business
titleSuffix: Configuration Manager
description: Manage and deploy apps from the Microsoft Store for Business with Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage apps from the Microsoft Store for Business with Configuration Manager

The [Microsoft Store for Business](https://www.microsoft.com/business-store) is where you find and acquire Windows apps for your organization. When you connect the store to Configuration Manager, you then synchronize the list of apps you've acquired. View these apps in the Configuration Manager console, and deploy them like you deploy any other app.


## <a name="bkmk_apps"></a> Online and offline apps

The Microsoft Store for Business supports two types of app:

- **Online**: This license type requires users and devices to connect to the store to get an app and its license. Windows 10 devices must be Azure Active Directory (Azure AD) domain-joined.  

- **Offline**: This type lets you cache apps and licenses to deploy directly within your on-premises network. Devices don't need to connect to the store or have a connection to the internet.

[Read more](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) about the Microsoft Store for Business.

Configuration Manager supports managing Microsoft Store for Business apps on both Windows 10 devices with the Configuration Manager client, and also Windows 10 devices enrolled with Microsoft Intune. Configuration Manager offers the following capabilities for online and offline apps:


|Capability|Offline apps|Online apps|
|------------|------------|------------|
|Synchronize app data to Configuration Manager<br>(synchronization occurs every 24 hours)|Yes|Yes|
|Create Configuration Manager applications from store apps|Yes|Yes|
|Support for free apps from the store|Yes|Yes|
|Support for paid apps from the store|No|Yes<sup>1</sup>|
|Support required deployments to user or device collections|Yes|Yes|
|Support available deployments to user or device collections|Yes|Yes|
|Support line-of-business apps from the store|Yes|Yes|
|Provision a store app for all users on a device<sup>2</sup><!--1358310-->|Yes|Yes|

- <sup>1</sup> To deploy online licensed apps to Windows 10 devices with the Configuration Manager client, they must be running Windows 10, version 1703 or later.  

- <sup>2</sup> Starting in version 1806. For more information, see [Create Windows applications](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  


### Deploying online apps using the Microsoft Store for Business to devices that run the Configuration Manager client

Before deploying Microsoft Store for Business apps to devices that run the full Configuration Manager client, consider the following points:

- For full functionality, devices must be running Windows 10, version 1703 or later.  

- Devices must be joined to Azure AD in the same tenant where you registered the Microsoft Store for Business as a management tool.  

- When the local Administrator account signs in on the device, it can't access Microsoft Store for Business apps.  

- Devices must have a live internet connection to the Microsoft Store for Business. For more information including proxy configuration, see [Prerequisites](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  


### Notes for devices running earlier versions of Windows 10

On devices with the Configuration Manager client and running Windows 10 version 1607 or earlier, the following functionality applies:  

When you enforce installation of the app on the device by one of the following methods:  

- The user installs the app  

- The deployment reaches its installation deadline   

- Post-installation re-evaluation for required deployments  

Then the following behaviors occur:  

- The Configuration Manager client "enforces" the app by launching the Microsoft Store for Business app  

- The user must complete the installation from the store  

- In the Configuration Manager console, the app deployment status reports failure with the following error: "The Microsoft Store app was opened on the client PC and is waiting for the user to complete the installation."  

At the next application evaluation cycle:  

- If user installed the application from the store, the application reports the status **Success**  

- If the user didn't try to install the app from the store:  

	- For required deployments, the Configuration Manager client tries to launch the store app again  

	- Available deployments aren't re-enforced


#### Further notes for devices running earlier versions of Windows 10:

- You can't deploy line-of-business apps from the Microsoft Store for Business  

- When you deploy paid apps from the store, users must sign in to the store and acquire the app themselves  

- If you deploy a group policy to disable access to the consumer version of the Microsoft Store, deployments from the Microsoft Store for Business don't work. This behavior occurs even if the Microsoft Store for Business is enabled.  



## <a name="bkmk_setup"></a> Set up Microsoft Store for Business synchronization

Synchronizing the list of apps acquired by your organization lets you see these apps in the Configuration Manager console.

Connect your Configuration Manager site to Azure AD and the Microsoft Store for Business. For more information and details of this process, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard). Create a connection to the **Microsoft Store for Business** service.


### <a name="bkmk_config"></a> Supplemental information and configuration 

On the **App** page of the Azure Services Wizard, first configure the **Azure environment** and **Web app**. Then read the **More Information** section at the bottom of the page. This information includes the following additional actions in the Microsoft Store for Business portal:  

- Configure Configuration Manager as the store management tool. For more information, see [Configure management provider](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Enable support for offline licensed apps. For more information, see [Distribute offline apps](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Acquire at least one app. For more information, see [Find and acquire apps](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

On the **Configurations** page of the Azure Services Wizard, specify the following information:  

- **Path to Microsoft Store for Business app content storage**: Specify a shared network path, including a folder of the share. For example, `\\server\share\folder`.  

- **Selected languages**: Select the languages to display to users for apps you sync with the Microsoft Store for Business.  

- **Default language**: If the user's language is unavailable, select a default language to use.  



## <a name="bkmk_deploy"></a> Create and deploy a Configuration Manager application from a Microsoft Store for Business app

After synchronization, create and deploy the store apps similar to any other app.

1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.  

2.  Choose the app you want to deploy, then click **Create Application** in the ribbon.  

The site creates a Configuration Manager application containing the Microsoft Store for Business app. 

Then deploy and monitor this application as you would any other Configuration Manager application. For more information, see the following articles:  
- [Deploy applications](/sccm/apps/deploy-use/deploy-applications)
- [Monitor applications from the console](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> For devices enrolled with Microsoft Intune, deployed apps are only available to the user who originally enrolled the device. No other users can access the app.



## Next steps

In the **Software Library** workspace, expand **Application Management**, then click **License Information for Store Apps**.

For each store app you manage, view the following information about the app:
- App name
- App platform
- The number of licenses for the app that you own
- The number of available licenses

After deploying online apps, any updates to that app come directly from the Microsoft Store. Furthermore, Configuration Manager doesn't check version compliance of online apps, just that Windows reports the app as installed.  

When deploying offline apps to Windows 10 devices with the Configuration Manager client, don't allow users to update applications external to Configuration Manager deployments. Control of updates to offline apps is especially important in multi-user environments such as classrooms. One option to disable the Microsoft Store is by using [group policy](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

After the Microsoft Store for Business administrator acquires an offline app, don't publish the app to users via the store. This configuration ensures that users can't install or update online. Users only receive offline app updates via Configuration Manager. 
