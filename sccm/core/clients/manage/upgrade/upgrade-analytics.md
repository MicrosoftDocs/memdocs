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

Upgrade Readiness (formerly Upgrade Analytics) is a part of [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) that allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. You can configure the specific version. Upgrade Readiness can be integrated with Configuration Manager to access client upgrade compatibility data in the Configuration Manager admin console. You are able to target devices for upgrade or remediation using dynamic collections created based on this data.

Upgrade Readiness is a solution that runs on [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). You can read more about Upgrade Readiness in [Manage Windows upgrades with Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness).

## Configure clients

Upgrade Readiness, like all Windows Analytics solutions, relies on Windows telemetry data. In order for Upgrade Readiness to receive sufficient telemetry data, the following pre-requisites must be satisfied:

- All clients must be configured with a **commercial ID key**. 
- Windows 10 clients must have telemetry configured to report at least basic level telemetry.
-  Clients running earlier versions on Windows must have specific KBs Installed as described in [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs). They must also have telemetry enabled in **Client Settings**.

Commercial ID key and Windows telemetry can be configured in **Client Settings**. To learn more, see [Use Windows Analytics with Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>If you encounter issues with Upgrade Readiness not receiving telemetry data from devices in your environment as expected then some of these issues may be addressed by using the [Upgrade Readiness deployment script](/windows/deployment/upgrade/upgrade-readiness-deployment-script). However, in most environments deploying the correct KBs, configuring commercial ID key and telemetry in **Client Settings** should be sufficient.

## Connect Configuration Manager to Upgrade Readiness

Beginning with Current Branch version 1706, the [Azure services wizard](../../../servers/deploy/configure/azure-services-wizard.md) is used to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, an Azure AD app registration of type *Web app / API* must be created in the [Azure portal](https://portal.azure.com). To read more about how to create an app registration, see [Register your application with your Azure Active Directory tenant](/azure/active-directory/active-directory-app-registration). In the **Azure portal**, you will also need to give your newly registered web app *contributor* permissions on the resource group that contains the OMS workspace that hosts your Upgrade Readiness data. The **Azure services wizard** will use this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

>[!IMPORTANT]
>*Contributor* permissions must be granted to the app itself as opposed to an Azure AD user identity. This is because it is the registered app and not an Azure AD user that accesses the data on behalf of your Configuration Manager infrastructure. To do this, you will have to search for the name of the app registration in the **Add users** blade when assigning the permission. This the same process that must be followed when [providing Configuration Manager with permissions to OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) for connections to [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.

### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services for use with Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

On the *Configuration* page, the following values are pre-populated if the web app import was successful and the correct permissions are assigned in the **Azure portal**. 
-  Azure subscriptions
-  Azure resource group
-  Windows Analytics workspace

More than one resource group or workspace will be available only if the registered Azure AD web app has *Contributor* permissions on more than one resource group or if the selected resource group contains more than one OMS workspace.
 
## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, choose **Monitoring** > **Overview** > **Upgrade Readiness**.
2. Review the data, which includes the upgrade readiness state and the percent of Windows devices that are reporting telemetry.
3. You can filter the dashboard to view data for devices in specific collections.
4. You can view the devices in a particular readiness state, and create a dynamic collection for those devices so that you can upgrade those devices if ready, or take action to remediate devices that are blocked from upgrading.

## Using the Upgrade Readiness Connector (version 1702 and earlier)

In Configuration Manager version 1702 or earlier, a different set of steps and requirements are necessary to create a connection to Upgrade Readiness.

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
