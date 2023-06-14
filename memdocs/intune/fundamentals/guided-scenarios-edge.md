---
title: Guided scenario - Deploy Microsoft Edge for Mobile 
titleSuffix: Microsoft Intune
description: Learn about the guided scenario to deploy Microsoft Edge for Mobile from the Microsoft 365 Device Management portal.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/06/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- intune-scenario
---

# Guided scenario - Deploy Microsoft Edge for Mobile

By following this [guided scenario](guided-scenarios-overview.md), you can assign the Microsoft Edge app to your users on iOS/iPadOS or Android devices at your organization. Assigning this app will allow your users to seamlessly browse content using their corporate devices.

Microsoft Edge lets users cut through the clutter of the web with built-in features that help them consolidate, arrange and manage work content. Users of iOS/iPadOS and Android devices who sign in with their corporate Azure AD accounts in the Microsoft Edge application will find their browser pre-loaded with workplace **Favorites** and website filters you define.

> [!NOTE]
> If you have blocked users from enrolling either iOS/iPadOS or Android devices, this scenario will not enable enrollment, and the users will need to install Edge for themselves.
The following Microsoft Edge enterprise features that are enabled by Intune policies include:

- **Dual-Identity** - Users can add both a work account, as well as a personal account, for browsing. There is complete separation between the two identities, which is similar to the architecture and experience in Microsoft 365 and Outlook. Intune admins will be able to set the desired policies for a protected browsing experience within the work account.
- **Intune app protection policy integration** - Admins can now target app protection policies to Microsoft Edge, including the control of cut, copy, and paste, preventing screen captures, and ensuring that user-selected links open only in other managed apps.
- **Azure Application Proxy integration** - Admins can control access to SaaS apps and web apps, helping ensure browser-based apps only run in the secure Microsoft Edge browser, whether end users connect from the corporate network or connect from the Internet.
- **Managed Favorites and Home Page shortcuts** - For ease of access, admins can set URLs to appear under favorites when end users are in their corporate context. Admins can set a homepage shortcut, which will show as the primary shortcut when the corporate user opens a new page or a new tab in Microsoft Edge.

## Prerequisites

- [Set the MDM authority to Intune](mdm-authority-set.md#set-mdm-authority-to-intune) - The mobile device management (MDM) authority setting determines how you manage your devices. As an IT admin, you must set an MDM authority before users can enroll devices for management.
- Intune Admin permissions needed:
  - Managed apps read, create, delete, and assign permissions
  - Mobile apps read, create, and assign permissions
  - Policy sets read, create, and assign permissions
  - Organization read, update permission

## Step 1 - Introduction

By following the **Deploy Microsoft Edge for Mobile** guided scenario, you will set up a basic deployment of Microsoft Edge for a selected group of iOS/iPadOS and Android users. This deployment will implement **Dual-Identity** and **Managed Favorites and Home Page shortcuts**. In addition, devices enrolled by the selected users will automatically have the Microsoft Edge app installed by Intune. This automatic installation will occur on all user-driven enrollment types, which include:

- iOS/iPadOS enrollment through the Company Portal app
- iOS/iPadOS user-affinity enrollment through Apple Business Manager
- Legacy Android enrollment through the Company Portal App

This guided scenario will automatically enable **MyApps** to appear in the Microsoft Edge favorites and configure the browser with the same branding you have set for the Intune Company Portal app.

### What you will need to continue

We'll ask you about the workplace favorites your users need, and the filters you require for web browsing. Make sure you complete the following tasks before you continue:

- Add users to Azure AD groups. For more information, see [Create a basic group and add members using Azure Active Directory](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).
- Enroll iOS/iPadOS or Android devices in Intune. For more information, see [Device enrollment](/mem/intune/fundamentals/deployment-guide-enrollment).
- Gather a list of workplace favorites to add in Microsoft Edge.
- Gather a list of website filters to enforce in Microsoft Edge.

## Step 2 - Basics

In this step, you must enter a name and description for your new Microsoft Edge policies. These policies can be referenced later if you need to change the assignments and configurations. The guided scenario will add and assign both an Microsoft Edge iOS/iPadOS app for your iOS/iPadOS devices and an Microsoft Edge Android app for your Android devices. Also, this step will create configuration policies for these apps.

## Step 3 - Configuration

In this step, the guided scenario will configure Microsoft Edge to show all the other apps assigned to users through Intune and share the same branding as the Microsoft Intune Company Portal app. You may further configure Microsoft Edge with a **Home page shortcut URL**, a list of **Managed Bookmarks**, and a list of **Blocked URLs**. The **Home page shortcut URL** will appear to users as the first icon beneath the search bar when they open a new tab in Microsoft Edge on their device. The **Managed Bookmarks** are a list of favorite URLs for your users to have available when using Microsoft Edge in their work context. The **Blocked URLs** specify the sites that are blocked for your users while in their work context. All other sites will be allowed.

## Step 4 - Assignments

In this step, you can choose the user groups that you want to include to have Microsoft Edge mobile configured for work. Microsoft Edge will also be installed on all iOS/iPadOS and Android devices enrolled by these users.

## Step 5 - Review + create

The final step allows you to review a summary of the settings you configured. Once you have reviewed your choices click **Create** to complete the guided scenario. 

> [!NOTE]
> Edge may take up to 12 hours to receive configuration. For more information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

> [!IMPORTANT]
> Once the guided scenario is complete it will display a summary. You can modify the resources listed in the summary later, however the table displaying these resources will not be saved.

## Next steps

- Enhance the security of using Microsoft Edge by setting up Intune app protection policy integration. For more information, see [Create Intune app protection policies](../apps/manage-microsoft-edge.md#create-intune-app-protection-policies).
- If you have intranet sites to include, explore protecting access with Azure Application Proxy integration. For more information, see [Manage proxy configuration](../apps/manage-microsoft-edge.md#manage-proxy-configuration).