---
# required metadata

title: Set up Symantec Endpoint Protection Mobile integration with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the Symantec Endpoint Protection Mobile solution with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 359448d9-2384-42ac-a21c-a25148c20a7b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Set up Symantec Endpoint Protection Mobile integration with Intune

Complete the following steps to integrate the Symantec Endpoint Protection Mobile (SEP Mobile) solution with Intune. You need to add SEP Mobile apps into Azure AD to have Single Sign On capabilities.

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Before you begin

### Azure AD account used to integrate Intune and SEP Mobile

- Make sure you have the Azure AD account properly configured in the [Symantec Endpoint Protection Mobile Management console](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/logging-on-to-the-console-v8025272-d23e2462.html) before starting the SEP Mobile Basic setup process.
- The Azure AD account must be a global administrator account to perform the integration.
### Network Setup

You can make sure your network is properly configured for integration with SEP Mobile setup by referring to the Symantec article [Configuring SEP Manager after installation](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/configuring-after-installation-v18374552-d23e1454.html).

### Full integration vs. Read-only

SEP Mobile supports two modes of integration with Intune:

- **Read-only integration (Basic setup):** Only inventories devices from Azure Active Directory and populates them in the Symantec Endpoint Protection Mobile Management console.
<br>
  - If the **Report the health and risk of devices to Intune**, and **Also report security incidents to Intune** boxes are not selected in the Symantec Endpoint Protection Mobile Management console, the integration is read-only and therefore will never change a device's state (compliant or noncompliant) in Intune.
<br></br>
- **Full integration:** Allows SEP Mobile to report devices on risk and security incident details to Intune, which creates a bi-directional communication between both cloud services.

### How are the SEP Mobile apps used with Azure AD and Intune?

- **iOS app:** Allows end-users to sign in to Azure AD using an iOS/iPadOS app.

- **Android app:** Allows end-users to sign in to Azure AD using an Android app.

- **Management app:** This is the SEP Mobile Azure AD multi-tenant app which enables service-to-service communication with Intune.

## To set up the read-only integration between Intune and SEP Mobile

> [!IMPORTANT]
> The SEP Mobile admin credentials must consist of an e-mail account that belongs to a valid user in the Azure Active Directory, otherwise the login will fail. SEP Mobile uses Azure Active Directory to authenticate its admin using Single Sign On (SSO).

1. Go to [Symantec Endpoint Protection Mobile Management Console](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/logging-on-to-the-console-v8025272-d23e2462.html).

2. Enter your **SEP Mobile admin credentials**, and then choose **Continue**.

3. Go to **Settings**, and under **Intune Integration**, choose **Basic Setup**.

4. Next to **iOS App**, choose **Add to Active Directory**.

    ![Image of the Symantec Endpoint Protection Mobile Management Console](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

5. When the login page opens, enter your Intune credentials, and then choose **Accept**.

    ![Image of the iOS/iPadOS app Intune login prompt](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

6. After the app is added to Azure AD, you'll see an indication that the app was added successfully.

    ![Image of the iOS/iPadOS app completion screen](./media/skycure-mtd-connector-integration/symantec-portal-basic-added.png)

7. Repeat these steps for the **SEP Mobile Android** and **Management** apps.

### Add an Azure AD Security group into SEP Mobile

You need to add an Azure AD security group that contains all devices running SEP Mobile.

- Enter and select all the security groups of devices that are running SEP Mobile, and then save the changes.

    ![Image showing user groups for SEP Mobile apps](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

SEP Mobile syncs the devices running its Mobile Threat Defense service with the Azure AD security groups.

![Image of Security group configuration on SEP Mobile management console](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.png)

## To set up the full integration between Intune and SEP Mobile

### Retrieve the Directory ID in Azure AD

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Type "Active Directory" in the search box, and then select **Azure Active Directory**.

3. Choose **Properties**.

4. Next to the **Directory ID**, choose the copy icon, and then paste it to a safe location. You'll need this identifier in a later step.

    ![Image showing Directory ID in the Azure portal](./media/skycure-mtd-connector-integration/symantec-azure-portal-directory-ID.png)

### (Optional) Create a dedicated Security Group for devices that need to run the SEP Mobile apps
1. In the [Azure portal](https://portal.azure.com), under **Manage**, choose **Users and groups**, and then choose **All groups**.

2. Choose the **Add** button. Type a group **Name**. Under **Membership type**, choose **Assigned**.

3. In the **Members** blade, select the group members, and then choose the **Select** button.

4. In the **Group** blade, choose **Create**.

### Set up the integration between Symantec Endpoint Protection Mobile and Intune

1. Go to [Symantec Endpoint Protection Mobile Management Console](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/logging-on-to-the-console-v8025272-d23e2462.html).

2. Enter your **SEP Mobile admin credentials**, then choose **Continue**.

3. Go to the **Settings** > **Integrations** > **Intune** > **EMM Integration Selection** section.

4. In the **Directory ID** box, paste the Directory ID you copied from Azure Active Directory in the previous section and save the settings.

    ![Image showing Directory ID in the SEP Mobile portal](./media/skycure-mtd-connector-integration/symantec-portal-directory-ID.png)

5. Go to the **Settings** > **Integrations** > **Intune** > **Basic Setup** section.

6. Next to **iOS App**, choose the **Add to Active Directory** button.

    ![Image showing adding the iOS/iPadOS app to Active Directory](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

7. Sign in using the Azure Active Directory credentials for the Microsoft 365 account that manages the directory.

8. Choose the **Accept** button to add the SEP Mobile iOS/iPadOS app to Azure Active Directory.

    ![Image showing the accept button](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

9. Repeat the same process for the **Android app** and the **Management App**.

10. Select all user groups that need to run the SEP Mobile apps, for example, the security group you created earlier.

    ![Image showing user groups for SEP Mobile apps](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

11. SEP Mobile syncs the devices in the selected groups and starts reporting information to Intune. You can view this data in the Full Integration section. Go to the **Settings** > **Integrations** > **Intune** > **Full Integration** section.

     ![Image showing SEP Mobile full integration completed](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.PNG)
## Next steps

[Set up SEP Mobile apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
