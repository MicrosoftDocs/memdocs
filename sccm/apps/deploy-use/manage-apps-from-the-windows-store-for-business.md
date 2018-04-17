---
title: "Manage apps from the Microsoft Store for Business"
titleSuffix: "Configuration Manager"
description: "Manage and deploy apps from the Microsoft Store for Business by using System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: aczechowski
ms.author: aaroncz
manager: angrobe
---

# Manage apps from the Microsoft Store for Business with System Center Configuration Manager
The [Microsoft Store for Business](https://www.microsoft.com/business-store) is where you can find and purchase Windows apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can synchronize the list of apps you've purchased with Configuration Manager. You can then view these apps in the Configuration Manager console, and deploy them like you would deploy any other app.


## Online and offline apps

The Microsoft Store for Business supports two types of app:

- **Online** - This license type requires users and devices to connect to the store to get an app and its license. Windows 10 devices must be Azure Active Directory domain-joined.
- **Offline** - Lets you cache apps and licenses to deploy directly within your on-premises network. Devices do not need to connect to the store or have a connection to the Internet.

[Read more](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) about the Microsoft Store for Business.

Configuration Manager supports managing Microsoft Store for Business apps on both Windows 10 devices with the Configuration Manager client, and also Windows 10 devices enrolled with Microsoft Intune. Configuration Manager offers the following capabilities for online and offline apps.

> [!IMPORTANT]
> To use Microsoft Store for Business, Windows 10 devices must be running the November 2015 (1511) release or later.


|Capability|Offline apps|Online apps|
|------------|------------|------------|
|Synchronize app data to Configuration Manager<br>(synchronization occurs every 24 hours)|Yes|Yes|
|Create Configuration Manager applications from store apps|Yes|Yes|
|Support for free apps from the store|Yes|Yes|
|Support for paid apps from the store|No|Yes<sup>1</sup>|
|Support required deployments to user or device collections|Yes|Yes|
|Support available deployments to user or device collections|Yes|Yes|
|Support line-of-business apps from the store|Yes|Yes|

<sup>1</sup>To deploy online licensed apps to Windows 10 PCs with the Configuration Manager client, they must be running the Windows 10 Creators Update, or later.

### Deploying online apps using the Microsoft Store for Business with PCs that run the Configuration Manager client
Before deploying Microsoft Store for Business apps to PCs that run the full Configuration Manager client, consider the following points:

- For full functionality, PCs must be running the Windows 10 Creators Update, or later.
- PCs must be joined to Azure Active Directory in the same tenant where you registered the Microsoft Store for Business as a management tool.
- When PCs are logged in with the built-in Administrator account, they cannot access Microsoft Store for Business apps.
- PCs must have a live internet connection to the Microsoft Store for Business.

### Notes for PCs running earlier versions of Windows 10
On PCs running a version of Windows 10 earlier than the Creators Update (with the Configuration Manager client), the following functionality applies:


- When enforcing installation by the user installing the application, the application reaching its installation deadline, or by post-installation re-evaluation for required deployments:
	- The application is "enforced" by launching the Microsoft Store for Business app. 
	- The end user must then complete the installation from the store before the app is installed
	- In the Configuration Manager console the application status reports failure with the following error: "The Microsoft Store app was opened on the client PC and is waiting for the user to complete the installation."
- At the next application evaluation cycle:
	- If the application was installed by the end user from the store, the application reports the Status **Success**. 
	- If the end user did not attempt to install the app from the store:
		- Required deployments attempt to launch the store and enforce the application installation again.
		- Available deployments are not re-enforced.

#### Further notes for PCs running earlier versions of Windows 10:

- You cannot deploy line-of-business apps from the Microsoft Store for Business
- When you deploy paid apps from the store, end users must log in to the store and purchase the app themselves.
- If you deploy a group policy to disable access to the consumer version of the Microsoft Store, deployments from the Microsoft Store for Business do not work, even if the Microsoft Store for Business is enabled.


## Set up Microsoft Store for Business synchronization
Synchronizing the list of apps purchased by your organization lets you see these apps in the Configuration Manager console.

<!-- Remove below after 1802... -->
### For Configuration Manager versions prior to 1706

**In Azure Active Directory, register Configuration Manager as a "Web Application and/or Web API" management tool. This action gives you a client ID that you need later.**
1. In the Active Directory node of [https://manage.windowsazure.com](https://manage.windowsazure.com), select your Azure Active Directory, then click **Applications** > **Add**.
2.  Click **Add an application my organization is developing**.
3.  Enter a name for the application, select **Web application** and/or **Web API**, then click the **Next** arrow.
4.  Enter the same URL for both the **Sign-on URL** and **App ID URI**. The URL can be anything and does not need to resolve to a real address. For example, you can enter *https://yourdomain/sccm*.
5.  Complete the wizard.

**In Azure Active Directory, create a client key for the registered management tool**
1.  Highlight the application you created and click **Configure**.
2.  Under **Keys**, select a duration from the list, and then click **Save**. This action creates a new client key. Do not navigate away from this page until you have successfully onboarded the Microsoft Store for Business to Configuration Manager.

**In the Microsoft Store for Business, configure Configuration Manager as the store management tool**
1.  Open [https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools) and sign-in if prompted.
2.  Accept the terms of use if requested.
3.  Under **Management Tools**, click **Add a management tool**.
4.  In **Search for the tool by name**, type the name of the application you created in AAD previously, then click **Add**.
5.  Click **Activate** next to the application you imported.
6.  In the **Manage > Account Information** page, select **Show Offline-Licensed Apps** if you want to allow offline-licensed apps to be purchased.

**Add the store account to Configuration Manager**

1. Ensure you have purchased at least one app from the Microsoft Store for Business. In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, then click **Microsoft Store for Business**.
2.  On the **Home** tab, in the **Microsoft Store for Business** group, click **Add Microsoft Store for Business Account**. 
3.  Add your tenant ID, client ID, and client key from Azure Active Directory, then complete the wizard.
4. Once you are done, you can see the account under **Microsoft Store for Business** in the Configuration Manager console.

### For Configuration Manager version 1706 and later
<!-- ...remove above after 1802 -->

1. In the console, go to **Administration** > **Cloud Services** > **Azure Services**, and then choose **Configure Azure Services** to start the **Azure Services Wizard**.
2. On the **Azure Services** page, select the service you want to configure, and then click **Next**.
3. On the **General** page, provide a friendly name for the Azure service name and an optional description, and then click **Next**.
4. On the **App** page, specify your Azure environment, and then click **Browse** to open the **Server App** window.
5. In the **Server App** window, select the server app you want to use, and then click **OK**. Server apps are the Azure web apps that contain the configurations for your Azure account, including your tenant ID, client ID, and a secret key for clients. If you do not have an available server app, use one of the following actions:
	- **Create:** To create a new server app, click **Create**. Provide a friendly name for the app and the tenant. Then, after you sign in to Azure, Configuration Manager creates the web app in Azure for you, including the client ID and secret key for use with the web app. Later, you can view these values from the Azure portal.
	- **Import:** To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant. Then specify the tenant ID, client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you **Verify** the information, click **OK** to continue. 
6. Review the **Information** page and complete any additional steps and configurations as directed. These configurations are necessary to use the service with Configuration Manager. For example, to configure the Microsoft Store for Business:
	- In Azure, you must register Configuration Manager as a web application or Web API and record the client ID. You also specify a client key for use by the management tool (which is Configuration Manager).
	- In the Microsoft Store for Business portal you must configure Configuration Manager as the store management tool, enable support for offline licensed apps, and then purchase at least one app. 
7. Click **Next** when you are ready to continue.
8. On the **App Configurations** page, complete the app catalog and language configurations for this service, and then click **Next**.
9. After the wizard completes, the Configuration Manager console shows that you have configured **Microsoft Store for Business** as a **Cloud Service Type**.




## Create and deploy a Configuration Manager application from a Microsoft Store for Business app
After synchronization, create and deploy the store apps like you would any other app.

1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.
2.  Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.
A Configuration Manager application is created containing the Microsoft Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.

> [!IMPORTANT]
> For devices enrolled with Microsoft Intune, deployed apps are only available to the user who originally enrolled the device. No other users can access the app.

## Next steps

In the **Software Library** workspace, expand **Application Management**, then click **License Information for Store Apps**.

For each store app you manage, you can view information about the app. This information includes the app name, platform, the number of licenses for the app that you own, and the number of licenses you have available.

After deploying online apps, any updates to that app will come directly from the Microsoft Store. Furthermore, Configuration Manager does not check version compliance of online apps, just that Windows reports the app as installed.  

When deploying offline apps to Windows 10 devices with the Configuration Manager client, do not allow users to update applications external to Configuration Manager deployments. Control of updates to offline apps is especially important in multi-user environments such as classrooms. One option to disable the Microsoft Store is by using [group policy](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

After the Microsoft Store for Business administrator purchases an offline app, do not publish the app to users via the store. This configuration ensures that users can't install or update online. Users will only receive offline app updates via Configuration Manager. 
