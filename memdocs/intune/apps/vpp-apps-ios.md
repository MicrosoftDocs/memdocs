---
# required metadata

title: Manage Apple volume-purchased apps
titleSuffix: Microsoft Intune
description: Learn about how you can sync apps you purchased in volume from iOS/iPadOS and macOS App Store into Microsoft Intune and then manage and track their usage.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 51d45ce2-d81b-4584-8bc4-568c8c62653d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- iOS/iPadOS
- macOS
- highpri
---

# How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple lets you purchase multiple licenses for an app that you want to use in your organization on iOS/iPadOS and macOS devices using [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/). You can then synchronize your volume purchase information with Intune and track your volume-purchased app use. Purchasing app licenses helps you efficiently manage apps within your company and retain ownership and control of purchased apps. 

Microsoft Intune helps you manage apps purchased through this program by:

- Synchronizing location tokens you download from Apple Business Manager.
- Tracking how many licenses are available and have been used for purchased apps.
- Helping you install apps up to the number of licenses you own.

Additionally, you can synchronize, manage, and assign books you purchased from Apple Business Manager with Intune to iOS/iPadOS devices. For more information, see [How to manage iOS/iPadOS eBooks you purchased through a volume-purchase program](vpp-ebooks-ios.md).

## What are location tokens?
Location tokens are volume purchase licenses that were commonly known as Volume Purchase Program (VPP) tokens. These location tokens are used to assign and manage licenses purchased using Apple Business Manager. Content Managers can purchase and associate licenses with location tokens they have permissions to in Apple Business Manager. These location tokens are then downloaded from Apple Business Manager and uploaded in Microsoft Intune. Microsoft Intune supports uploading multiple location tokens per tenant. Each token is valid for one year.

> [!NOTE]
> The Apple Volume Purchase Program (VPP) has been integrated into Apple Business Manager. Apple Business Manager is a portal for admins to deploy Apple devices and acquire content in volume. Content may include apps, books, and custom apps. Location tokens are used to assign and manage licenses purchased using Apple Business Manager. VPP is now called legacy VPP tokens.

## How are purchased apps licensed?
Purchased apps can be assigned to groups using two types of licenses that Apple offers for iOS/iPadOS and macOS devices.

> [!NOTE]
> Device-licensed VPP apps must be installed and updated through the MDM channel only. Users cannot go the store directly to manually install or update a VPP app.

| Action | Device Licensing | User Licensing |
|------- | -----------------| ---------------|
| App   Store sign-in | Not required. | Each end user must use a unique Apple ID when prompted   to sign in to App Store. |
| Device   configuration blocking access to App Store | Apps can be installed and updated using Company Portal. | The invitation to join Apple Business Manager requires access to App   Store. If you have set a policy to disable App Store, user licensing for VPP   apps will not work. |
| Automatic   app update | As configured by the Intune admin in Apple Business Manager token settings.<p>If the assignment type is available for enrolled devices, available app updates can also be installed from the Company Portal by selecting the **Update** action on the app details page. | As configured by the Intune admin in Apple Business Manager token settings.<p>If the assignment type is available for enrolled devices, available app updates can also be installed from the Company Portal by selecting the **Update** action on the app details page. |
| User   Enrollment | Not supported. | Supported using Managed Apple IDs. |
| Books | Not supported. | Supported. |
| Licenses   used | 1 license per device. The license is associated with the   device. | 1 license for up to 5 devices using the same personal   Apple ID. The license is associated with the user.<p>An end user   associated with a personal Apple ID and a Managed Apple ID in Intune consumes   2 app licenses. |
| License   migration | Apps can migrate silently from user to device licenses only when using **Required** assignment type. | Apps cannot migrate from device to user licenses for any assignment type. |

> [!NOTE]  
> Company Portal does not show device-licensed apps on User Enrollment devices because only user-licensed apps can be installed on User Enrollment devices.
>
> When you create a new assignment for a Apple Volume Purchase Program (VPP) app, the default license type is now "device". Existing assignments remain unchanged. 

## What app types are supported?
You can purchase and distribute public as well as private apps using Apple Business Manager.
- **Store apps:** Using Apple Business Manager, Content Managers can acquire both free and paid apps that are available in the App Store.
- **Custom Apps:** Using Apple Business Manager, Content Managers can also acquire Custom Apps made available privately to your organization. These apps are tailored to your organization's specific needs by developers with whom you work directly. Learn more about [how to distribute Custom Apps](https://developer.apple.com/business/custom-apps/).

## Prerequisites
- An [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/) account for your organization. 
- Purchased app licenses assigned to one or more location tokens. 
- Downloaded location tokens. 

> [!IMPORTANT]
> - A location token can only be used with one device management solution at a time. Before you start to use purchased apps with Intune, revoke and remove any existing location tokens used with other mobile device management (MDM) vendor. 
> - A location token is only supported for use on one Intune tenant at a time. Do not reuse the same token for multiple Intune tenants.
> - By default, Intune synchronizes the location tokens with Apple once a day. You can initiate a manual sync at any time from Intune.
> - After you have imported the location token to Intune, do not import the same token to any other device management solution. Doing so might result in the loss of license assignment and user records.

## Migrate from Volume Purchase Program (VPP) to Apps and Books
If your organization has not migrated to Apple Business Manager or Apple School Manager yet, review [Apple's guidance on migrating to Apps and Books](https://support.apple.com/HT208257) before proceeding to manage purchased apps in Intune.

> [!IMPORTANT]
> - For the best migration experience, migrate only one VPP purchaser per location. If each purchaser migrates to a unique location, all licenses — assigned and unassigned — will move to Apps and Books.
> - Do not delete the existing legacy VPP token in Intune or apps and assignments associated with existing legacy VPP token in Intune. These actions will require all app assignments to be recreated in Intune.

Migrate existing purchased VPP content and tokens to Apps and Books in Apple Business Manager or Apple School Manager as follows:

1. Invite VPP purchasers to join your organization and direct each user to select a unique location. 
2. Ensure that all VPP purchasers within your organization have completed step 1 before proceeding.
3. Verify that all purchased apps and licenses have migrated to Apps and Books in Apple Business Manager or Apple School Manager.
4. Download the new location token by going to **Apple Business (or School) Manager** > **Your Name** > **Preferences** > **Payments and Billing** > **Apps and Books** > **Content Tokens** > **Download**.
5. Update the location token in Microsoft Intune admin center by going to **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens** and manually upload the token.

## Upload an Apple VPP or Apple Business Manager location token

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**.
3. On the list of VPP tokens pane, select **Create**. The **Create VPP token** process is displayed. There are four pages used when creating a VPP token. The first is **Basics**.
4. On the **Basics** page, specify the following information:
   - **Token Name** - An administrative field for setting the token name.
   - **Apple ID** - Enter the Managed Apple ID of the account associated with the uploaded token.
   - **VPP token file** - If you haven't already, sign up for Apple Business Manager or Apple School Manager. After you sign up, download the Apple Business Manager location token (Apple VPP token) for your account and select it here.
5. Click **Next** to display the **Settings** page.
6. On the **Settings** page, specify the following information:
   - **Take control of token from another MDM** - Setting this option to **yes** allows the token to be reassigned to Intune from another MDM solution.
   - **Country/Region** - Select the VPP country/region store.  Intune synchronizes VPP apps for all locales from the specified VPP country/region store.

        > [!WARNING]  
        > Changing the country/region will update the apps metadata and App Store URL on next sync with the Apple service for apps created with this token. The app will not be updated if it does not exist in the new country/region store.

   - **Type of VPP account** - Choose from **Business** or **Education**.
   - **Automatic app updates** - Choose from **Yes** or **No** to enable automatic updates. When enabled, Intune detects the VPP app updates inside the app store and automatically pushes them to the device when the device checks in.

        > [!NOTE]
        > Automatic app updates for Apple VPP apps will automatically update for both **Required** and **Available** install intents. For apps deployed with **Available** install intent, the automatic update generates a status message for the IT admin informing that a new version of the app is available. This status message is viewable by selecting the app, selecting Device Install Status, and checking the Status Details. 
        >
        > When updating a VPP app, it can take up to 24 hours for the device to receive the updated VPP app. The device must be unlocked and available to install the update successfully.

    - **I grant Microsoft permission to send both user and device information to Apple.** - You must select **I agree** to proceed. To review what data Microsoft sends to Apple, see [Data Intune sends to Apple](../protect/data-intune-sends-to-apple.md).
7. Click **Next** to display the **Scope tags** page.
8. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
9. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the VPP token.
10. When you are done, click **Create**. The token is displayed in the list of tokens pane.

## Synchronize a VPP token

You can synchronize the app names, metadata and license information for your purchased apps in Intune by choosing **Sync** for a selected token.

## Assign a volume-purchased app

1. Select **Apps** > **All apps**.
2. On the list of apps pane, choose the app you want to assign, and then choose **Properties**. Select **Edit** next to **Assignments**.
3. On the **Assignments** tab, choose whether the app will be **Required** or **Available for enrolled devices**.
4. Choose **Add group** under the assignment type you've selected, then on the **Select groups** pane choose the Azure AD user or device groups to which you want to assign the app.

    > [!NOTE]
    > When you create a new assignment for a Apple Volume Purchase Program (VPP) app, the default license type is "device". Existing assignments remain unchanged.
5. Once you are done, choose **Save**.

>[!NOTE]
>The Available deployment intent is not supported for device groups, only user groups are supported. The list of apps displayed is associated with a token. If you have an app that is associated with multiple VPP tokens, you see the same app being displayed multiple times; once for each token.
   
>[!NOTE]
>Apps assigned as Available do not become managed on the device until the user initiates an install of the application. Once an app assigned as Available has been installed, or the user has attempted to install the application, Intune will ensure that the app is licensed.
   
> [!NOTE]  
> Intune (or any other MDM for that matter) does not actually install VPP apps. Instead, Intune connects to your VPP account and tells Apple which app licenses to assign to which devices. From there, all the actual installation is handled between Apple and the device.
> 

## End-User Prompts for VPP

The end-user will receive prompts for VPP app installation in a number of scenarios. The following table explains each condition:

| # | Scenario                                | Invite to Apple VPP program                              | App install prompt | Prompt for Apple ID |
|---|--------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------------------|
| 1 | BYOD – user licensed (not User Enrollment device)                             | Y                                                                                               | Y                                           | Y                                 |
| 2 | Corp – user licensed (not supervised device)     | Y                                                                                               | Y                                           | Y                                 |
| 3 | Corp – user licensed (supervised device)         | Y                                                                                               | N                                           | Y                                 |
| 4 | BYOD – device licensed                           | N                                                                                               | Y                                           | N                                 |
| 5 | CORP – device licensed (not supervised device)                           | N                                                                                               | Y                                           | N                                 |
| 6 | CORP – device licensed (supervised device)                           | N                                                                                               | N                                           | N                                 |
| 7 | Kiosk mode (supervised device) – device licensed | N                                                                                               | N                                           | N                                 |
| 8 | Kiosk mode (supervised device) – user licensed   | --- | ---                                          | ---                                |
   
> [!Note]  
> User and device licensed apps running on supervised devices (scenarios 3 and 6 in the table above) will still prompt for updates if the app is in use or is running in the background. Accepting the prompt to install the app may not result in the app installing. In order to update the app, you must:  close the app, initiate a sync, and leave the device unlocked while the app updates. 
   
> [!Note]  
> It is not recommended to assign VPP apps to Kiosk-mode devices using user licensing.

> [!Note]  
> You cannot update any app while the device is locked in Single App Mode. You need to exit Single App Mode long enough to update apps as needed. During that time, you should restrict the visible apps as much as possible, except for Settings and other apps that cannot be blocked. 
   
## Revoking app licenses

You can revoke all associated iOS/iPadOS or macOS volume-purchase program (VPP) app licenses based on a given device, user, or app.  But there are some differences between iOS/iPadOS and macOS platforms. 

| Action | iOS/iPadOS | macOS |
|------- | ---------- | ----- |
| Remove app assignment | Removing an app assignment is a prerequisite to revoking an app license. When you remove an app assignment for a user, Intune does not reclaim the user or device license until you change the assignment to **Uninstall**. If the app assignment is removed while the app is installed and never assigned as **Uninstall**, it will remain installed, but it will no longer be offered for installation to the user or device. | Removing an app assignment is a prerequisite to revoking an app license. When you remove an app assignment for a user, Intune does not reclaim the user or device license until you change the assignment to **Uninstall**. If the app assignment is removed while the app is installed and never assigned as **Uninstall**, it will remain installed, but it will no longer be offered for installation to the user or device. |
| Revoke app license | After changing the app assignment to **Uninstall**, you can reclaim an app license from the user or device using the **Revoke license** action. You must change the assignment to **Uninstall** to remove the app from the device and revoke the app license. | After changing the app assignment to **Uninstall**, you can reclaim an app license from the user or device using the **Revoke license** action. The macOS app with revoked license remains usable on the device, but cannot be updated until a license is reassigned to the user or device. According to Apple, such apps are removed after a 30-day grace period. You must change the assignment to **Uninstall** to remove the app from the device and revoke the app license. |

>[!NOTE]
> - Intune reclaims app licenses when an employee leaves the company and is no longer part of the AAD groups.
> - When assigning a purchased app with **Uninstall** intent, Intune both reclaims the license and uninstalls the app.
> - App licenses are not reclaimed when a device is removed from Intune management. 
> - Intune will revoke app licenses when the user is deleted from Azure AD.

## Deleting VPP tokens
<!-- 820879 -->  
You can delete an Apple Volume Purchasing Program (VPP) token using the console. This may be necessary when you have duplicate instances of a VPP token. Deleting a token will also delete any associated apps and assignment. Deleting a token revokes associated app licenses but doesn't uninstall the apps.  

>[!NOTE]
>Intune cannot revoke app licenses after a token has been deleted. 

<!-- 820870 -->  
To revoke the license of all VPP apps for a given VPP token, you must first revoke all app licenses associated with the token, then delete the token.

## Renewing VPP tokens or Apple Business Manager location token

You can renew an Apple Business Manager location token (Apple VPP token) by downloading the token from [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/) again and updating the existing token in Intune. 

To renew an Apple Business Manager location token (Apple VPP token), use the following steps:

1. Navigate to [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
2. Download the existing token in **Apple Business (or School) Manager**, by selecting **Preferences** > **Payments and Billing** > **Apps and Books** > **Server Tokens**.
3. Update the token in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**.
4. Select the VPP token you are renewing, click **Edit** on the Basics category, upload the new token on this page, and then save your changes.

> [!NOTE]
> You must renew the existing Apple VPP token or location token when the user who set up the token in Apple Business Manager changes their password or the user leaves your Apple Business Manager organization. Tokens that are not renewed will show "invalid" status in Intune.

## Configure updates for VPP apps

You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. The **Prevent automatic updates** setting is dependent on the token-level **Allow automatic updates** setting. To use the **Prevent automatic updates**, the **Allow automatic updates** setting must be set to **Yes**. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments**.

## Deleting a VPP app
You can delete purchased apps that don't have any available or used licenses associated with them. This may be necessary to clean up apps that are no longer assigned.

To delete a VPP app, use the following steps:
1. Create a new location in [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/). 
2. Revoke all licenses for the app that use the associated location token. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > *select the app to delete* > **App licenses** > **Revoke licenses**.
3. In Apple Business Manager or Apple School Manager, transfer all licenses for the app from the original location to the new location. 
4. Sync the location token in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
5. Delete the app in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > *right-click on the app to delete* > **Delete**.

Deleting a VPP app will cause the following results:
- The associated app assignments will be removed. 
- If the VPP app has assigned licenses when attempting to delete, an error will be displayed to you.

> [!NOTE]
> Purchased books associated with a VPP token won't be deleted.

## Assigning custom role permissions for VPP

Access to Apple Business Manager location token and apps (Apple VPP tokens and VPP apps) can be controlled independently using permissions assigned to custom administrator roles in Intune.

* To allow an Intune custom role to manage Apple Business Manager location tokens, in Microsoft Intune admin center, select **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**, assign permissions for **Managed apps**.
* To allow an Intune custom role to manage apps purchased using iOS/iPadOS VPP tokens under **Apps** > **All apps**, assign permissions for **Mobile apps**. 

> [!NOTE]
> You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change does not apply to Intune for Education tenants who still need to assign the **Managed apps** permission.   
   
## Additional information

Apple provides direct assistance to create and renew VPP tokens. For more information, see [Distribute content to your users with the Volume Purchase Program (VPP)](https://go.microsoft.com/fwlink/?linkid=2014661) as part of Apple's documentation. 

If **Assigned to external MDM** is indicated in Intune, then you (the admin) must remove the VPP token from the 3rd party MDM before using the VPP token in Intune.

If status is **Duplicate** for a token, then multiple tokens with the same **Token Location** have been uploaded. Remove the duplicate token to begin syncing the token again. You can still assign and revoke licenses for tokens that are marked as duplicate. However, licenses for new apps and books purchased may not be reflected once a token is marked as duplicate.

## Frequently asked questions

### How many tokens can I upload?

You can upload up to 3,000 tokens in Intune.

### How long does the portal take to update the license count once an app is installed or removed from the device?

The license should be updated within a few hours after installing or uninstalling an app. Note that if the end user removes the app from the device, the license is still assigned to that user or device.

### Is it possible to oversubscribe an app and, if so, in what circumstance?

Yes. The Intune admin can oversubscribe an app. For example, if the admin purchases 100 licenses for app XYZ, and then targets the app to a group with 500 members in it. The first 100 members (users or devices) will get the license assigned to them, the rest of the members will fail on license assignment.
   
> [!NOTE]
> When the amount of used licenses is greater than or equal to 50% of total available licenses for a specific app, an alert will appear under the Enrollment alerts tab. The alert will disappear when the amount of used licenses is less than 50% of total available licenses for the app. 

## Next steps

See [How to monitor apps](apps-monitor.md) for information to help you monitor app assignments.

See [How to troubleshoot apps](/troubleshoot/mem/intune/troubleshoot-app-install) for information on troubleshooting app-related issues.
