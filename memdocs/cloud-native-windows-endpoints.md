---
# required metadata

title: Get started with cloud native Windows endpoints 
titleSuffix: Microsoft Endpoint Manager
description: Use this guide to set up secure cloud native Windows endpoints that are Azure AD joined, enrolled in Intune, and then deploy at scale with Autopilot.
keywords:
author: scottbreenmsft; rogersoMS
ms.author: brenduns
manager: dougeby
ms.date: 07/27/2021
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Get started with cloud native Windows endpoints with Microsoft Endpoint Manager

Increasing demand for remote work is accelerating adoption of Zero Trust security models, enabled by cloud- powered solutions. The shifting of device management to the cloud provides a better end-user experience and simplifies IT operations, while reducing reliance on on-premises infrastructure. This guide walks you through the steps to create a cloud native Windows endpoint configuration for your organization.

> [!TIP]
> If you’re looking for a Microsoft recommended, standardized solution to build on top of, you might be interested in *Windows in cloud configuration* which can easily be configured using a [Guided Scenario](/mem/intune/fundamentals/guided-scenarios-overview) in Intune. See [Windows Cloud Configuration for Endpoint Management - Microsoft 365](/microsoft-365/windows/cloud-configuration). This guide (for *cloud native Windows endpoints*) differs from the *Windows in cloud configuration for Endpoint Management* solution by guiding you through the configuration and highlighting areas you might want to customise.

## Overview

### What is a cloud native Windows endpoint?

A cloud native Windows endpoint is joined to [Azure AD](/azure/active-directory/devices/concept-azure-ad-join) (AADJ) and managed by a Mobile Device Management (MDM) solution. Unlike traditional domain join or [Hybrid Azure AD joined](/azure/active-directory/devices/concept-azure-ad-join-hybrid) endpoints, it has no dependencies on on-premises Active Directory. This document focuses on Microsoft Endpoint Manager (MEM) as the MDM solution. Cloud native endpoints can be easily deployed by using [Autopilot](/mem/autopilot/windows-autopilot) to transform the pre-installed Windows operating system.

### Benefits of cloud native Windows endpoints

- **Best for remote work** - Cloud native endpoints don't require line of sight to an on-premises domain controller, which significantly simplifies the user experience especially in remote work situations. For instance, a VPN connection isn't required for the initial device sign-in or to update the local device password after a network password change.
- **Reduced reliance on on-premises infrastructure** - Reducing your reliance on on-premises infrastructure will allow devices to be provisioned on any network, simplifying requirements and management.

- **Unified cross platform endpoint management** - You can step away from complex Group Policy management and modernize endpoint management by using a unified MDM solution that handles multiple platforms, like iOS, Android, macOS, and Windows all together in one place.

- **Preserve Single-Sign-On (SSO) to on-premises applications** - Cloud native endpoints don't compromise the user experience while on the corporate network. They natively provide SSO to on-premises infrastructure such as file servers, print servers, and web applications. For more information, see [SSO to on-premises resources](/azure/active-directory/devices/azuread-join-sso).

- **Personalization preservation** - Cloud native endpoints can easily take advantage of Microsoft 365 services to provide a synchronized and seamless experience across endpoints, including:
  - Windows wallpaper
  - Automatic sync of documents and desktop files to OneDrive
  - Settings for Office
  - Outlook signatures
  - Microsoft Edge settings

### How to get started

Use the five ordered phases in this guide, which build on each other to help you prepare your cloud native Windows endpoint configuration. By completing these phases in order, you'll see tangible progress along the way and to be ready to provision new devices at the end of this guide.

**Phases**:
:::image type="content" source="./media/cloud-native-windows-endpoints/phases.png" alt-text="Five phases for setting up cloud native Windows endpoints.":::

- Phase 1 – Set up your environment
- Phase 2 – Build your first cloud native Windows endpoint
- Phase 3 – Secure your cloud native Windows endpoint
- Phase 4 – Apply your custom settings and applications
- Phase 5 – Deploy at scale with Autopilot

At the end of this guide, you’ll have a cloud native Windows endpoint ready to start testing in your environment.
Before you get started, you might want to check out the Azure AD join planning guide at [How to plan your Azure Active Directory join implementation](/azure/active-directory/devices/azureadjoin-plan).

## Phase 1 – Set up your environment

:::image type="content" source="./media/cloud-native-windows-endpoints/phase-1.png" alt-text="Phase 1.":::

Before you build your first cloud native Windows endpoint, there are some key requirements and configuration that need to be checked. This phase will walk you through checking the requirements, configuring [Autopilot](/mem/autopilot/windows-autopilot), and creating some settings and applications.

### Step 1 - Network requirements

Your cloud native Windows endpoint will need access to several internet services. Start your testing on an open network or use your corporate network after providing access to all the endpoints that are listed at [Windows Autopilot networking requirements](/mem/autopilot/networking-requirements).

If your wireless network requires certificates, you can start with an Ethernet connection during testing while you determine the best approach for wireless connections for device provisioning.

### Step 2 - Enrollment and Licensing

Before you can join Azure AD and enroll in Intune, there are a few things you need to check. You could create a new Azure AD group (for example, with the name **Intune MDM Users**), and add specific test user accounts and target each of the following configurations at that group to limit who can enroll devices while you set up your configuration. To create an Azure AD group, see [Create a basic group and add members](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).

- **Enrollment restrictions** - Enrollment restrictions allow you to control what types of devices can enroll into management with Intune. For this guide to be successful, make sure *Windows (MDM)* enrollment is allowed, which is the default configuration.

  For information on configuring Enrollment Restrictions, see [Set enrollment restrictions in Microsoft Intune](/mem/intune/enrollment/enrollment-restrictions-set).

- **Azure AD Device MDM settings** - When you join a Windows device to Azure AD, Azure AD can be configured to tell your devices to automatically enroll with an MDM. This configuration is required for Autopilot to work seamlessly.

  To check your Azure AD Device MDM settings are enabled properly, see [Quickstart - Set up automatic enrollment in Intune](/mem/intune/enrollment/quickstart-setup-auto-enrollment).

- **Licensing** - Users enrolling Windows devices from the Out Of Box Experience (OOBE) into Intune will require two key capabilities.

  Users will require the following licenses:
  - A **Microsoft Intune** or **Microsoft Intune for Education** license
  - A license like one of the following options that allows for automatic MDM enrollment:
    - **Azure AD Premium P1**
    - **Microsoft Intune for Education**

  To assign licenses, see [Assign Microsoft Intune licenses](/mem/intune/fundamentals/licenses-assign).

  > [!NOTE]
  > Both types of licenses are typically included with licensing bundles like Microsoft 365 E3 (or A3) and above. View comparisons of M365 licensing [here](/microsoft-365/compare-microsoft-365-enterprise-plans).

### Step 3 - Import your test device

To test the Cloud Native Windows endpoint, we need to start by getting a virtual machine or physical device ready for testing. The following steps will gather the device details and upload them into the Autopilot service for use later in this document.

> [!NOTE]
> While the following steps provide a way to import a device for testing, Partners and OEMs can import devices into Autopilot on your behalf as part of purchasing. There is more information about Autopilot in [Phase 5](#phase-5-deploy-at-scale-with-autopilot).

1. Install Windows (preferably 20H2 or later) in a virtual machine or reset physical device so that it’s waiting at the OOBE setup screen. For a virtual machine, you can optionally create a checkpoint.

2. Complete the necessary steps to connect to the Internet.

3. Open a command prompt by using the keyboard combination **Shift+F10**.

4. Verify that you have internet access by pinging bing.com:
   - `ping bing.com`

5. Switch into PowerShell by running the command:
   - `powershell.exe`

6. Download the *Get-WindowsAutoPilotInfo* script by running the commands:
   - `Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process`
   - `Install-Script Get-WindowsAutoPilotInfo`

7. When prompted, enter **Y** to accept.

8. Type the command:
   - `Get-WindowsAutoPilotInfo.ps1 -GroupTag CloudNative -Online`

   > [!NOTE]
   > Group Tags allow you to create dynamic Azure AD groups based on a subset of devices. Group Tags can be set when importing devices or changed later in the Microsoft Endpoint Manager admin console. We'll use the Group Tag *CloudNative* in Step 4. You can set the tag name to something different for your testing.

9. Log into the credential prompt with your Intune Administrator account.

10. Leave the computer at the out of box experience until [Phase 2](#phase-2-build-your-first-cloud-native-windows-endpoint).

### Step 4 - Create Azure AD dynamic group for the device

To limit the configurations from this guide to the test devices that you import to Autopilot, create a dynamic Azure AD group that automatically includes the devices that import to Autopilot and have the Group Tag *CloudNative*. You can then target all your configurations and applications at this group.

1. Open the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).

2. Select **Groups**.

3. Select **New Group** and enter the following details:
   1. Group type: **Security**
   2. Group Name: **Autopilot Cloud Native Windows Endpoints**
   3. Membership type: **Dynamic Device**

4. Select **Add dynamic query**.

5. In the **Rule Syntax** section, select **Edit.**

6. Paste the following text:
   - `(device. devicePhysicalIds -any (_ -eq "[OrderID]:CloudNative"))`

7. Select **OK**, then **Save**, then **Create**.

> [!TIP]
> Dynamic groups take a few minutes to populate after changes occur. In large organizations, it [can take much longer](/azure/active-directory/enterprise-users/groups-troubleshooting#troubleshooting-dynamic-memberships-for-groups). After creating a new group, wait a few minutes before you check to confirm the device is now a member of the group.

### Step 5 - Configure the Enrollment Status Page

The enrollment status page (ESP) is the mechanism an IT pro uses to control the end-user experience during endpoint provisioning. See [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status). To limit the scope of the enrollment status page, you can create a new profile and target the **Autopilot Cloud Native Windows Endpoints** group created in the previous step, *Create Azure AD dynamic group for the device*.

- For the purposes of testing, we recommend the following settings, but feel free to adjust them as required:
  - **Show app and profile configuration progress** - Yes
  - **Only show page to devices provisioned by out-of-box experience (OOBE)** – Yes (*default*)

### Step 6 - Create and assign Autopilot profile

Now we can create an Autopilot profile and assign it to our test device. This profile tells your device to join Azure AD and what settings to apply during OOBE.

1. Open the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).

2. Select **Devices** > **Enroll devices** > **Deployment profiles** (under **Windows Autopilot Deployment Program**).

3. Select **Create profile** > **Windows PC**.

4. Enter the name **Autopilot Cloud Native Windows Endpoint**, and then select **Next**.

5. Review and leave the default settings and select **Next**.

6. Leave the scope tags and select **Next**.

7. Assign the profile to the Azure AD group you created called **Autopilot Cloud Native Windows Endpoint**, select **Next**, and then select **Create**.

### Step 7 - Sync Autopilot devices

The Autopilot service will synchronize several times a day. You can also trigger a sync immediately so that your device is ready to test. To synchronize immediately:

1. Open the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).

2. Select **Devices** > **Enroll devices** > **Devices**.

3. Select **Sync**.

The sync takes several minutes and will continue in the background. When the sync is complete, the profile status for the imported device displays **Assigned**.

### Step 8 - Configure settings for an optimal Microsoft 365 experience

We’ve selected a few settings to configure that will demonstrate an optimal Microsoft 365 end-user experience on your Windows cloud native device. These settings are configured using a device configuration settings catalog profile. For more information, see [Create a policy using the settings catalog in Microsoft Intune](/mem/intune/configuration/settings-catalog). Once you’ve created the profile and added your settings, assign the profile to the **Autopilot Cloud Native Windows Endpoints** group created previously.

- **Microsoft Outlook**
  To improve the first run experience for Microsoft Outlook, the following setting will automatically configure a profile when Outlook is opened for the first time.

  - Microsoft Outlook 2016\Account Settings\Exchange (User setting)
    - Automatically configure only the first profile based on Active Directory primary SMTP address - **Enabled**

- **Microsoft Edge**
  To improve the first run experience for Microsoft Edge, the following settings will configure Edge to sync the user’s settings and skip the first run experience.

  - Microsoft Edge
    - Hide the first-run experience and splash screen - **Enabled**
    - Force synchronization of browser data and do not show the sync consent prompt - **Enabled**

- **Microsoft OneDrive**
  To improve the first sign-in experience, the following settings will configure Microsoft OneDrive to automatically sign in and redirect Desktop, Pictures, and Documents to OneDrive.

  - OneDrive
    - Silently sign in users to the OneDrive sync app with their Windows credentials - **Enabled**
    - Silently move Windows known folders to OneDrive – **Enabled**
Navigate to aad.portal.azure.com to get the Azure AD tenant ID and paste it in.

The following screenshot shows an example of a settings catalog profile with each of the suggested settings configured:
:::image type="content" source="./media/cloud-native-windows-endpoints/settings-catalog-example.png" alt-text="Example of a settings catalog profile.":::

### Step 9 - Create and assign some applications

Your cloud native endpoint will need some applications. To get started, we recommend configuring the following applications and targeting them at the **Autopilot Cloud Native Windows Endpoints** group created previously.

- **Microsoft 365 Apps** (formerly Office 365 ProPlus)
  Microsoft 365 Apps such as Word, Excel, and Outlook can easily be deployed to devices using the built-in *Microsoft 365 apps for Windows* app profile in Intune. 

  - Select **configuration designer** for the settings format, as opposed to XML.
  - Select **Current Channel** for the update channel.
  - Ensure that you de-select (uncheck) the option for **OneDrive (Groove) ** as this is the legacy OneDrive. Because OneDrive is included with Windows, it is not mandatory to install it. Remove additional applications you don't want installed by unchecking them.

  To deploy Microsoft 365 Apps, see [Add Microsoft 365 apps to Windows devices using Microsoft Intune](/mem/intune/apps/apps-add-office365)

- **Microsoft Edge**
  Microsoft Edge is the new browser from Microsoft built on Chromium open source. Edge can easily be deployed to devices using the built-in app profile in Intune. 

  To deploy Microsoft Edge, see [Add Microsoft Edge for Windows to Microsoft Intune](/mem/intune/apps/apps-windows-edge).

  > [!NOTE]
  > Microsoft Edge is included on devices that run:
  >
  > - Windows 10 20H2 or later.
  > - Windows 10 1803 or later, with the May 2021 or later cumulative monthly security update.

  For additional details, see [New Microsoft Edge to replace Microsoft Edge Legacy with April’s Windows 10 Update Tuesday release](https://techcommunity.microsoft.com/t5/microsoft-365-blog/new-microsoft-edge-to-replace-microsoft-edge-legacy-with-april-s/ba-p/2114224)

- **Company Portal**
  Deploying the Intune *Company Portal* app to all devices as a required application is strongly recommended. Company Portal is the self-service hub for users – allowing them to install applications from multiple sources (Intune, Microsoft Store, Configuration Manager), sync their device with Intune, check compliance status, etc. 

  To setup a relationship between Intune and the Microsoft Store for Business (MSfB) and acquire the Company Portal app as an offline app which can be sync’d to Intune and targeted at devices, see [Add and assign the Windows Company Portal app for Autopilot provisioned devices](/mem/intune/apps/store-apps-company-portal-autopilot).

- **Microsoft Store App** (Whiteboard)
  While Intune can deploy a wide variety of apps, to keep things simple for this guide, we will deploy a store app (Microsoft Whiteboard).  Follow the steps from [Get the offline Company Portal app from the store](/mem/intune/apps/store-apps-company-portal-autopilot#get-the-offline-company-portal-app-from-the-store) but select *Microsoft Whiteboard* as the app , set it *Online*, and deploy the app as *available* instead of as a required app. The app should later appear within Company Portal for manual installation by the user.


