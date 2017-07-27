---
title: "Install and assign the client from the internet | Microsoft Docs"
description: "Install and assign the System Center Configuration Manager client from the internet."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe

---

# Install and assign Configuration Manager clients from the Internet using Azure AD for authentication

You can use Configuration Manager cloud services with Azure AD to support the following scenarios:

- Manually install the Configuration Manager client from the internet and have it assign to a Configuration Manager site (requires the cloud management gateway site system role).
- Use Azure AD to authenticate clients on the Internet to access your Configuration Manager sites. Azure AD replaces the need to configure and use client authentication certificates.
- Discover Azure AD users into your site to use in collections, and other Configuration Manager operations.

Use the following steps to help you accomplish this:

- **Step 1: Set up the Cloud Management Gateway**
- **Step 2: Set up the Azure Services app in Configuration Manager Cloud Services**
- **Step 3: Configure client settings to register Windows 10 devices with Azure AD**
- **Step 4: Install and register the Configuration Manager client using Azure Active Directory Identity**


## Before you start

- You must have an Azure AD tenant.
- Your devices must run Windows 10 and be Azure AD joined. Clients can also be domain joined in addition to Azure AD joined).
- In addition to the [existing prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) for the management point site system role, you must additionally ensure that **ASP.NET 4.5** (and any other options that are automatically selected with this) are enabled on the computer that hosts this site system role.
- To use Configuration Manager to deploy the client:
	- At least one management point must be configured for HTTPS mode.
	- You must set up a Cloud Management Gateway.

## Step 1: Set up the Cloud Management Gateway

Set up the Cloud Management Gateway to let clients access your Configuration Manager site from the internet without using certificates 
You'll find help about how to do this in the following topics: 
•	[Plan for cloud management gateway in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
•	[Set up cloud management gateway for Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
•	[Monitor cloud management gateway in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## Step 2: Set up the Azure Services app in Configuration Manager Cloud Services

This connects your Configuration Manager site to Azure AD and is a prerequisite for all other operations in this section. To do this: 

1.	In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and then click **Azure Services**.
2.	On the **Home** tab, in the **Azure Services** group, click **Configure Azure Services**.
3.	On the **Azure Services** page of the Azure Services Wizard, select **Cloud Management** to allow clients to authenticate with the hierarchy using Azure AD.
4.	On the **General** page of the wizard, specify a name, and a description for your Azure service.
5.	On the **App** page of the wizard, select your Azure environment from the list, then click **Browse** to select the server and client apps that will be used to configure the Azure service:
	- In the **Server App** window, select the server app you want to use, and then click **OK**. Server apps are the Azure web apps that contain the configurations for your Azure account, including your Tenant ID, Client ID, and a secret key for clients. If you do not have an available server app, use one of the following:
		- **Create:** To create a new server app, click **Create**. Provide a friendly name for the app and the tenant. Then, after you sign-in to Azure, Configuration Manager creates the web app in Azure for you, including the Client ID and secret key for use with the web app. Later, you can view these from the Azure portal.
		- **Import:** To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you Verify the information, click **OK** to continue. This option is not currently available in this technical preview.
	- Repeat the same process for the client app.
You need to grant the **Read directory data** application permission when you use **Application Import**, to set the correct permissions in the portal. If you use **Application Creation** the permissions are automatically created with the application, but you still need to give consent to the application in the Azure portal.
6.	On the **Discovery** page of the wizard, optionally **Enable Azure Active Directory User Discovery**, and then click **Settings**. In the **Azure AD User Discovery Settings** dialog box, configure a schedule for when discovery occurs. You can also enable delta discovery which checks for only new, or changed accounts in Azure AD.
7.	Complete the wizard.
	
At this point, you have connected your Configuration Manager site to Azure AD. 

## Step 3: Configure client settings to register Windows 10 devices with Azure AD

1.	Configure the following client settings (found in the Cloud Services) section using the information in [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).
	- **Automatically register new Windows 10 domain joined devices with Azure Active Directory** – Set to **Yes** (default), or **No**.
	- **Enable clients to use a cloud management gateway** – Set to **Yes** (default), or **No**.
2.	Deploy the client settings to the required collection of devices.

To confirm that the device is joined to Azure AD, run the command **dsregcmd.exe /status** in a command prompt window. The **AzureAdjoined** field in the results will show **YES** if the device is Azure AD joined.


## Step 4: Install and register the Configuration Manager client using Azure Active Directory Identity

Before you start, ensure that the client installation source files are stored locally on the device to which you want to install the client. Then, use the instructions in [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) using the following installation command line (replace the values in the example with your own values): 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck:** If your management point or cloud management gateway uses a non-public server certificate, then the client might not be able to reach the CRL location.
- **/Source:** Local folder: Location of the client installation files.
- **CCMHOSTNAME:** The name of your Internet management point. You can find this by running **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** from a command prompt on a managed client.
- **SMSMP:** The name of your lookup management point – this can be on your intranet.
- **SMSSiteCode:** The site code of your Configuration Manager site.
- **AADTENANTID:**, **AADTENANTNAME:** The ID and name of the Azure AD tenant you linked to Configuration Manager. You can find this by running dsregcmd.exe /status from a command prompt on an Azure AD joined device.
- **AADCLIENTAPPID:** The Azure AD client app ID. For help finding this, see [Use portal to create an Azure Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri:** The identifier URI of the onboarded Azure AD server app.


## Next steps

Once complete, you can continue to [monitor and manage clients](/sccm/core/clients/manage/monitor-clients).
