---
# required metadata

title: Upgrade Readiness
titleSuffix: "Configuration Manager"
description: Integrate Upgrade Readiness with Configuration Manager. Access upgrade compatibility data in your admin console. Target devices for upgrade or remediation.
keywords:
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
  - configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: maayan
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Integrate Upgrade Readiness with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Upgrade Readiness (formerly Upgrade Analytics) enables you to assess and analyze device readiness with Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager admin console. You are able to target devices for upgrade or remediation from the device list.

Upgrade Readiness is a solution in the Microsoft Operations Management Suite (OMS). You can read more about Upgrade Readiness in [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## Configure clients

There are several configuration steps that you have to take to ensure that your clients can provide data to Upgrade Readiness:

-  Configure client telemetry settings as described in [Configure Windows telemetry in your organization](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Install the KBs described in the *Deploy the compatibility update and related KBs *section of [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

	> [!NOTE]
	> You can download a script to automate many of the client setup tasks. See the *Run the Upgrade Readiness deployment script* section of [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) for information about the script.

## Connect to Upgrade Readiness

### Prerequisites

Beginning with Current Branch version 1706, the Azure Services Wizard is used to simplify the process of configuring Azure services you use with Configuration Manager. In order to use the wizard, you need to configure an Azure web app. For more information, see, [Azure Services Wizard](/sccm/core/servers/deploy/configureazure-services-wizard).

### Use the Azure Wizard to create the connection

1.  In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and then click **Azure Services**.
2.  On the **Home** tab, in the **Azure Services** group, click **Configure Azure Services**.
3.  Type a friendly Name on the Azure Services page. You can also type a description. Then select **Upgrade Readiness Connector** and click **Next**.
4.  Specify your Azure environment on the App page. Click **Browse** to set up a server app.
5.  Click **Import** to connect to your Web app in Azure.
    -  Type the **Azure AD Tenant Name**.
    -  Type the **Azure AD Tenant ID**.
    -  Type the **Application Name**.
    -  Type the **Client ID**.
    -  Type the **Secret Key**.
    -  Select the date for the **Secret Key Expiry** date.
    -  Type any URL for the **Application ID URI**.
    -  Click **Verify**, and then click **OK**.

6.	Specify the connection to Upgrade Readiness on the Configuration page. Select the following values:  
    -  Azure subscriptions
    -  Azure resource group
    -  Windows Analytics workspace
8.	Click **Next**. You can review your connection in the Summary page. 

## Complete Upgrade Readiness tasks  

After you've create the connection, perform these tasks, as described in [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).  

1. Add the UpgradeReadiness service to the OMS workspace.  
2. Generate a commercial ID.  
3. Subscribe to Upgrade Readiness.   

## Use the Upgrade Readiness deployment script  

You can automate many of the Upgrade Readiness tasks and troubleshoot data sharing issues with the Microsoft **Upgrade Readiness deployment script**.  
The Upgrade Readiness deployment script does the following:  

- Sets commercial ID key + CommercialDataOptIn + RequestAllAppraiserVersions keys.  
- Verifies that user computers can send data to Microsoft.  
- Checks whether the computer has a pending restart.   
- Verifies that the latest version of KB package 10.0.x is installed (requires 10.0.14913 or subsequent releases).  
- If enabled, turns on verbose mode for troubleshooting.  
- Initiates the collection of the telemetry data that Microsoft needs to assess your organization’s upgrade readiness.  
- If enabled, displays the script’s progress in a cmd window. This provides visibility into issues (success or fail for each step) and/or writes to log file.  

## To run the Upgrade Readiness deployment script:  

1. Download the [Upgrade Readiness deployment script](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) and extract UpgradeReadiness.zip. The files in the **Diagnostics** folder are necessary only if you plan to run the script in troubleshooting mode.  
2. Edit these parameters in RunConfig.bat:  
- Storage location for log information. Example: %SystemDrive%\URDiagnostics. You can store log information on a remote file share or a local directory. If the script is blocked from creating the log file for the given path, it creates the log files in the drive with the Windows directory.  
- Commercial ID key.  
- By default, the script sends log information to both the console and the log file. To change the default behavior, use one of the following options:  
	- logMode = 0 log to console only  
	- logMode = 1 log to file and console  
	- logMode = 2 log to file only  
    - For troubleshooting, set **isVerboseLogging** to **$true** to generate log information that can help with diagnosing issues. By default, **isVerboseLogging** is set to **$false**. Ensure the Diagnostics folder is installed in the same directory as the script to use this mode.  
	- Notify users if they need to restart their computers. By default, this is set to off.  

3. After you finish editing the parameters in RunConfig.bat, run the script as an administrator.  


## View Microsoft Upgrade Readiness properties in Configuration Manager  

1.  In the Configuration Manager console, navigate to **Cloud Services**, then choose **OMS Connector** to open the **OMS Connection Properties** page.  

2.  Within this page there are two tabs:
  * The **Azure Active Directory** tab shows your **Tenant**, **Client ID**, **Client secret key expiration**, and allows you to **Verify** your **Client secret key** if it has expired.
  * The **Upgrade Readiness** tab shows your **Azure subscription**, **Azure resource group**, and **Operations Management Suite workspace**.

## View and use the upgrade information

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness and then take action.

1. In the Configuration Manager console, choose **Monitoring** > **Overview** > **Upgrade Readiness**.
2. Review the data, which includes the upgrade readiness state and the percent of Windows devices that are reporting telemetry.
3. You can filter the dashboard to view data for devices in specific collections.
4. You can view the devices in a particular readiness state, and create a dynamic collection for those devices so that you can upgrade those devices if ready, or take action to bring them to a readiness state.

## Create a connection to Upgrade Readiness (1702 and earlier)

Before the 1706 branch of Configuration Manager, to create a connection to Upgrade Readiness required the following steps.

### Prerequisites

- In order to add the connection, your Configuration Manager environment must first configure a [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in an [online mode](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). When you add the connection to your environment, it will also install the Microsoft Monitoring Agent on the machine running this site system role.
- Register Configuration Manager as a “Web Application and/or Web API” management tool, and get the [client ID from this registration](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Create a client key for the registered management tool in Azure Active Directory.
- In the Azure portal, provide the registered web app with permission to access OMS, as described in [Provide Configuration Manager with permissions to OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
	> When configuring permission to access OMS, be sure to choose the **Contributor** role, and assign it permissions to the resource group of the registered app.

### Create the connection

1.  In the Configuration Manager console, choose **Administration** > **Cloud Services** > **Upgrade Readiness Connector** > **Create Connection to Upgrade Analytics** to start the **Add Upgrade Analytics Connection Wizard**.
3.  On the **Azure Active Directory** screen, provide **Tenant**, **Client ID**, and **Client secret key**, then select **Next**.
4.  On the **Upgrade Readiness** screen, provide your connection settings by filling in your **Azure subscription**, **Azure resource group**, and **Operations Management Suite workspace**.
5.  Verify your connection settings on the **Summary** screen, then select **Next**.

	> [!NOTE]
	> You must connect Upgrade Readiness to the top-tier site in your hierarchy. If you connect Upgrade Readiness to a standalone primary site and then add a central administration site to your environment, you must delete and recreate the OMS connection within the new hierarchy.
