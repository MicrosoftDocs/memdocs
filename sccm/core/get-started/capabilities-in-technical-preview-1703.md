---
title: "Capabilities in Technical Preview 1703 Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1703."
ms.custom: na
ms.date: 03/30/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1703 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1703. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Deploy volume-purchased iOS apps to device collections

You can now deploy licensed apps to devices as well as users. Depending on the apps ability to support device licensing, an appropriate license will be claimed when you deploy it, as follows:

|||||
|-|-|-|-|
|Configuration Manager version|App supports device licensing?|Deployment collection type|Claimed license|
|Earlier than 1702|Yes|User|User license|
|Earlier than 1702|No|User|User license|
|Earlier than 1702|Yes|Device|User license|
|Earlier than 1702|No|Device|User license|
|1702 and later|Yes|User|User license|
|1702 and later|No|User|User license|
|1702 and later|Yes|Device|Device license|
|1702 and later|No|Device|User license|

For more information about volume-purchased iOS apps, see [Manage volume-purchased iOS apps](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## Direct links to applications in Software Center

You can now provide end users with a direct link to an application in Software Center. This means they no longer must open Software Center and search for an application before they can install it.
This is available only for Configuration Manager applications, not packages and programs or task sequences.

### Try it out                 

Use the following URL format to open Software Center to a particular application:

**Softwarecenter:SoftwareId=*Application Identifier***

### How to get the application identifier of an application.

1.	In the Configuration Manager console, click **Software Library**.
2.	In the Software Library workspace, expand **Application Management**, and then click **Applications**.
3.	In the **Applications** view, right-click one of the column headers, and then, from the list, select **CI Unique ID**. You’ll see that the unique ID of each application is now shown in the list.
4.	Note the **CI Unique ID** of the application you want to provide a link to, for example:
**ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.	Then, remove any text following the application GUID, in this case **/2**. This leaves you with the application identifier.
6.	Finally, to finish constructing the link, precede it with **Softwarecenter:SoftwareID=**. Using the example above, the final link will read:
**Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

By using this link, end users can open Software Center directly to the application you specified.


## PFX certificates for Configuration Manager Windows client computers

You can now deploy PFX certificate profiles you imported to Configuration Manager client computers running Windows 10.

### Try it out

Use the instructions in [How to create PFX certificate profiles](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) to import a PFX profile, deploy the profile, and then check if the certificate was installed for the targeted user.



## Configure Azure Services wizard
Technical preview 1703 introduces the **Configure Azure Services** wizard. This wizard provides a common configuration experience that replaces the individual workflows to set up the cloud services you use with Configuration Manager. This is done by using an **Azure web app** to provide the subscription and configuration details that you otherwise enter each time you set up a new Configuration Manager component or service with Azure.

With technical preview 1703, only Windows Store for Business (WSfB) is configured by using this wizard.  Other cloud services are configured by using their separate workflows.

-	Use the information in this preview topic to replace the configuration steps found in the [Set up Windows Store for Business synchronization](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) section of the Current Branch topic [Manage apps from the Windows Store for Business with System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-	For more information about web apps, see [Authentication and authorization in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), and [Web Apps overview](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### Prerequisites and planning
When you set up a connection between Configuration Manager and the Windows Store for Business, you must provide a folder where app content synchronized from the store will be kept. To ensure that this folder is secure and that its content can be deployed to devices, make sure the following permissions are in place:
-	The computer on which you install the service connection point site system role (the top-level site in the hierarchy) must have read and write permissions to the folder you specified when using the **Computer$** account.  

-	The app author must have read permissions to the folder you specified.  

-	The **Computer$** account of each computer that hosts an instance of the SMS Provider must be able to use the folder you specified.

In Azure Active Directory, register Configuration Manager as a web application or Web API management tool. This creates the client ID that you will need later.

### Use the wizard to configure the WSfB cloud service

1. In the console, go to **Administration** > **Overview** > **Cloud Services Management** > **Azure** > **Azure Services**, and then choose **Configure Azure Services** to start the **Azure Services Wizard**.

2. On the **Azure Services** page, select the service you want to configure, and then click **Next**. With this preview, only WSfB can be configured.

3. On the **General** page, provide a friendly name for the **Azure service name** and an optional description, and then click **Next**.

4. On the **App** page, specify your Azure environment, and then click **Browse** to open the Server App window.

5. In the **Server App** window, select the server app you want to use, and then click **OK**.
Server apps are the Azure web apps that contain the configurations for your Azure account, including your Tenant ID, Client ID, and a secret key for clients. If you do not have an available server app, use one of the following:
  -	**Create**: To create a new server app, click **Create**. Provide a friendly name for the app and the tenant. Then, after you sign-in to Azure, Configuration Manager creates the web app in Azure for you, including the Client ID and secret key for use with the web app. Later, you can view these from the Azure portal.
  -	**Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you **Verify** the information, click **OK** to continue.  </br></br>

6. Review the **Information** page and complete any additional steps and configurations as directed. These configurations are necessary to use the service with Configuration Manager.
For example, to configure WSfB:

  1. In Azure you must register Configuration Manager as a web application or Web API and record the client ID. You also specify a client key for use by the management tool (which is Configuration Manager).

  2.	In the WSfB console you must configure Configuration Manager as the store management tool, enable support for offline licensed apps, and then purchase at least one app.   </br>

  Click **Next** when you are ready to continue.

7. On the **App Configurations** page, complete the app catalog and language configurations for this service, and then click **Next**.
8. After the wizard completes, the Configuration Manager console shows that you have configured **Windows Store for Business** as a **Cloud Service Type**.

You can now use the remainder of the [Current Branch content](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) for managing apps from the WSfB to synchronize, create and deploy, and monitor Windows Store for Business Apps.

### Modify a cloud service configuration
You can view and edit the properties of a cloud service to modify the configuration.

In the console go to **Administration** > **Overview** > **Cloud Services Management** > **Azure** > **Azure Services**, and then choose **Configure Azure Services**, select a Cloud Service and then choose **Properties**.



## Convert from BIOS to UEFI in an operating system upgrade task sequence
Windows 10 Creators Update introduces a simple conversion tool that automates the process to repartition the hard disk for UEFI-enabled hardware and integrates the conversion tool into the Windows 10 in-place upgrade process. When you combine this tool with your operating system upgrade task sequence and the OEM tool that converts the firmware from BIOS to UEFI, you can convert your computers from BIOS to UEFI during an in-place upgrade to the Windows 10 Creators Update.

**Requirements**:
- Windows 10 Creators Update
- Computers that support UEFI
- OEM tool that converts the computer’s firmware from BIOS to UEFI

### To convert from BIOS to UEFI during an in-place upgrade
1.	Create an operating system upgrade task sequence that performs an in-place upgrade to Windows 10 Creators Update. For details, see [Create a task sequence to upgrade an operating system](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).
2.	Edit the task sequence. In the **Post-Processing group**, add the following task sequence steps:
    1.	From General, add a **Run Command Line** step. You will add the command line for the MBR2GPT tool that coverts a disk from MBR to GPT without modifying or deleting data from the disk. In Command line, type the following:  **MBR2GPT /convert /disk:0 /AllowFullOS**.

        > [!NOTE]  
            > You can also choose to run the MBR2GPT.EXE tool when in Windows PE instead of in the full operating system. You can do this by adding a step to restart the computer to WinPE before the step to run the MBR2GPT.EXE tool and removing the /AllowFullOS option from the command line. For details about the tool and available options, see [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).    

    2.	Add a step to start the OEM tool that will convert the firmware from BIOS to UEFI. This will typically be a Run Command Line task sequence step with a command line to start the OEM tool.
    3.	From General, add the **Restart Computer** step. For Specify what to run after restart, select **The currently installed default operating system**.
3.	Deploy the task sequence.


## Collapsible task sequence groups
This version introduces the ability to expand and collapse task sequence groups. You can expand or collapse individual groups or expand or collapse all groups at once.


## Client settings to configure Windows Analytics for Upgrade Readiness
Beginning with this version, you can use device client settings to simplify the configuration of Windows Analytics when you use [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) with Configuration Manager. Windows Analytics collects and reports telemetry data about your Configuration Manager clients to your Operations Manager Suite (OMS) workspace. The telemetry data you collect can help you prioritize decisions about Windows upgrades for your managed devices.

Telemetry data that Configuration Manager collects is in the form of the Event Tracing for Windows (ETW) log files. These log file are submitted to the Configuration Manager site when the client submits hardware inventory. These files are then transferred to your OMS workspace. The log files and their data are removed from your Configuration Manager site after the logs transfer to OMS.

For information about Windows telemetry settings, see [Configure Windows telemetry in your organization](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### Prerequisites
- You must have configured your site to use Log Analytics from the OMS Upgrade Readiness. For information see [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) in the content library for the Current Branch.
- Clients must use hardware inventory to submit the telemetry data.

### Configure Windows Analytics client settings
To configure Windows Analytics, in the Configuration Manager console go to **Administration** > **Client Settings**, double-click **Default Client Settings** and then select **Windows Analytics**.  

Then, configure the following:
- **Commercial ID**  
The commercial ID maps information from devices you manage to your OMS workspace. If you have already configured commercial ID for use with Upgrade Readiness for use with Configuration Manager, use that ID. If you do not yet have a commercial ID, see [Generate your commercial ID key]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Set a **Telemetry level for Windows 10 devices**   
For information about what is collected by each Windows 10 telemetry level, see  [Telemetry levels]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels) in the Windows on-line documentation.

- Choose to **opt-in to commercial data collection on Windows 7, 8 and 8.1 devices**   
For information about data collected from these operating systems when you opt-in, see download  the [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) pdf file from Microsoft.

- **Configure Internet Explore data collection**
