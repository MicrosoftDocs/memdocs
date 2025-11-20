---
title: Step 2. Create App Protection Policies for Microsoft Edge for Business
description: Step 2. Create app protection policies for Microsoft Edge for Business across Windows, Android, and iOS platforms.
ms.date: 11/05/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
zone_pivot_groups: app-protection-platforms
---

# Step 2: App Protection Policies for Microsoft Edge for Business

This guide organizes app protection policy creation by platform to help you implement the appropriate security level for each device type. The following sections provide detailed configuration steps for Windows, Android, and iOS/iPadOS platforms.

Each platform section includes instructions for creating Level 1, Level 2, and Level 3 app protection policies aligned with the Microsoft Data Protection Framework.

> [!NOTE]
> App protection policies provide data protection without requiring device enrollment, making them ideal for BYOD (Bring Your Own Device) scenarios and unmanaged devices.

## Microsoft Data Protection Framework compliance

- **Level 1** – Fully compliant with Microsoft's *Enterprise Basic Data Protection* requirements  
- **Level 2** – Fully compliant with Microsoft's *Enterprise Enhanced Data Protection* requirements  
- **Level 3** – Fully compliant with Microsoft's *Enterprise High Data Protection* requirements  
- **Web content transfer** – All policies include *Restrict web content transfer with other apps* set to Microsoft Edge

> [!IMPORTANT]
> Framework alignment:  
> These configurations align with Microsoft's Data Protection Framework and are mapped to NIST, DISA STIG, and CISA controls as defined in the [Secure Your Corporate Data in Intune with Microsoft Edge for Business](mamedge-overview.md) guide.

This guide references industry frameworks (NIST, DISA STIG, and CISA) as inputs. Applying these settings alone does not make your organization compliant with any specific standard. Perform your own compliance assessments against the official requirements.

::: zone pivot="windows"

## App protection policies for Windows

App protection policies for Windows provide secure and compliant access to work resources on personal computers by using Data Loss Prevention (DLP) controls.

Prerequisites:

- Windows
- Company Portal installed
- Appropriate Intune license (APP support)
- Microsoft Edge sign-in with Microsoft Entra ID account

### Level 1 – Enterprise basic data protection for Windows

Level 1 configuration provides the minimum data protection for a Windows device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Windows**.  
3. On the **Basics** tab, enter:  
   - **Name:** Edge Windows APP Level 1 Basic
   - **Description:** Basic data protection for Microsoft Edge with fundamental controls
4. Select **Next**.  
5. On the **Apps** tab, choose **+ Select apps** > **Microsoft Edge** > **Select**.  
6. Select **Next**.  
7. On the **Data protection** tab, configure:  

| Setting | Value |
|--------|-------|
| [Receive data from](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | All destinations |
| [Send org data to](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | All sources |
| [Allow cut, copy, and paste for](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | Any destination and any source |
| [Printing org data](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#functionality) | Allow |

8. Select **Next**.  
9. On the **Health checks** tab, configure:  

| Setting | Value |
|--------|-------|
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 90 days / Wipe data |
| [Max allowed device threat level](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | Low / Block access |

10. Select **Next**.  
11. On the **Assignments** tab, assign the policy to **SEB-Level1-Users**.  
12. Select **Next**, review the configuration, and then choose **Create**.

### Level 2 – Enterprise enhanced data protection for Windows

Level 2 configuration includes more controls for enhanced data protection.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Windows**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enterprise enhanced data protection – Windows  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on Windows devices.
4. Select **Next**.  
5. On the **Apps** tab, choose **+ Select apps** > **Microsoft Edge** > **Select**.  
6. Select **Next**.  
7. On the **Data protection** tab, configure:  

| Setting | Value |
|--------|-------|
| [Send org data to](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No destinations |
| [Receive data from](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No sources |
| [Allow cut, copy, and paste for](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No destination or source |
| [Printing org data](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#functionality) | Allow |

8. Select **Next**.  
9. On the **Health checks** tab, configure:

| Setting | Value |
|--------|--------|
| [Disabled account](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | Block access |
| [Min OS version](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 10.0.22621.2506 / Block access |
| [Max allowed device threat level](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | Medium / Block access |
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 30 days / Wipe data |

10. Select **Next**.  
11. On the **Assignments** tab, assign the policy to **SEB-Level2-Users**.  
12. Select **Next**, review the configuration, and then choose **Create**.

### Level 3 – Enterprise high data protection for Windows

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Windows**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – Enterprise high data protection – Windows  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on Windows devices.
4. Select **Next**.  
5. On the **Apps** tab, choose **+ Select apps** > **Microsoft Edge** > **Select**.  
6. Select **Next**.  
7. On the **Data protection** tab, configure:  

| Setting | Value |
|--------|-------|
| [ReceiveDataFromOtherApps](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No sources |
| [SendOrgDataToOtherApps](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No destinations |
| [RestrictCutCopyPasteIn](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#data-transfer) | No destination or source |
| [PrintBlocked](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#functionality) | Block |

8. Select **Next**.  
9. On the **Health checks** tab, configure:  

| Setting | Value |
|--------|--------|
| [Disabled account](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | Block access |
| [Min OS version](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 10.0.22621.2506 / Block access |
| [Max allowed device threat level](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | Medium / Block access |
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 1440 minutes / Block access |
| [Offline grace period](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy-settings-windows#conditional-launch) | 30 days / Wipe data |

10. Select **Next**.  
11. On the **Assignments** tab, assign the policy to **SEB-Level3-Users**.  
12. Select **Next**, review the configuration, and then choose **Create**.

#### Framework Compliance Summary for Windows

| Microsoft Framework Requirement | Level 1 | Level 2 | Level 3 |
|--------------------------------|----------|----------|----------|
| Data transfer restrictions | All destinations/sources | No destinations/sources | No destinations/sources |
| Copy/paste controls | Any destination/source | No destination/source | No destination/source |
| Screen capture | Allow | Block | Block |
| Encryption | Not required | Required | Required |
| Offline grace period | 10,080 minutes / 90 days | 1,440 minutes / 30 days | 1,440 minutes / 30 days |
| OS version requirements | Not required | Min required | Min + Max required |
| Device threat level | Low | Medium | Secured |
| Print restrictions | Allow | Block | Block |

::: zone-end

::: zone pivot="ios-ipados"

## App protection policies for iOS/iPadOS

App protection policies for iOS and iPadOS provide data protection for Microsoft Edge for Business on mobile devices without requiring device enrollment.

Prerequisites:

- iOS/iPadOS 15 or later  
- Microsoft Edge for iOS installed  
- Company Portal installed (or Mobile Application Management [MAM] managed)  
- User signed in with a corporate Entra ID account  

### Level 1 – Enterprise basic data protection for iOS/iPadOS

Level 1 configuration provides the minimum data protection for an iOS/iPadOS device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **iOS/iPadOS**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Enterprise basic data protection – iOS/iPadOS  
   - **Description:** Provides Level 1 basic data protection for Microsoft Edge for Business on iOS and iPadOS devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Back up org data to iTunes and iCloud:** Allow  
   - **Send org data to other apps:** All apps  
   - **Receive data from other apps:** All apps  
   - **Restrict cut, copy, and paste between apps:** Any app  
   - **Third-party keyboards:** Allow  
   - **Encrypt org data:** Require
   - **Print org data:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
   - **Org data notifications:** Allow
   - **Genmoji:** Allow  
   - **Screen capture:** Allow  
   - **Writing tools:** Allow  
8. Select **Next**.  
9. On the **Access requirements** tab, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Allow  
   - **Select minimum PIN length:** 4  
   - **Touch ID instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of inactivity):** 1440
   - **Face ID instead of PIN for access:** Allow
   - **PIN reset after number of days:** No  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after (minutes of inactivity):** 30  
10. On the **Conditional launch** tab, configure:
   - **Max PIN attempts:** 5, Reset PIN
   - **Offline grace period:** 10,080 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken / rooted devices:** Block access
11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level1-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.  

### Level 2 – Enterprise enhanced data protection for iOS/iPadOS

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **iOS/iPadOS**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enterprise enhanced data protection – iOS/iPadOS  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on iOS and iPadOS devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Back up org data to iTunes and iCloud:** Block  
   - **Send org data to other apps:** Policy-managed apps  
   - **Select apps to exempt:** Default list (skype; app-settings; calshow; itms; itmss; itms-apps; itms-appss; itms-services)
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint Online, Photo Library  
   - **Transfer telecommunication data to:** Any dialer app  
   - **Transfer messaging data to:** Any messaging app  
   - **Restrict cut, copy, and paste between apps:** Policy managed apps with paste in  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
   - **Org data notifications:** Block org data  
   - **Genmoji:** Block  
   - **Screen capture:** Block  
   - **Writing tools:** Block  
   - **Sync policy managed app data with native contacts app:** Block
8. Select **Next**.  
9. On the **Access requirements** tab, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Allow  
   - **Select minimum PIN length:** 4  
   - **Touch ID instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of inactivity):** 1440
   - **Face ID instead of PIN for access:** Allow
   - **PIN reset after number of days:** No  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after (minutes of inactivity):** 30  
10. On the **Conditional launch** tab, configure:
   - **Disabled account:** Block access  
   - **Min OS version:** 14.8, Block access  
   - **Min patch version:** 2024-10-01, Block access
   - **Offline grace period:** 30 days, Wipe data  
   - **Min app version:** Latest, Warn
11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level2-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.

### Level 3 – Enterprise high data protection for iOS/iPadOS

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **iOS/iPadOS**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – Enterprise high data protection – iOS/iPadOS  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on iOS and iPadOS devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Transfer telecommunication data to:** A specific dialer app  
   - **Dialer app URL scheme:** replace_with_dialer_app_url_scheme  
   - **Transfer messaging data to:** A specific messaging app  
   - **Messaging app URL scheme:** replace_with_messaging_app_url_scheme  
   - **Receive data from other apps:** Policy-managed apps  
   - **Open data into org documents:** Block
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library
   - **Third-party keyboards:** Block  
   - **Print org data:** Block
8. Select **Next**.  
9. On the **Access requirements** tab, configure:
   - **Simple PIN:** Block
   - **Select minimum PIN length:** 6
   - **PIN reset after number of days:** Yes
   - **Number of days:** 365
10. On the **Conditional launch** tab, configure:  
   - **Jailbroken / rooted devices:** Wipe data  
   - **Max allowed threat level:** Secured, Block access  
   - **Min OS version:** 14.8, Block access
   - **Max OS version:** 26.0.1, Block access
   - **Offline grace period:** 30 days, Block access
11. Add the additional recommended controls:
   - **Access Requirements:**
       - **PIN reset after number of days:** Yes (365 days)  
       - **Work or school account credentials for access:** Require  
       - **Override Touch ID with PIN after timeout:** Require  
       - **Timeout (minutes of inactivity):** 30  
   - **Conditional Launch:**  
       - **Min SDK version:** 21.1.0, Block access  
12. Select **Next**.  
13. On the **Assignments** tab, assign the policy to **SEB-Level3-Users**.  
14. Select **Next**, review the configuration, and then choose **Create**.

#### Framework Compliance Summary for iOS/iPadOS  

| Microsoft Framework Requirement | Level 1 | Level 2 | Level 3 |
|-------------------------------------|-------------|-------------|-------------|
| Data transfer restrictions | All apps | Policy-managed apps | Policy-managed apps |
| Receive data from other apps | All apps | Policy-managed apps | Policy-managed apps |
| Copy/paste controls | Any app | Policy-managed apps with paste in | Policy-managed apps with paste in |
| Encryption of org data | Required | Required | Required |
| Print org data | Allow | Allow | Block |
| Screen capture | Allow | Block | Block |
| Third-party keyboards | Allow | Block | Block |
| Web content transfer | Microsoft Edge | Microsoft Edge | Microsoft Edge |
| Offline grace period | 10,080 minutes / Block access<br>90 days / Wipe data | 10,080 minutes / Block access<br>30 days / Wipe data | 10,080 minutes / Block access<br>30 days / Block access |
| Max PIN attempts | 5 / Reset PIN | 5 / Reset PIN | 5 / Reset PIN |
| PIN length requirement | 4-digit | 4-digit | 6-digit |
| Simple PIN allowed | Yes | Yes | No |
| Override biometrics with PIN | Required | Required | Required |
| Work/school credentials required | Not required | Not required | Required |
| Device threat level enforcement | Low | Medium | Secured |
| Jailbroken/rooted devices | Block access | Block access | Wipe data |
| Minimum OS version | N/A | 14.8 | 14.8 |
| Maximum OS version | N/A | N/A | 26.0.1 |
| App version requirement | N/A | Latest / Warn | Latest / Warn |

::: zone-end

::: zone pivot="android"

## App protection policies for Android

App protection policies for Android provide data protection for Microsoft Edge for Business on mobile devices without requiring device enrollment.

> [!IMPORTANT]
> Framework alignment:  
> These configurations align with Microsoft's Data Protection Framework and are mapped to NIST, DISA STIG, and CISA controls as defined in the [Secure Your Corporate Data in Intune with Microsoft Edge for Business](mamedge-overview.md) guide.
>
> This guide references industry frameworks (NIST, DISA STIG, CISA) as inputs. Applying these settings does not by itself make your organization compliant with any specific standard; perform your own compliance assessments against official requirements.

Prerequisites:

- Android 8.0 or later  
- Microsoft Edge for Android installed  
- Company Portal or Mobile Application Management (MAM) managed  
- User Microsoft Entra ID account

### Level 1 – Enterprise basic data protection for Android

Level 1 configuration provides the minimum data protection for an Android device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Android**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Enterprise basic data protection – Android  
   - **Description:** Provides Level 1 basic data protection for Microsoft Edge for Business on Android devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Back up org data to Android backup services:** Allow  
   - **Send org data to other apps:** All apps  
   - **Receive data from other apps:** All apps  
   - **Restrict cut, copy, and paste between apps:** Any app
   - **Screen capture and Google Assistant:** Allow
   - **Approved keyboards:** Not required  
   - **Encrypt org data:** Require  
   - **Encrypt org data on enrolled devices:** Require  
   - **Sync policy managed app data with native apps or add-ins:** Allow  
   - **Print org data:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
   - **Org data notifications:** Allow  
8. Select **Next**.  
9. On the **Access requirements** tab, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Allow  
   - **Select minimum PIN length:** 4  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of inactivity):** 1,440  
   - **Class 3 biometrics (Android 9.0+):** Not required  
   - **Override biometrics with PIN after biometric updates:** Not required  
   - **PIN reset after number of days:** No  
   - **Select number of previous PIN values to maintain:** 0  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after (minutes of inactivity):** 30  
10. On the **Conditional launch** tab, configure:
   - **Max PIN attempts:** 5, Reset PIN
   - **Offline grace period:** 10,080 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken / rooted devices:** Block access
   - **Play Integrity verdict:** Basic integrity and certified devices, Block access  
   - **Require threat scan on apps:** Block access  
   - **Require device lock:** Low, Warn
11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level1-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.  

### Level 2 – Enterprise enhanced data protection for Android

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Android**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enterprise enhanced data protection – Android  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on Android devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Back up org data to Android backup services:** Block  
   - **Send org data to other apps:** Policy-managed apps  
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint Online, Photo Library  
   - **Receive data from other apps:** Policy-managed apps  
   - **Transfer telecommunication data to:** Any dialer app  
   - **Restrict cut, copy, and paste between apps:** Policy-managed apps with paste in  
   - **Screen capture and Google Assistant:** Block  
   - **Org data notifications:** Block org data  
8. Select **Next**.  
9. On the **Conditional launch** tab, configure:
   - **Offline grace period:** 30 days, Wipe data  
   - **Disabled account:** Block access  
   - **Min OS version:** 9.0, Block access  
   - **Min patch version:** 2024-11-01, Block access  
   - **Play Integrity verdict:** Basic integrity and device integrity, Block access  
   - **Require device lock:** Medium, Block access  
   - **Samsung Knox device attestation:** Block access
11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level2-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.

### Level 3 – Enterprise high data protection for Android

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Managed apps** > **Protection** > **Create** > **Android**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – Enterprise high data protection – Android  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on Android devices.  
4. Select **Next**.  
5. On the **Apps** tab, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.
   - Choose **Microsoft Edge**, then **Select**.
6. Select **Next**.
7. On the **Data protection** tab, configure:  
   - **Transfer telecommunication data to:** Any policy-managed dialer app  
   - **Receive data from other apps:** Policy-managed apps  
   - **Open data into org documents:** Block  
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library  
   - **Approved keyboards:** Require  
   - **Select keyboards to approve:** Microsoft SwiftKey Keyboard, Samsung Keyboard, Gboard – the Google Keyboard
   - **Print org data:** Block
8. Select **Next**.  
9. On the **Access requirements** tab, configure:  
   - **Simple PIN:** Block
   - **Select minimum PIN length:** 6
   - **PIN reset after number of days:** Yes
   - **Number of days:** 365
   - **Class 3 biometrics (Android 9.0+):** Require
   - **Override biometrics with PIN after biometric updates:** Require
10. On the **Conditional launch** tab, configure:
   - **Offline grace period:** 30 days, Block access  
   - **Jailbroken / rooted devices:** Wipe data  
   - **Max allowed threat level:** Secured, Block access  
   - **Max OS version:** 16.0, Block access  
   - **Require device lock:** High, Block access  
   - **Samsung Knox device attestation:** Wipe data
11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level3-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.

#### Framework Compliance Summary for Android  

| Microsoft Framework Requirement | Level 1 | Level 2 | Level 3 |
|---------------------------------|---------|---------|---------|
| Data transfer restrictions | All apps | Policy-managed apps | Policy-managed apps |
| Receive data from other apps | All apps | Policy-managed apps | Policy-managed apps |
| Copy/paste controls | Any app | Policy-managed apps with paste in | Policy-managed apps with paste in |
| Encryption of org data | Required | Required | Required |
| Print org data | Allow | Allow | Block |
| Screen capture | Allow | Block | Block |
| Approved keyboards | Not required | Not required | Required (Microsoft SwiftKey, Samsung Keyboard, Gboard) |
| Web content transfer | Microsoft Edge | Microsoft Edge | Microsoft Edge |
| Offline grace period | 10,080 minutes / Block access <br>90 days / Wipe data | 10,080 minutes / Block access <br>30 days / Wipe data | 10,080 minutes / Block access <br>30 days / Block access |
| Max PIN attempts | 5 / Reset PIN | 5 / Reset PIN | 5 / Reset PIN |
| PIN length requirement | 4-digit | 4-digit | 6-digit |
| Simple PIN allowed | Yes | Yes | No |
| Biometric instead of PIN | Allow | Allow | Block |
| Override biometrics with PIN after timeout | Required | Required | Required |
| Work or school credentials required | Not required | Not required | Required |
| Device lock complexity | Low | Low | High |
| Device threat level / Play Integrity verdict | Basic integrity | Basic + Device integrity | Secured |
| Jailbroken / rooted devices | Block access | Block access | Wipe data |
| Minimum OS version | 8.0 | 9.0 | 9.0 |
| Maximum OS version | N/A | N/A | 16.0 |
| Minimum patch version | N/A | 2024-10-01 | 2024-10-01 |
| Samsung Knox device attestation | N/A | Block access on supported devices | Wipe data (on supported devices) |
| Class 3 biometrics (Android 9.0 +) | Not required | Not required | Required |

::: zone-end

#### Validation

[!INCLUDE [App protection policy validation](includes/app-protection-policy-validation.md)]

## Related resources

For specific recommendations per level, see [Data protection framework using app protection policies](../apps/app-protection-framework.md).

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-03.png" alt-text="Step 3 to integrate Mobile Threat Defense with Microsoft Edge for Business.":::](mamedge-3-scc.md)

Continue with [Step 3](mamedge-3-scc.md) to integrate Mobile Threat Defense with Microsoft Edge for Business.
