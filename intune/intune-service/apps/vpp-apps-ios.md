---
title: Manage Apple Volume-Purchased Apps
description: Learn how to sync apps you bought in volume through Apple Business Manager with Microsoft Intune. Then manage and track these apps on iOS/iPadOS and macOS devices.
ms.date: 10/27/2025
ms.topic: how-to
ms.reviewer: bryanke
ms.collection:
- M365-identity-device-management
- iOS/iPadOS
- macOS
- highpri
---

# How to Manage iOS and macOS Apps Purchased Through Apple Business Manager with Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple lets you purchase multiple licenses for an app that you want to use in your organization on iOS/iPadOS and macOS devices using [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/). You can then synchronize your volume purchase information with Intune and track your volume-purchased app use. Purchasing app licenses helps you efficiently manage apps within your company and retain ownership and control of purchased apps.

Microsoft Intune helps you manage apps purchased through this program by:

- Synchronizing location tokens you download from Apple Business Manager.
- Tracking how many licenses are available and used for purchased apps.
- Installing apps up to the number of licenses you own.

You can synchronize, manage, and assign books you purchased from Apple Business Manager with Intune to iOS/iPadOS devices. For more information, see [How to manage iOS/iPadOS eBooks you purchased through a volume-purchase program](vpp-ebooks-ios.md).

## What are location tokens?
Location tokens are volume purchase licenses that were commonly known as Volume Purchase Program (VPP) tokens. These location tokens are used to assign and manage licenses purchased using Apple Business Manager. Content Managers can purchase and associate licenses with location tokens they have permissions to in Apple Business Manager. These location tokens are then downloaded from Apple Business Manager and uploaded in Microsoft Intune. Microsoft Intune supports uploading multiple location tokens per tenant. Each token is valid for one year.

> [!NOTE]
> The Apple Volume Purchase Program (VPP) is integrated into Apple Business Manager. Apple Business Manager is a portal for admins to deploy Apple devices and acquire content in volume. Content could include apps, books, and custom apps. Location tokens are used to assign and manage licenses purchased using Apple Business Manager. VPP is now called legacy VPP tokens.

## How are purchased apps licensed?
Purchased apps can be assigned to groups using two types of licenses that Apple offers for iOS/iPadOS and macOS devices.

> [!NOTE]
> Device-licensed VPP apps must be installed and updated through the MDM channel only. Users can't go the store directly to manually install or update a VPP app.

| Action | Device Licensing | User Licensing |
|------- | -----------------| ---------------|
| App   Store sign-in | Not required. | Each end user must use a unique Apple Account when prompted   to sign in to App Store. |
| Device   configuration blocking access to App Store | Apps can be installed and updated using Company Portal. | The invitation to join Apple Business Manager requires access to the App Store. If you set a policy to disable the App Store, user licensing for VPP apps doesn't work.|
| Automatic   app update | As configured by the Intune admin in Apple Business Manager token settings.<p>If the assignment type is available for enrolled devices, available app updates can also be installed from the Company Portal by selecting the **Update** action on the app details page. | As configured by the Intune admin in Apple Business Manager token settings.<p>If the assignment type is available for enrolled devices, available app updates can also be installed from the Company Portal by selecting the **Update** action on the app details page. |
| User   Enrollment | Not supported. | Supported using Managed Apple Accounts. |
| Books | Not supported. | Supported. |
| Licenses   used | One license per device. The license is associated with the   device. | One license for up to five devices using the same personal   Apple Account. The license is associated with the user.<p>An end user   associated with a personal Apple Account and a Managed Apple Account in Intune consumes   two app licenses. |
| License   migration | Apps can migrate silently from user to device licenses only when using **Required** assignment type. | Apps can't migrate from device to user licenses for any assignment type. |

> [!NOTE]
> Company Portal doesn't show device-licensed apps on User Enrollment devices because only user-licensed apps can be installed on User Enrollment devices.
>
> When you create a new assignment for an Apple Volume Purchase Program (VPP) app, the default license type is now "device." Existing assignments remain unchanged.

## What app types are supported?
You can purchase and distribute public and private apps using Apple Business Manager.
- **Store apps:** Content Managers can use Apple Business Manager to acquire both free and paid apps from the App Store.
- **Custom Apps:** Content Managers can also use Apple Business Manager to acquire Custom Apps made available privately to your organization. These apps are tailored to your organization's specific needs by developers with whom you work directly. Learn more about [how to distribute Custom Apps](https://developer.apple.com/business/custom-apps/).

## Prerequisites
- [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/) account for your organization.
- App licenses assigned to one or more location tokens.
- Location tokens.

> [!IMPORTANT]
> - A location token can only be used with one device management solution at a time. Before you start to use purchased apps with Intune, revoke and remove any existing location tokens used with other mobile device management (MDM) vendor.
> - A location token is only supported for use on one Intune tenant at a time. Don't reuse the same token for multiple Intune tenants.
> - Intune synchronizes the location tokens with Apple once a day, by default. You can initiate a manual sync at any time from Intune.
> - Import of the same token to another device management solution after you import the location token to Intune can result in the loss of license assignment and user records.

## Migrate from Volume Purchase Program (VPP) to Apps and Books
If your organization isn't migrated to Apple Business Manager or Apple School Manager, review [Apple's guidance on migrating to Apps and Books](https://support.apple.com/HT208257) before proceeding to manage purchased apps in Intune.

> [!IMPORTANT]
> - Only migrate one VPP purchaser per location. If each purchaser migrates to a unique location, all licenses—assigned and unassigned—move to Apps and Books.
> - Don't delete the existing legacy VPP token in Intune or apps and assignments associated with existing legacy VPP token in Intune. These actions require all app assignments to be recreated in Intune.

Migrate existing purchased VPP content and tokens to Apps and Books in Apple Business Manager or Apple School Manager as follows:

1. Invite VPP purchasers to join your organization and direct each user to select a unique location.
2. Ensure that all VPP purchasers within your organization completed step 1 before proceeding.
3. Verify that all purchased apps and licenses migrated to Apps and Books in Apple Business Manager or Apple School Manager.
4. Download the new location token by going to **Apple Business (or School) Manager** > **Your Name** > **Preferences** > **Payments and Billing** > **Apps and Books** > **Content Tokens** > **Download**.
5. Update the location token in Microsoft Intune admin center by going to **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens** and manually upload the token.

## Upload an Apple VPP or Apple Business Manager location token

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**.
3. On the list of VPP tokens pane, select **Create**. The **Create VPP token** process is displayed. There are four pages used when creating a VPP token. The first is **Basics**.
4. On the **Basics** page, specify the following information:
   - **Token Name** - An administrative field for setting the token name.
   - **Apple Account** - Enter the Managed Apple Account of the account associated with the uploaded token.
   - **VPP token file** - If you haven't already, sign up for Apple Business Manager or Apple School Manager. After you sign up, download the Apple Business Manager location token (Apple VPP token) for your account and select it here.
5. Select **Next** to display the **Settings** page.
6. On the **Settings** page, specify the following information:
   - **Take control of token from another MDM** - Setting this option to **yes** allows the token to be reassigned to Intune from another MDM solution.
   - **Country/Region** - Select the VPP country/region store. Intune synchronizes VPP apps for all locales from the specified VPP country/region store.

        > [!WARNING]
        > Changing the country/region updates the app metadata and App Store URL during the next sync with the Apple service for apps created with this token. The app doesn't update if it doesn't exist in the new country/region store.

   - **Type of VPP account** - Choose from **Business** or **Education**.
   - **Automatic app updates** - Choose from **Yes** or **No** to enable automatic updates. When enabled, Intune detects the VPP app updates inside the app store and automatically pushes them to the device when the device checks in.

        > [!NOTE]
        > Apple VPP apps update automatically for both **Required** and **Available** install intents. However, in both cases, you might temporarily see the error message **"0x87D13B9F / The VPP app is installed but there is a newer version available"** if the device checks in but the update doesn't install. At next check-in, Intune sends the install command to the device as long as the user is still included in the **Required** or **Available** assignment. However, if the user or device is removed from the assignments, Intune no longer pushes updates to that particular app, even if Intune originally installed the app.
        >
        > When you update a VPP app, it can take up to 24 hours for the device to receive the update. The device must be unlocked and available to install the update.
        >
        > If you changed app install intents of Apple VPP apps from **Required** to **Available**, the apps that are already installed stop updating automatically. Manually installing the app after you change the intent to Available resumes automatic updates.

    - **I grant Microsoft permission to send both user and device information to Apple.** - You must select **I agree** to proceed. To review what data Microsoft sends to Apple, see [Data Intune sends to Apple](../protect/data-intune-sends-to-apple.md).
7. Select **Next** to display the **Scope tags** page.
8. Select **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
9. Select **Next** to display the **Review + create** page. Review the values and settings you entered for the VPP token.
10. When you're done, select **Create**. The token is displayed in the list of tokens pane.

## Synchronize a VPP token

You can synchronize the app names, metadata, and license information for your purchased apps in Intune by choosing **Sync** for a selected token.

## Assign a volume-purchased app

1. In Intune, select **Apps** > **All Apps**.
2. On the list of apps pane, choose the app you want to assign, and then choose **Properties**. Select **Edit** next to **Assignments**.
3. On the **Assignments** tab, choose whether the app is **Required** or **Available for enrolled devices**.
4. Choose **Add group** under the assignment type you selected, then on the **Select groups** pane choose the Microsoft Entra user or device groups to which you want to assign the app.

    > [!NOTE]
    > When you create a new assignment for an Apple Volume Purchase Program (VPP) app, the default license type is "device." Existing assignments remain unchanged.
5. Once you're done, choose **Save**.

> [!NOTE]
> The Available deployment intent isn't supported for device groups. Only user groups support this intent. The list of apps displayed is associated with a token. If an app is associated with multiple VPP tokens, the same app appears multiple times—once for each token.
>
> Apps assigned as Available don't become managed on the device until the user initiates an install of the application. Once an app assigned as Available is installed, or the user attempts to install the application, Intune ensures that the app is licensed.

Intune (or any other MDM for that matter) doesn't actually install VPP apps. Instead, Intune connects to your VPP account and tells Apple which app licenses to assign to which devices. From there, all the actual installation is handled between Apple and the device.

> [!NOTE]
> The **VPP token name** column, available in the Apps workload, allows you to quickly determine the token and app association. This column is available in the **All apps** list (**Apps** > **All apps**) and the app selection pane for **App configuration policies** (**Apps** > **App configuration policies**).

## End-User Prompts for VPP

The end-user receives prompts for VPP app installation in many scenarios. The following table explains each condition:

| # | Scenario                                | Invite to Apple VPP program                              | App install prompt | Prompt for Apple Account |
|---|--------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------------------|
| 1 | Bring your own device (BYOD) – user licensed (not User Enrollment device)                             | Y                                                                                               | Y                                           | Y                                 |
| 2 | Corp – user licensed (not supervised device)     | Y                                                                                               | Y                                           | Y                                 |
| 3 | Corp – user licensed (supervised device)         | Y                                                                                               | N                                           | Y                                 |
| 4 | BYOD – device licensed                           | N                                                                                               | Y                                           | N                                 |
| 5 | CORP – device licensed (not supervised device)                           | N                                                                                               | Y                                           | N                                 |
| 6 | CORP – device licensed (supervised device)                           | N                                                                                               | N                                           | N                                 |
| 7 | Kiosk mode (supervised device) – device licensed | N                                                                                               | N                                           | N                                 |
| 8 | Kiosk mode (supervised device) – user licensed   | --- | ---                                          | ---                                |

> [!Note]
> User and device licensed apps running on supervised devices (scenarios 3 and 6 in the previous table) will still prompt for updates if the app is in use or is running in the background. Accepting the prompt to install the app may not result in the app installing. In order to update the app, you must:  close the app, initiate a sync, and leave the device unlocked while the app updates.

> [!Note]
> It is not recommended to assign VPP apps to Kiosk-mode devices using user licensing.

> [!Note]
> You cannot update any app while the device is locked in Single App Mode. You need to exit Single App Mode long enough to update apps as needed. During that time, you should restrict the visible apps as much as possible, except for Settings and other apps that cannot be blocked.

## Revoking app licenses

You can revoke all associated iOS/iPadOS or macOS volume-purchase program (VPP) app licenses based on a given device, user, or app. But there are some differences between iOS/iPadOS and macOS platforms.

| Action | iOS/iPadOS | macOS |
|------- | ---------- | ----- |
| Remove app assignment | Removing an app assignment is a prerequisite to revoking an app license. When you remove an app assignment for a user, Intune doesn't reclaim the user or device license until you change the assignment to **Uninstall**. If the app assignment is removed while the app is installed and never assigned as **Uninstall**, it remains installed, but is no longer offered for installation to the user or device. | Removing an app assignment is a prerequisite to revoking an app license. When you remove an app assignment for a user, Intune doesn't reclaim the user or device license until you change the assignment to **Uninstall**. If the app assignment is removed while the app is installed and never assigned as **Uninstall**, it remains installed, but is no longer offered for installation to the user or device. |
| Revoke app license | After removing the app assignment, you can reclaim an app license from the user or device using the **Revoke license** action. You must change the assignment to **Uninstall** to remove the app from the device and revoke the app license. | After removing the app assignment, you can reclaim an app license from the user or device using the **Revoke license** action. The macOS app with revoked license remains usable on the device, but can't be updated until a license is reassigned to the user or device. According to Apple, such apps are removed after a 30-day grace period. You must change the assignment to **Uninstall** to remove the app from the device and revoke the app license. |

>[!NOTE]
> - Intune reclaims app licenses when an employee leaves the company and is no longer part of the Microsoft Entra groups.
> - When assigning a purchased app with **Uninstall** intent, Intune both reclaims the license and uninstalls the app.
> - App licenses aren't reclaimed when a device is removed from Intune management.
> - Intune revokes app licenses when the user is deleted from Microsoft Entra ID.
> - Intune only supports revoking VPP app licenses that meet the following conditions:
>   - The VPP app license is assigned from Intune
>   - The VPP app license is for devices managed by Intune
>   - The VPP app license relates to devices where the Intune device record still exists for the device

## Deleting VPP apps

To delete a VPP app from Intune, follow the steps:
> - Remove all app assignment groups.
> - Revoke all app licenses and insure in ABM (Apple Business Manager) no user or device still holds a license.
> - Transfer all app licenses to a different VPP token.
> - Delete the VPP app from Intune console. This step is not necessary with V2 VPP token as subsequent sync would remove the app.

## Deleting VPP tokens
<!-- 820879 -->
You can delete an Apple Volume Purchasing Program (VPP) token using the console. You might need to do this action if you have duplicate instances of a VPP token. Deleting a token also deletes any associated apps and assignment. Deleting a token revokes associated app licenses but doesn't uninstall the apps.

>[!NOTE]
>Intune can't revoke app licenses after a token is deleted.

<!-- 820870 -->
To revoke the license of all VPP apps for a given VPP token, you must first revoke all app licenses associated with the token, then delete the token.

## Renewing VPP tokens or Apple Business Manager location token

Renew an Apple Business Manager location token (Apple VPP token) by downloading the token again from [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/), and then updating the existing token in Intune.

To renew an Apple Business Manager location token (Apple VPP token), use the following steps:

1. Navigate to [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
2. Within Apple Business (or School) Manager, select **Preferences** > **Payments and Billing** > **Apps and Books** > **Content  Tokens**.
3. Select **Download** and save the token file.
4. Update the token in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**.
5. Select the VPP token you're renewing, select **Edit** on the Basics category, upload the new token on this page, and then save your changes.

> [!NOTE]
> The expiration date listed in Intune might take some time to reflect the new certificate expiration date after renew. Confirm renew was successful by refreshing the page until the expiration date updates.
>
> Renew the existing Apple VPP token or location token if there are any changes to the Managed Apple ID account used to set up the token (Domain change, Password changed or expired, Account is disabled). Tokens show "invalid" status in Intune in any of those scenarios or if the token expired.

## Configure updates for VPP apps

You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. The **Prevent automatic updates** setting is dependent on the token-level **Allow automatic updates** setting. To use the **Prevent automatic updates**, the **Allow automatic updates** setting must be set to **Yes**. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments**.

## Deleting a VPP app
You can delete purchased apps that don't have any available or used licenses associated with them. Deleting the apps might be necessary to clean up apps that are no longer assigned.

To delete a VPP app, use the following steps:
1. Create a new location in [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
2. Revoke all licenses for the app that use the associated location token. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All Apps** > *select the app to delete* > **App licenses** > **Revoke licenses**.
3. In Apple Business Manager or Apple School Manager, transfer all licenses for the app from the original location to the new location.
4. Sync the location token in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
5. Delete the app in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All Apps** > *right-click on the app to delete* > **Delete**.

Deleting a VPP app causes the following results:
- The associated app assignments are removed.
- An error is displayed if the VPP app assigned licenses when attempting to delete.

> [!NOTE]
> Purchased books associated with a VPP token aren't deleted.

## Assigning custom role permissions for VPP

Access to Apple Business Manager location token and apps (Apple VPP tokens and VPP apps) can be controlled independently using permissions assigned to custom administrator roles in Intune.

* To allow an Intune custom role to manage Apple Business Manager location tokens, in Microsoft Intune admin center, select **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**, assign permissions for **Managed apps**.
* To allow an Intune custom role to manage apps purchased using iOS/iPadOS VPP tokens under **Apps** > **All Apps**, assign permissions for **Mobile apps**.

> [!NOTE]
> You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission.

## Additional information

Apple provides direct assistance to create and renew VPP tokens. For more information, see [Distribute content to your users with the Volume Purchase Program (VPP)](https://go.microsoft.com/fwlink/?linkid=2014661) as part of Apple's documentation.

If a token’s status is **Duplicate**, you uploaded multiple tokens with the same **Token Location.** Remove the duplicate token to begin syncing the token again. You can still assign and revoke licenses for tokens that are marked as duplicate. However, licenses for new apps and books purchased might not be reflected once a token is marked as duplicate.

## Frequently asked questions

### How many tokens can I upload?

You can upload up to 3,000 tokens in Intune.

### How long does the portal take to update the license count once an app is installed or removed from the device?

The license should be updated within a few hours after installing or uninstalling an app. If the end user removes the app from the device, the license is still assigned to that user or device.

### Is it possible to oversubscribe an app and, if so, in what circumstance?

Yes. The Intune admin can oversubscribe an app. For example, if the admin purchases 100 licenses for app XYZ, and then targets the app to a group with 500 members in it. The first 100 members (users or devices) get the license assigned to them. The rest of the members fail on license assignment.

> [!NOTE]
> When the number of used licenses is greater than or equal to 50% of total available licenses for a specific app, an alert appears under the Enrollment alerts tab. The alert disappears when the number of used licenses is less than 50% of total available licenses for the app.

## Next steps

See [How to monitor apps](apps-monitor.md) for information to help you monitor app assignments.

See [How to troubleshoot apps](/troubleshoot/mem/intune/troubleshoot-app-install) for information on troubleshooting app-related issues.
