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

::: zone pivot="windows"

## App protection policies for Windows

App protection policies for Windows provide secure and compliant access to work resources on personal computers by using Data Loss Prevention (DLP) controls.

> [!IMPORTANT]
> Framework alignment:  
> These configurations align with Microsoft's Data Protection Framework and are mapped to NIST, DISA STIG, and CISA controls as defined in the [Secure Your Corporate Data in Intune with Microsoft Edge for Business](mamedge-overview.md) guide.
> 
> This guide references industry frameworks (NIST, DISA STIG, CISA) as inputs. Applying these settings does not by itself make your organization compliant with any specific standard; perform your own compliance assessments against official requirements.

> **Microsoft Data Protection Framework Compliance:**
> - **Level 1** – Fully compliant with Microsoft’s “Enterprise Basic Data Protection” requirements  
> - **Level 2** – Fully compliant with Microsoft’s “Enterprise Enhanced Data Protection” requirements  
> - **Level 3** – Fully compliant with Microsoft’s “Enterprise High Data Protection” requirements  

#### Prerequisites:

- Windows
- Company Portal installed
- Appropriate Intune license (APP support)
- Microsoft Edge sign-in with Microsoft Entra ID account

### Level 1 – Enterprise basic data protection (Windows)

Level 1 configuration provides the minimum data protection for a Windows device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Windows**.  
3. On the **Basics** step, set:  
   - **Name:** Level 1 – Enterprise basic data protection – Windows  
   - **Description:** Provides Level 1 basic data protection for Microsoft Edge for Business on Windows devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Send org data to other apps:** All destinations  
   - **Receive data from other apps:** All sources  
   - **Allow cut, copy, and paste for:** Any destination and any source  
   - **Print org data:** Allow  
6. **Next** > **Health checks**, configure:  
   - **Offline grace period:** 10,080 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Max allowed device threat level:** Low, Block access  
7. **Next** through **Scope tags**, assign to **SEB-Level1-Users** group.  
8. **Create**.

### Level 2 – Enterprise enhanced data protection (Windows)

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Windows**.  
3. On the **Basics** step, set:  
   - **Name:** Level 2 – Enterprise enhanced data protection – Windows  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on Windows devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Send org data to other apps:** No destinations  
   - **Receive data from other apps:** No sources  
   - **Allow cut, copy, and paste for:** No destination or source  
   - **Print org data:** Block  
6. **Next** > **Health checks**, configure:  
   - **Disabled account:** Block access  
   - **Min OS version:** 10.0.22621.2506, Block access  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 30 days, Wipe data  
   - **Max allowed device threat level:** Medium, Block access  
7. **Next** through **Scope tags**, assign to **SEB-Level2-Users** group.  
8. **Create**.

### Level 3 – Enterprise high data protection (Windows)

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Windows**.  
3. On the **Basics** step, set:  
   - **Name:** Level 3 – Enterprise high data protection – Windows  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on Windows devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Send org data to other apps:** No destinations  
   - **Receive data from other apps:** No sources  
   - **Allow cut, copy, and paste for:** No destination or source  
   - **Print org data:** Block  

   :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png" alt-text="Apps - App protection policies - Create policy - Data Protection in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png":::

6. **Next** > **Health checks**, configure:  
   - **Min OS version:** 10.0.22621.2506, Block access  
   - **Offline grace period:** 1440 minutes, Block access  
   - **Offline grace period:** 30 days, Wipe data  
   - **Max OS version:** 10.0.22641, Warn  
   - **Max allowed device threat level:** Secured, Block access  

   :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png" alt-text="Apps - App protection policies - Create policy - Health Checks in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png":::

7. **Next** > select appropriate scope tag.  
8. Assign to **SEB-Level3-Users** group.  
9. **Review + create** > **Create**.  

**Validation:**
- In Intune console: **Apps > App protection policies > select policy > Monitor > App protection status**.  
- On client: Sign in to Edge with organization account and attempt copy/paste to an unmanaged app → should be blocked on Levels 2 and 3.  

**Framework Compliance Summary**

| Microsoft Framework Requirement | Level 1 | Level 2 | Level 3 | Status |
|--------------------------------|----------|----------|----------|---------|
| Data transfer restrictions | All destinations/sources | No destinations/sources | No destinations/sources | ✅ |
| Copy/paste controls | Any destination/source | No destination/source | No destination/source | ✅ |
| Screen capture | Allow | Block | Block | ✅ |
| Encryption | Not required | Required | Required | ✅ |
| Offline grace period | 10,080 min / 90 days | 720 min / 30 days | 1440 min / 30 days | ✅ |
| OS version requirements | Not required | Min required | Min + Max required | ✅ |
| Device threat level | Low | Medium | Secured | ✅ |
| Print restrictions | Allow | Block | Block | ✅ |

::: zone-end

::: zone pivot="ios-ipados"

## App protection policies for iOS/iPadOS

App protection policies for iOS/iPadOS provide data protection for Microsoft Edge for Business on mobile devices without requiring device enrollment.

> [!IMPORTANT]
> Framework alignment:  
> These configurations align with Microsoft's Data Protection Framework and are mapped to NIST, DISA STIG, and CISA controls as defined in the [Secure Your Corporate Data in Intune with Microsoft Edge for Business](mamedge-overview.md) guide.
> 
> This guide references industry frameworks (NIST, DISA STIG, CISA) as inputs. Applying these settings does not by itself make your organization compliant with any specific standard; perform your own compliance assessments against official requirements.

> [!NOTE]
> **Microsoft Data Protection Framework Compliance:**
> - **Level 1** – Fully compliant with Microsoft's "Enterprise Basic Data Protection" requirements  
> - **Level 2** – Fully compliant with Microsoft's "Enterprise Enhanced Data Protection" requirements  
> - **Level 3** – Fully compliant with Microsoft's "Enterprise High Data Protection" requirements
> - **Web Content Transfer** – All policies include "Restrict web content transfer with other apps" set to Microsoft Edge

#### Prerequisites:

- iOS/iPadOS 15+
- Microsoft Edge for iOS installed
- Company Portal or MAM managed
- User Microsoft Entra ID account

### Level 1 – Enterprise basic data protection (iOS/iPadOS)

Level 1 configuration provides the minimum data protection for an iOS/iPadOS device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > iOS/iPadOS**.  
3. On the **Basics** step, set:  
   - **Name:** Level 1 – Enterprise basic data protection – iOS/iPadOS  
   - **Description:** Provides Level 1 basic data protection for Microsoft Edge for Business on iOS/iPadOS devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Back up org data to:** Allow  
   - **Send org data to other apps:** All apps  
   - **Receive data from other apps:** All apps  
   - **Save copies of org data:** Allow  
   - **Restrict cut, copy, and paste between other apps:** Any app  
   - **Org data notifications:** Allow  
   - **Third-party keyboards:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Allow  
   - **Printing org data:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
7. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Allow  
   - **Select Minimum PIN length:** 4  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Not required  
   - **Timeout (minutes of activity):** 720  
   - **Face ID instead of PIN for access:** Allow  
   - **PIN reset after number of days:** No  
   - **App PIN when device PIN is set:** Not required  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
8. **Next** > **Conditional launch**, configure:  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken/rooted devices:** Block access  
9. **Next** through **Scope tags**, assign to **SEB-Level1-Users** group.  
10. **Create**.

### Level 2 – Enterprise enhanced data protection (iOS/iPadOS)

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > iOS/iPadOS**.  
3. On the **Basics** step, set:  
   - **Name:** Level 2 – Enterprise enhanced data protection – iOS/iPadOS  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on iOS/iPadOS devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Back up org data to iTunes and iCloud backups:** Block  
   - **Send org data to other apps:** Policy managed apps  
   - **Select apps to exempt:** Default / skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;  
   - **Receive data from other apps:** Policy managed apps  
   - **Open data into Org documents:** Block  
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library  
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint  
   - **Restrict cut, copy, and paste between other apps:** Policy managed apps with paste in  
   - **Org data notifications:** Block org data  
   - **Third-party keyboards:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Encryption**, configure:  
   - **Encrypt org data:** Require  
7. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Block  
   - **Printing org data:** Block  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
8. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Block  
   - **Select Minimum PIN length:** 6  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of activity):** 30  
   - **Face ID instead of PIN for access:** Allow  
   - **PIN reset after number of days:** Yes, 365 days  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
9. **Next** > **Conditional launch**, configure:  
   - **Disabled account:** Block access  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 30 days, Wipe data  
   - **Jailbroken/rooted devices:** Wipe data  
   - **Min OS version:** (Format: Major.Minor.Build), Warn  
   - **Min app version:** (Latest recommended), Warn  
   - **Max allowed threat level:** Medium, Block access  
10. **Next** through **Scope tags**, assign to **SEB-Level2-Users** group.  
11. **Create**.

### Level 3 – Enterprise high data protection (iOS/iPadOS)

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > iOS/iPadOS**.  
3. On the **Basics** step, set:  
   - **Name:** Level 3 – Enterprise high data protection – iOS/iPadOS  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on iOS/iPadOS devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Transfer telecommunication data to:** A specific dialer app  
   - **Dialer App URL Scheme:** replace_with_dialer_app_url_scheme  
   - **Back up org data to iTunes and iCloud backups:** Block  
   - **Send org data to other apps:** Policy managed apps  
   - **Select apps to exempt:** Default / skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;  
   - **Receive data from other apps:** Policy managed apps  
   - **Open data into Org documents:** Block  
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library  
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint Online, Photo Library  
   - **Restrict cut, copy, and paste between other apps:** Policy managed apps with paste in  
   - **Org data notifications:** Block org data  
   - **Third-party keyboards:** Block  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Encryption**, configure:  
   - **Encrypt org data:** Require  
7. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Block  
   - **Printing org data:** Block  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
8. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Block  
   - **Select Minimum PIN length:** 6  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of activity):** 30  
   - **Face ID instead of PIN for access:** Allow  
   - **PIN reset after number of days:** Yes, 365 days  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
9. **Next** > **Conditional launch**, configure:  
   - **Disabled account:** Block access  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken/rooted devices:** Wipe data  
   - **Min OS version:** (Format: Major.Minor.Build), Block access  
   - **Max OS version:** (Format: Major.Minor.Build), Warn  
   - **Min app version:** (Latest recommended), Block access  
   - **Max allowed threat level:** Secured, Block access  
10. **Next** through **Scope tags**, assign to **SEB-Level3-Users** group.  
11. **Create**.

**Validation:**
- In Intune console: **Apps > App protection policies > select policy > Monitor > App protection status**.  
- On iOS device: Open Edge > Menu > Settings > confirm corporate policies applied.  
- Test data protection: Attempt copy/paste, save, and screenshot operations – should be blocked per level.  

::: zone-end

::: zone pivot="android"

## App protection policies for Android

App protection policies for Android provide data protection for Microsoft Edge for Business on mobile devices without requiring device enrollment.

> [!IMPORTANT]
> Framework alignment:  
> These configurations align with Microsoft's Data Protection Framework and are mapped to NIST, DISA STIG, and CISA controls as defined in the [Secure Your Corporate Data in Intune with Microsoft Edge for Business](mamedge-overview.md) guide.
> 
> This guide references industry frameworks (NIST, DISA STIG, CISA) as inputs. Applying these settings does not by itself make your organization compliant with any specific standard; perform your own compliance assessments against official requirements.

> [!NOTE]
> **Microsoft Data Protection Framework Compliance:**
> - **Level 1** – Fully compliant with Microsoft's "Enterprise Basic Data Protection" requirements  
> - **Level 2** – Fully compliant with Microsoft's "Enterprise Enhanced Data Protection" requirements  
> - **Level 3** – Fully compliant with Microsoft's "Enterprise High Data Protection" requirements
> - **Web Content Transfer** – All policies include "Restrict web content transfer with other apps" set to Microsoft Edge

#### Prerequisites:

- Android 8.0+
- Microsoft Edge for Android installed
- Company Portal or MAM managed
- User Microsoft Entra ID account

### Level 1 – Enterprise basic data protection (Android)

Level 1 configuration provides the minimum data protection for an Android device while minimizing effects to users.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Android**.  
3. On the **Basics** step, set:  
   - **Name:** Level 1 – Enterprise basic data protection – Android  
   - **Description:** Provides Level 1 basic data protection for Microsoft Edge for Business on Android devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Back up org data to:** Allow  
   - **Send org data to other apps:** All apps  
   - **Receive data from other apps:** All apps  
   - **Save copies of org data:** Allow  
   - **Restrict cut, copy, and paste between other apps:** Any app  
   - **Screen capture and Google Assistant:** Allow  
   - **Approved keyboards:** Not required  
   - **Org data notifications:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Allow  
   - **Printing org data:** Allow  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
7. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Allow  
   - **Select Minimum PIN length:** 4  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Not required  
   - **Timeout (minutes of activity):** 720  
   - **PIN reset after number of days:** No  
   - **App PIN when device PIN is set:** Not required  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
8. **Next** > **Conditional launch**, configure:  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken/rooted devices:** Block access  
9. **Next** through **Scope tags**, assign to **SEB-Level1-Users** group.  
10. **Create**.

### Level 2 – Enterprise enhanced data protection (Android)

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Android**.  
3. On the **Basics** step, set:  
   - **Name:** Level 2 – Enterprise enhanced data protection – Android  
   - **Description:** Provides Level 2 enhanced data protection for Microsoft Edge for Business on Android devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Back up org data to:** Block  
   - **Send org data to other apps:** Policy managed apps  
   - **Receive data from other apps:** Policy managed apps  
   - **Open data into Org documents:** Block  
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library  
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint  
   - **Restrict cut, copy, and paste between other apps:** Policy managed apps with paste in  
   - **Screen capture and Google Assistant:** Block  
   - **Approved keyboards:** Require  
   - **Select keyboards to approve:** Add/remove keyboards as needed  
   - **Org data notifications:** Block org data  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Encryption**, configure:  
   - **Encrypt org data:** Require  
   - **Encrypt org data on enrolled devices:** Require  
7. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Block  
   - **Printing org data:** Block  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
8. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Block  
   - **Select Minimum PIN length:** 6  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of activity):** 30  
   - **PIN reset after number of days:** Yes, 365 days  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
9. **Next** > **Conditional launch**, configure:  
   - **Disabled account:** Block access  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 30 days, Wipe data  
   - **Jailbroken/rooted devices:** Wipe data  
   - **Min OS version:** (Format: Major.Minor), Warn  
   - **Min patch version:** (Format: YYYY-MM-DD), Warn  
   - **SafetyNet device attestation:** Basic integrity, Warn  
   - **Require threat scan on apps:** Block access  
   - **Max allowed threat level:** Medium, Block access  
10. **Next** through **Scope tags**, assign to **SEB-Level2-Users** group.  
11. **Create**.

### Level 3 – Enterprise high data protection (Android)

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps > App protection policies > Create policy > Android**.  
3. On the **Basics** step, set:  
   - **Name:** Level 3 – Enterprise high data protection – Android  
   - **Description:** Provides Level 3 high data protection for Microsoft Edge for Business on Android devices.  
4. **Next** > **Apps** > select **Microsoft Edge** > **Select**.  
5. **Next** > **Data protection**, configure:  
   - **Transfer telecommunication data to:** Any policy-managed dialer app  
   - **Back up org data to:** Block  
   - **Send org data to other apps:** Policy managed apps  
   - **Receive data from other apps:** Policy managed apps  
   - **Open data into Org documents:** Block  
   - **Allow users to open data from selected services:** OneDrive for Business, SharePoint, Camera, Photo Library  
   - **Save copies of org data:** Block  
   - **Allow users to save copies to selected services:** OneDrive for Business, SharePoint Online, Photo Library  
   - **Restrict cut, copy, and paste between other apps:** Policy managed apps with paste in  
   - **Screen capture and Google Assistant:** Block  
   - **Approved keyboards:** Require  
   - **Select keyboards to approve:** Add/remove keyboards as needed  
   - **Org data notifications:** Block org data  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
6. **Next** > **Encryption**, configure:  
   - **Encrypt org data:** Require  
   - **Encrypt org data on enrolled devices:** Require  
7. **Next** > **Functionality**, configure:  
   - **Sync policy managed app data with native apps or add-ins:** Block  
   - **Printing org data:** Block  
   - **Restrict web content transfer with other apps:** Microsoft Edge  
8. **Next** > **Access requirements**, configure:  
   - **PIN for access:** Require  
   - **PIN type:** Numeric  
   - **Simple PIN:** Block  
   - **Select Minimum PIN length:** 6  
   - **Biometric instead of PIN for access:** Allow  
   - **Override biometrics with PIN after timeout:** Require  
   - **Timeout (minutes of activity):** 30  
   - **PIN reset after number of days:** Yes, 365 days  
   - **App PIN when device PIN is set:** Require  
   - **Work or school account credentials for access:** Not required  
   - **Recheck access requirements after:** 30 minutes  
9. **Next** > **Conditional launch**, configure:  
   - **Disabled account:** Block access  
   - **Max PIN attempts:** 5, Reset PIN  
   - **Offline grace period:** 720 minutes, Block access  
   - **Offline grace period:** 90 days, Wipe data  
   - **Jailbroken/rooted devices:** Wipe data  
   - **Min OS version:** (Format: Major.Minor), Block access  
   - **Max OS version:** (Format: Major.Minor), Warn  
   - **Min patch version:** (Format: YYYY-MM-DD), Block access  
   - **Min app version:** (Latest recommended), Block access  
   - **SafetyNet device attestation:** Basic integrity and certified devices, Block access  
   - **Required SafetyNet evaluation type:** Hardware-backed key  
   - **Require threat scan on apps:** Block access  
   - **Require device lock:** High, Block access  
   - **Max allowed threat level:** Secured, Block access  
   - **Samsung Knox device attestation:** Block access  
10. **Next** through **Scope tags**, assign to **SEB-Level3-Users** group.  
11. **Create**.

**Validation:**
- In Intune console: **Apps > App protection policies > select policy > Monitor > App protection status**.  
- On Android device: Open Edge > Menu > Settings > confirm corporate policies applied.  
- Test data protection: Attempt copy/paste, save, screenshot, and Google Assistant operations – should be blocked per level.  
- Test SafetyNet attestation: Verify device integrity checks are enforced (Level 2/3).

::: zone-end

## Related resources

For specific recommendations per level, see [Data protection framework using app protection policies](../apps/app-protection-framework.md).

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-03.png" alt-text="Step 3 to integrate Mobile Threat Defense with Microsoft Edge for Business.":::](mamedge-3-scc.md)

Continue with [Step 3](mamedge-3-scc.md) to integrate Mobile Threat Defense with Microsoft Edge for Business.
