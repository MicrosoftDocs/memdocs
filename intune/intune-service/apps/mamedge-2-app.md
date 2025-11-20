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

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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
| [Receive data from](app-protection-policy-settings-windows.md#data-transfer) | All destinations |
| [Send org data to](app-protection-policy-settings-windows.md#data-transfer) | All sources |
| [Allow cut, copy, and paste for](app-protection-policy-settings-windows.md#data-transfer) | Any destination and any source |
| [Printing org data](app-protection-policy-settings-windows.md#functionality) | Allow |

8. Select **Next**.  
9. On the **Health checks** tab, configure:  

| Setting | Value |
|--------|-------|
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 90 days / Wipe data |
| [Max allowed device threat level](app-protection-policy-settings-windows.md#conditional-launch) | Low / Block access |

10. Select **Next**.  
11. On the **Assignments** tab, assign the policy to **SEB-Level1-Users**.  
12. Select **Next**, review the configuration, and then choose **Create**.

### Level 2 – Enterprise enhanced data protection for Windows

Level 2 configuration includes more controls for enhanced data protection.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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
| [Send org data to](app-protection-policy-settings-windows.md#data-transfer) | No destinations |
| [Receive data from](app-protection-policy-settings-windows.md#data-transfer) | No sources |
| [Allow cut, copy, and paste for](app-protection-policy-settings-windows.md#data-transfer) | No destination or source |
| [Printing org data](app-protection-policy-settings-windows.md#functionality) | Allow |

8. Select **Next**.  
9. On the **Health checks** tab, configure:

| Setting | Value |
|--------|--------|
| [Disabled account](app-protection-policy-settings-windows.md#conditional-launch) | Block access |
| [Min OS version](app-protection-policy-settings-windows.md#conditional-launch) | 10.0.22621.2506 / Block access |
| [Max allowed device threat level](app-protection-policy-settings-windows.md#conditional-launch) | Medium / Block access |
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 30 days / Wipe data |

10. Select **Next**.  
11. On the **Assignments** tab, assign the policy to **SEB-Level2-Users**.  
12. Select **Next**, review the configuration, and then choose **Create**.

### Level 3 – Enterprise high data protection for Windows

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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
| [ReceiveDataFromOtherApps](app-protection-policy-settings-windows.md#data-transfer) | No sources |
| [SendOrgDataToOtherApps](app-protection-policy-settings-windows.md#data-transfer) | No destinations |
| [RestrictCutCopyPasteIn](app-protection-policy-settings-windows.md#data-transfer) | No destination or source |
| [PrintBlocked](app-protection-policy-settings-windows.md#functionality) | Block |

8. Select **Next**.  
9. On the **Health checks** tab, configure:  

| Setting | Value |
|--------|--------|
| [Disabled account](app-protection-policy-settings-windows.md#conditional-launch) | Block access |
| [Min OS version](app-protection-policy-settings-windows.md#conditional-launch) | 10.0.22621.2506 / Block access |
| [Max allowed device threat level](app-protection-policy-settings-windows.md#conditional-launch) | Medium / Block access |
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 1440 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-windows.md#conditional-launch) | 30 days / Wipe data |

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

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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

| Setting | Value |
|--------|--------|
| [Back up org data to](app-protection-policy-settings-ios.md#data-transfer) | Allow |
| [Send org data to other apps](app-protection-policy-settings-ios.md#data-transfer) | All apps |
| [Receive data from other apps](app-protection-policy-settings-ios.md#data-transfer) | All apps |
| [Restrict cut, copy, and paste between apps](app-protection-policy-settings-ios.md#data-transfer) | Any app |
| [Third-party keyboards](app-protection-policy-settings-ios.md#data-transfer) | Allow |
| [Encrypt org data](app-protection-policy-settings-ios.md#encryption) | Require |
| [Sync policy managed app data with native contacts app](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Print org data](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Restrict web content transfer with other apps](app-protection-policy-settings-ios.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Genmoji](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Screen capture](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Writing tools](app-protection-policy-settings-ios.md#functionality) | Allow |

8. Select **Next**.  
9. On the **Access requirements** tab, configure:  

| Setting | Value |
|--------|--------|
| [PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-ios.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Select minimum PIN length](app-protection-policy-settings-ios.md#access-requirements) | 4 |
| [Touch ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-ios.md#access-requirements) | Require (1440 minutes) |
| [Face ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Biometric instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [PIN reset after number of days](app-protection-policy-settings-ios.md#access-requirements) | No |
| [App PIN when device PIN is set](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-ios.md#access-requirements) | Not required |
| [Recheck access requirements after](app-protection-policy-settings-ios.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Max PIN attempts](app-protection-policy-settings-ios.md#conditional-launch) | 5 / Reset PIN |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 90 days / Wipe data |
| [Jailbroken/rooted devices](app-protection-policy-settings-ios.md#conditional-launch) | Block access |

11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level1-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.  

### Level 2 – Enterprise enhanced data protection for iOS/iPadOS

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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

| Setting | Value |
|--------|--------|
| [Back up org data to](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Send org data to other apps](app-protection-policy-settings-ios.md#data-transfer) | Policy managed apps |
| [Select apps to exempt](app-protection-policy-settings-ios.md#data-transfer) | skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services |
| [Receive data from other apps](app-protection-policy-settings-ios.md#data-transfer) | All apps |
| [Save copies of org data](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Allow users to save copies to selected services](app-protection-policy-settings-ios.md#data-transfer) | OneDrive for Business, SharePoint Online, Photo Library |
| [Transfer telecommunication data to](app-protection-policy-settings-ios.md#data-transfer) | Any dialer app |
| [Transfer messaging data to](app-protection-policy-settings-ios.md#data-transfer) | Any messaging app |
| [Restrict cut, copy, and paste between apps](app-protection-policy-settings-ios.md#data-transfer) | Policy managed apps with paste in |
| [Third-party keyboards](app-protection-policy-settings-ios.md#data-transfer) | Allow |
| [Encrypt org data](app-protection-policy-settings-ios.md#encryption) | Require |
| [Sync policy managed app data with native contacts app](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Print org data](app-protection-policy-settings-ios.md#functionality) | Allow |
| [Restrict web content transfer with other apps](app-protection-policy-settings-ios.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-ios.md#functionality) | Block org data |
| [Genmoji](app-protection-policy-settings-ios.md#functionality) | Block |
| [Screen capture](app-protection-policy-settings-ios.md#functionality) | Block |
| [Writing tools](app-protection-policy-settings-ios.md#functionality) | Block |

8. Select **Next**.  
9. On the **Access requirements** tab, configure:  

| Setting | Value |
|--------|--------|
| [PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-ios.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Select minimum PIN length](app-protection-policy-settings-ios.md#access-requirements) | 4 |
| [Touch ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-ios.md#access-requirements) | Require (1440 minutes) |
| [Face ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Biometric instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [PIN reset after number of days](app-protection-policy-settings-ios.md#access-requirements) | No |
| [App PIN when device PIN is set](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-ios.md#access-requirements) | Not required |
| [Recheck access requirements after](app-protection-policy-settings-ios.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Disabled account](app-protection-policy-settings-ios.md#conditional-launch) | Block access |
| [Min OS version](app-protection-policy-settings-ios.md#conditional-launch) | 14.8 / Block access |
| [Min patch version](app-protection-policy-settings-ios.md#conditional-launch) | 2024-10-01 / Block access |
| [Min app version](app-protection-policy-settings-ios.md#conditional-launch) | Latest / Warn |
| [Max PIN attempts](app-protection-policy-settings-ios.md#conditional-launch) | 5 / Reset PIN |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 30 days / Wipe data |
| [Jailbroken/rooted devices](app-protection-policy-settings-ios.md#conditional-launch) | Block access |

11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level2-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.

### Level 3 – Enterprise high data protection for iOS/iPadOS

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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

| Setting | Value |
|--------|--------|
| [Back up org data to](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Send org data to other apps](app-protection-policy-settings-ios.md#data-transfer) | Policy managed apps |
| [Select apps to exempt](app-protection-policy-settings-ios.md#data-transfer) | skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services |
| [Receive data from other apps](app-protection-policy-settings-ios.md#data-transfer) | Policy managed apps |
| [Save copies of org data](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Allow users to save copies to selected services](app-protection-policy-settings-ios.md#data-transfer) | OneDrive for Business, SharePoint, Camera, Photo Library |
| [Transfer telecommunication data to](app-protection-policy-settings-ios.md#data-transfer) | A specific dialer app |
| [Dialer App URL Scheme](app-protection-policy-settings-ios.md#data-transfer) | replace_with_dialer_app_url_scheme |
| [Transfer messaging data to](app-protection-policy-settings-ios.md#data-transfer) | A specific dialer app |
| [Messaging App URL Scheme](app-protection-policy-settings-ios.md#data-transfer) | replace_with_messaging_app_url_scheme |
| [Restrict cut, copy, and paste between apps](app-protection-policy-settings-ios.md#data-transfer) | Policy managed apps with paste in |
| [Open data into org documents](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Third-party keyboards](app-protection-policy-settings-ios.md#data-transfer) | Block |
| [Encrypt org data](app-protection-policy-settings-ios.md#encryption) | Require |
| [Sync policy managed app data with native contacts app](app-protection-policy-settings-ios.md#functionality) | Block |
| [Print org data](app-protection-policy-settings-ios.md#functionality) | Block |
| [Restrict web content transfer with other apps](app-protection-policy-settings-ios.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-ios.md#functionality) | Block org data |
| [Genmoji](app-protection-policy-settings-ios.md#functionality) | Block |
| [Screen capture](app-protection-policy-settings-ios.md#functionality) | Block |
| [Writing tools](app-protection-policy-settings-ios.md#functionality) | Block |

8. Select **Next**.  
9. On the **Access requirements** tab, configure:

| Setting | Value |
|--------|--------|
| [PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-ios.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-ios.md#access-requirements) | Block |
| [Select minimum PIN length](app-protection-policy-settings-ios.md#access-requirements) | 6 |
| [Touch ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Face ID instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Biometric instead of PIN for access](app-protection-policy-settings-ios.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [Override Touch ID with PIN after timeout](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [PIN reset after number of days](app-protection-policy-settings-ios.md#access-requirements) | Yes (90 days) |
| [App PIN when device PIN is set](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-ios.md#access-requirements) | Require |
| [Recheck access requirements after](app-protection-policy-settings-ios.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Jailbroken/rooted devices](app-protection-policy-settings-ios.md#conditional-launch) | Wipe data |
| [Max allowed threat level](app-protection-policy-settings-ios.md#conditional-launch) | Secured / Block access |
| [Max OS version](app-protection-policy-settings-ios.md#conditional-launch) | 26.0.1 / Block access |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-ios.md#conditional-launch) | 30 days / Block access |
| [Disabled account](app-protection-policy-settings-ios.md#conditional-launch) | Block access |
| [Min OS version](app-protection-policy-settings-ios.md#conditional-launch) | 14.8 / Block access |
| [Min patch version](app-protection-policy-settings-ios.md#conditional-launch) | 2024-10-01 / Block access |
| [Min app version](app-protection-policy-settings-ios.md#conditional-launch) | Latest / Warn |
| [Min SDK version](app-protection-policy-settings-ios.md#conditional-launch) | 21.1.0 / Block access |
| [Max PIN attempts](app-protection-policy-settings-ios.md#conditional-launch) | 5 / Reset PIN |

11. Select **Next**.  
12. On the **Assignments** tab, assign the policy to **SEB-Level3-Users**.  
13. Select **Next**, review the configuration, and then choose **Create**.

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

| Setting | Value |
|--------|--------|
| [Back up org data to Android backup services](app-protection-policy-settings-android.md#data-transfer) | Allow |
| [Send org data to other apps](app-protection-policy-settings-android.md#data-transfer) | All apps |
| [Receive data from other apps](app-protection-policy-settings-android.md#data-transfer) | All apps |
| [Restrict cut, copy, and paste between other apps](app-protection-policy-settings-android.md#data-transfer) | Any app |
| [Screen capture and Google Assistant](app-protection-policy-settings-android.md#functionality) | Allow |
| [Approved keyboards](app-protection-policy-settings-android.md#data-transfer) | Not required |
| [Encrypt org data](app-protection-policy-settings-android.md#encryption) | Require |
| [Encrypt org data on enrolled devices](app-protection-policy-settings-android.md#encryption) | Require |
| [Sync policy managed app data with native apps or add-ins](app-protection-policy-settings-android.md#functionality) | Allow |
| [Printing org data](app-protection-policy-settings-android.md#functionality) | Allow |
| [Restrict web content transfer with other apps](app-protection-policy-settings-android.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-android.md#functionality) | Allow |

8. Select **Next**.  
9. On the **Access requirements** tab, configure:

| Setting | Value |
|--------|--------|
| [PIN required](app-protection-policy-settings-android.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-android.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-android.md#access-requirements) | Allow |
| [Select minimum PIN length](app-protection-policy-settings-android.md#access-requirements) | 4 |
| [Biometric instead of PIN for access](app-protection-policy-settings-android.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Timeout (minutes of inactivity)](app-protection-policy-settings-android.md#access-requirements) | 1440 |
| [Class 3 Biometrics (Android 9.0+)](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [Override Biometrics with PIN after biometric updates](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [PIN reset after number of days](app-protection-policy-settings-android.md#access-requirements) | No |
| [Select number of previous PIN values to maintain](app-protection-policy-settings-android.md#access-requirements) | 0 |
| [App PIN when device PIN is set](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [Recheck access requirements after](app-protection-policy-settings-android.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Max PIN attempts](app-protection-policy-settings-android.md#app-conditions) | 5 / Reset PIN |
| [Offline grace period](app-protection-policy-settings-android.md#app-conditions) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-android.md#app-conditions) | 90 days / Wipe data |
| [Jailbroken/rooted devices](app-protection-policy-settings-android.md#device-conditions) | Block access |
| [Play integrity verdict](app-protection-policy-settings-android.md#device-conditions) | Basic integrity / Block access |
| [Require threat scan on apps](app-protection-policy-settings-android.md#device-conditions) | Block access |
| [Require device lock](app-protection-policy-settings-android.md#device-conditions) | Low Complexity / Block access |

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

| Setting | Value |
|--------|--------|
| [Back up org data to Android backup services](app-protection-policy-settings-android.md#data-transfer) | Block |
| [Send org data to other apps](app-protection-policy-settings-android.md#data-transfer) | Policy managed apps |
| [Receive data from other apps](app-protection-policy-settings-android.md#data-transfer) | All apps |
| [Save copies of org data](app-protection-policy-settings-android.md#data-transfer) | Block |
| [Allow users to save copies to selected services](app-protection-policy-settings-android.md#data-transfer) | OneDrive for Business, SharePoint, Photo Library |
| [Transfer telecommunication data to](app-protection-policy-settings-android.md#data-transfer) | Any dialer app |
| [Transfer messaging data to](app-protection-policy-settings-android.md#data-transfer) | Any messaging app |
| [Restrict cut, copy, and paste between apps](app-protection-policy-settings-android.md#data-transfer) | Policy managed apps with paste in |
| [Screen capture and Google Assistant](app-protection-policy-settings-android.md#functionality) | Block |
| [Approved keyboards](app-protection-policy-settings-android.md#data-transfer) | Not required |
| [Encrypt org data](app-protection-policy-settings-android.md#encryption) | Require |
| [Encrypt org data on enrolled devices](app-protection-policy-settings-android.md#encryption) | Require |
| [Sync policy managed app data with native apps or add-ins](app-protection-policy-settings-android.md#functionality) | Allow |
| [Printing org data](app-protection-policy-settings-android.md#functionality) | Allow |
| [Restrict web content transfer with other apps](app-protection-policy-settings-android.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-android.md#functionality) | Block org data |

8. Select **Next**
9. On the **Access requirements** tab, configure:

| Setting | Value |
|--------|--------|
| [PIN required](app-protection-policy-settings-android.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-android.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-android.md#access-requirements) | Allow |
| [Select minimum PIN length](app-protection-policy-settings-android.md#access-requirements) | 4 |
| [Biometric instead of PIN for access](app-protection-policy-settings-android.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Timeout (minutes of inactivity)](app-protection-policy-settings-android.md#access-requirements) | 1440 |
| [Class 3 Biometrics (Android 9.0+)](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [Override Biometrics with PIN after biometric updates](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [PIN reset after number of days](app-protection-policy-settings-android.md#access-requirements) | No |
| [Select number of previous PIN values to maintain](app-protection-policy-settings-android.md#access-requirements) | 0 |
| [App PIN when device PIN is set](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-android.md#access-requirements) | Not required |
| [Recheck access requirements after](app-protection-policy-settings-android.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Disabled account](app-protection-policy-settings-android.md#app-conditions) | Block access |
| [Offline grace period](app-protection-policy-settings-android.md#app-conditions) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-android.md#app-conditions) | 30 days / Wipe data |
| [Min OS version](app-protection-policy-settings-android.md#device-conditions) | 9.0 / Block access |
| [Min patch version](app-protection-policy-settings-android.md#device-conditions) | 2024-10-01 / Block access |
| [Play integrity verdict](app-protection-policy-settings-android.md#device-conditions) | Basic integrity and device integrity / Block access |
| [Jailbroken/rooted devices](app-protection-policy-settings-android.md#device-conditions) | Block access |
| [Require threat scan on apps](app-protection-policy-settings-android.md#device-conditions) | Block access |
| [Require device lock](app-protection-policy-settings-android.md#conditional-launch) | Medium / Block access |
| [Samsung Knox device attestation](app-protection-policy-settings-android.md#conditional-launch) | Block access on supported devices |
| [Max PIN attempts](app-protection-policy-settings-android.md#app-conditions) | 5 / Reset PIN |

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

| Setting | Value |
|--------|--------|
| [Back up org data to Android backup services](app-protection-policy-settings-android.md#data-transfer) | Block |
| [Send org data to other apps](app-protection-policy-settings-android.md#data-transfer) | Policy managed apps |
| [Receive data from other apps](app-protection-policy-settings-android.md#data-transfer) | Policy managed apps |
| [Save copies of org data](app-protection-policy-settings-android.md#data-transfer) | Block |
| [Allow users to save copies to selected services](app-protection-policy-settings-android.md#data-transfer) | OneDrive for Business, SharePoint, Camera, Photo Library |
| [Allow users to open data from selected services](app-protection-policy-settings-android.md#data-transfer) | OneDrive for Business, SharePoint, Camera, Photo Library |
| [Transfer telecommunication data to](app-protection-policy-settings-android.md#data-transfer) | Any policy-managed dialer app |
| [Transfer messaging data to](app-protection-policy-settings-android.md#data-transfer) | Any policy-managed messaging app |
| [Restrict cut, copy, and paste between apps](app-protection-policy-settings-android.md#data-transfer) | Policy managed apps with paste in |
| [Open data into org documents](app-protection-policy-settings-android.md#data-transfer) | Block |
| [Approved keyboards](app-protection-policy-settings-android.md#data-transfer) | Require (Microsoft SwiftKey Keyboard, Samsung Keyboard, Gboard – the Google Keyboard) |
| [Screen capture and Google Assistant](app-protection-policy-settings-android.md#functionality) | Block |
| [Encrypt org data](app-protection-policy-settings-android.md#encryption) | Require |
| [Encrypt org data on enrolled devices](app-protection-policy-settings-android.md#encryption) | Require |
| [Sync policy managed app data with native apps or add-ins](app-protection-policy-settings-android.md#functionality) | Block |
| [Printing org data](app-protection-policy-settings-android.md#functionality) | Block |
| [Restrict web content transfer with other apps](app-protection-policy-settings-android.md#functionality) | Microsoft Edge |
| [Org data notifications](app-protection-policy-settings-android.md#functionality) | Block org data |

8. Select **Next**.  
9. On the **Access requirements** tab, configure:

| Setting | Value |
|--------|--------|
| [PIN required](app-protection-policy-settings-android.md#access-requirements) | Require |
| [PIN type](app-protection-policy-settings-android.md#access-requirements) | Numeric |
| [Simple PIN](app-protection-policy-settings-android.md#access-requirements) | Block |
| [Select minimum PIN length](app-protection-policy-settings-android.md#access-requirements) | 6 |
| [Biometric instead of PIN for access](app-protection-policy-settings-android.md#access-requirements) | Allow |
| [Override biometrics with PIN after timeout](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Timeout (minutes of inactivity)](app-protection-policy-settings-android.md#access-requirements) | 30 |
| [Class 3 Biometrics (Android 9.0+)](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Override Biometrics with PIN after biometric updates](app-protection-policy-settings-android.md#access-requirements) | Require |
| [PIN reset after number of days](app-protection-policy-settings-android.md#access-requirements) | Yes (90 days) |
| [Select number of previous PIN values to maintain](app-protection-policy-settings-android.md#access-requirements) | 0 |
| [App PIN when device PIN is set](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Work or school account credentials for access](app-protection-policy-settings-android.md#access-requirements) | Require |
| [Recheck access requirements after](app-protection-policy-settings-android.md#access-requirements) | 30 minutes |

10. On the **Conditional launch** tab, configure:

| Setting | Value |
|--------|--------|
| [Require device lock](app-protection-policy-settings-android.md#device-conditions) | High Complexity / Block access |
| [Jailbroken/rooted devices](app-protection-policy-settings-android.md#conditional-launch) | Wipe data |
| [Max allowed threat level](app-protection-policy-settings-android.md#conditional-launch) | Secured / Block access |
| [Max OS version](app-protection-policy-settings-android.md#conditional-launch) | 16.0 / Block access |
| [Samsung Knox device attestation](app-protection-policy-settings-android.md#conditional-launch) | Wipe data |
| [Offline grace period](app-protection-policy-settings-android.md#app-conditions) | 10080 minutes / Block access |
| [Offline grace period](app-protection-policy-settings-android.md#conditional-launch) | 30 days / Block access |
| [Disabled account](app-protection-policy-settings-android.md#app-conditions) | Block access |
| [Min OS version](app-protection-policy-settings-android.md#device-conditions) | 9.0 / Block access |
| [Min patch version](app-protection-policy-settings-android.md#device-conditions) | 2024-10-01 / Block access |
| [Play integrity verdict](app-protection-policy-settings-android.md#device-conditions) | Basic integrity and device integrity / Block access |
| [Play integrity verdict evaluation type](app-protection-policy-settings-android.md#device-conditions) | Check strong integrity |
| [Require threat scan on apps](app-protection-policy-settings-android.md#device-conditions) | Block access |
| [Max Company Portal version age (days)](app-protection-policy-settings-android.md#device-conditions) | 180 / Block access |
| [Max PIN attempts](app-protection-policy-settings-android.md#app-conditions) | 5 / Reset PIN |

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
