---
title: Plan for Software Center
titleSuffix: Configuration Manager
description: Decide how you want to configure and brand Software Center for users to interact with Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Plan for Software Center

*Applies to: Configuration Manager (current branch)*

Users change settings, browse for applications, and install applications from Software Center. When you install the Configuration Manager client on a Windows device, it automatically installs Software Center as well.

## <a name="bkmk_userex"></a> Configure Software Center

> [!IMPORTANT]
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

Use client settings to configure the appearance and behaviors of Software Center. For more information, see [Software Center client settings](../../core/clients/deploy/about-client-settings.md#software-center). The following list is a summary of some of the configurations:

- Change the branding of Software Center to include your organization's name, colors, and logo. For more information, see [Brand Software Center](#brand-software-center).

- Configure which default tabs are visible, and add up to five custom tabs to Software Center.<!--4063773-->

- Starting in version 2006, you can configure co-managed devices to use the Company Portal for both Intune and Configuration Manager apps. For more information, see [Use the Company Portal app on co-managed devices](../../comanage/company-portal.md).<!--CMADO-3601237,INADO-4297660-->

You can allow users to set in Software Center if they regularly use the computer for work. This option configures an affinity between the user and device, which can affect some deployments. For more information, see [Link users and devices with user device affinity](../deploy-use/link-users-and-devices-with-user-device-affinity.md#let-users-create-their-own-device-affinities).

Be aware of the following settings for features that are no longer supported:

- The client setting **Use new Software Center** in the **Computer Agent** group is enabled by default. The previous version of Software Center is no longer supported.

- The client setting **Hide application catalog link in Software Center** in the **Software Center Customizations** is enabled by default. This link would appear on the **Installation Status** tab of Software Center. The application catalog is no longer supported.

For more information, see [Removed and deprecated features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### Software Center and user-available applications

When you deploy an app with the purpose **Available** to a user collection, users can see these available applications in Software Center. This behavior provides a self-service capability for users to easily install approved software, without requiring assistance from IT staff.

Software Center gets application deployment information in policy from the management point. It uses the same management point from the assigned primary site as the Configuration Manager client. In a large environment, you can scale client communication to management points by assigning them to [boundary groups](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->

Users can browse and install user-available applications on Azure Active Directory (Azure AD)-joined devices. Starting in version 2006, they can get user-available apps on internet-based, domain-joined devices. For more information, see [Prerequisites to deploy user-available applications](prerequisites-deploy-user-available-apps.md).

## Brand Software Center

Change the appearance of Software Center to meet your organization's branding requirements. This configuration helps users trust Software Center.

### Configure Software Center branding

<!-- 1351224 -->
Customize the appearance of Software Center by adding your organization's branding elements:

- **Organization name**: Software Center displays this name in the top banner
- **Color scheme**: The primary color for the banner and other elements
- **Foreground color**: By default, when you select an item, the font color is white. Starting in version 2103, you can change this color for better visibility with certain primary colors, and better accessibility.<!--8655575-->
- **Logo**: A JPG, PNG, or BMP of 400 x 100 pixels, with a maximum size of 750 KB

The following image shows a example of Software Center that's customized with all four branding settings:

:::image type="content" source="media/8655575-software-center-foreground-color.png" alt-text="Software Center with customized branding":::

For more information, see the following articles:

- [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) group of client settings
- [How to configure client settings](../../core/clients/deploy/configure-client-settings.md)

### Branding priorities

Configuration Manager applies the organization name for Software Center according to the following priorities:

1. **Software Center Customization** client setting for **Company Name**. For more information, see [About client settings: Software Center](../../core/clients/deploy/about-client-settings.md#software-center).

2. **Computer Agent** client setting for **Organization name**. For more information, see [About client settings: Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

## Next steps

- [Software Center user guide](../../core/understand/software-center.md)

- [Plan for and configure application management](plan-for-and-configure-application-management.md)

- [Use the Company Portal app on co-managed devices](../../comanage/company-portal.md)

> [!NOTE]
> This article used to include more sections, which have moved to the following articles:
>
> - [User notifications for required deployments](user-notifications.md)
