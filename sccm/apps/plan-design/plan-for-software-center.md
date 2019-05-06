---
title: Plan for Software Center
titleSuffix: Configuration Manager
description: Decide how you want to configure and brand Software Center for users to interact with Configuration Manager.
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Plan for Software Center

*Applies to: System Center Configuration Manager (Current Branch)*

Users change settings, browse for applications, and install applications from Software Center. When you install the Configuration Manager client on a Windows device, it automatically installs Software Center as well. The new Software Center has a modern look. Apps that would have appeared only in the Silverlight-dependent Application Catalog (user-available apps) now appear in Software Center under the **Applications** tab.

For more information on the other features of Software Center, see the [Software Center user guide](/sccm/core/understand/software-center).  


## <a name="bkmk_userex"></a> Configure Software Center  

Review the following improvements to Software Center:

### Starting in version 1802

- The client setting **Use new Software Center** in the **Computer Agent** group is enabled by default. The previous version of Software Center is no longer supported. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Users can browse and install user-available applications on Azure Active Directory (Azure AD)-joined devices. For more information, see [Deploy user-available applications on Azure AD-joined devices](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

### Starting in version 1806

- Specify the visibility of the application catalog website link on the **Installation Status** tab of Software Center. For more information, see [Software Center](/sccm/core/clients/deploy/about-client-settings#software-center) client settings.  

- Application catalog roles are no longer required to display user-available applications in Software Center. This change helps you reduce the server infrastructure required to deliver applications to users. Software Center now relies upon the management point to obtain this information, which helps larger environments scale better by assigning them to [boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > If you're currently using the application catalog, and update Configuration Manager to version 1806, it continues to work. The application catalog website point and web service point roles are no longer *required*, but still *supported*. The **Silverlight user experience** for the application catalog *website point* is no longer supported. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
    >
    > Start planning to remove the application catalog roles from your infrastructure in the future. Take advantage of the Software Center improvements to use the management point, and simplify your Configuration Manager environment.  

Use the following table to help understand the requirements for Software Center depending upon the specific version of Configuration Manager:

| Device type | Site version | Infrastructure |
|-----------------|--------------|----------------|
| Azure AD-joined device<br>(or "cloud domain-joined") | 1802 or 1806 | Management point for all app deployments |
| [Hybrid Azure AD-joined](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) device on the internet | 1802 or 1806 | Cloud management gateway and management point for all app deployments |
| On-premises Active Directory domain-joined device | 1802 | Application catalog required for user-available apps through Software Center |
| On-premises Active Directory domain-joined device | 1806 | Management point for all app deployments |

> [!Important]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.


## <a name="bkmk_impact"></a> Replace toast notifications with dialog window

<!--3555947-->
Sometimes users don't see the Windows toast notification about a restart or required deployment. Then they don't see the experience to snooze the reminder. This behavior can lead to a poor user experience when the client reaches a deadline.

Starting in version 1902, when [software changes are required](#software-changes-are-required) or deployments [need a restart](#restart-required), you have the option of using a more intrusive dialog window.

### Software changes are required

When you [deploy an application](/sccm/apps/deploy-use/deploy-applications) as required with a deadline in the future, on the **User Experience** page of the Deploy Software Wizard, select the following user notification options:

- **Display in Software Center and show all notifications**
- **When software changes are required, show a dialog window to the user instead of a toast notification**

Configuring this deployment setting changes the user experience for this scenario.

From the following toast notification:

![Toast notification that Software changes are required](media/3555947-required-toast.png)  

To the following dialog window:

![Dialog window for Required software changes](media/3555947-required-dialog.png)


### Restart required

In the [Computer Restart](/sccm/core/clients/deploy/about-client-settings#computer-restart) group of client settings, enable the following option: **When a deployment requires a restart, show a dialog window to the user instead of a toast notification**.  

Configuring this client setting changes the user experience for all required deployments that require a restart of the following types:

- [Application](/sccm/apps/deploy-use/deploy-applications)
- [Task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Software update](/sccm/sum/deploy-use/deploy-software-updates)

From the following toast notification:

![Toast notification that Restart required](media/3555947-restart-toast.png)  

To the following dialog window:

![Dialog window to Restart your computer](media/3555947-restart-dialog.png)


## Branding Software Center

Change the appearance of Software Center to meet your organization's branding requirements. This configuration helps users trust Software Center.

Configuration Manager applies custom branding for Software Center according to the following priorities:  

- If you haven't installed the application catalog (recommended):  

    1. **Software Center** client settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. **Organization name** client setting in **Computer Agent** group. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- If you've installed the application catalog:  

    1. **Software Center** client settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. If you connect a Microsoft Intune subscription to Configuration Manager, then Software Center displays the *organization name*, *color*, and *company logo* that you specify in the Intune subscription properties. For more information, see [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. The *organization name* and *color* that you specify in the Application Catalog website point properties. For more information, see [Configuration options for Application Catalog website point](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. **Organization name** client setting in **Computer Agent** group. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

### Configure Software Center branding

<!-- 1351224 -->
Customize the appearance of Software Center by adding your organization's branding elements and specifying the visibility of tabs.

For more information, see the following articles:

- [Software Center](/sccm/core/clients/deploy/about-client-settings#software-center) group of client settings  
- [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings)  


## See also

- [Software Center user guide](/sccm/core/understand/software-center)
- [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management)
