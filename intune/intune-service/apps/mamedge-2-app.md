---
title: Step 2. Create App Protection Policies for Microsoft Edge for Business
description: Step 2. Create app protection policies for Microsoft Edge for Business across Windows, Android, and iOS platforms.
ms.date: 10/28/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 2: App Protection Policies for Microsoft Edge for Business

This guide organizes app protection policy creation by platform to help you implement the appropriate security level for each device type. The following sections provide detailed configuration steps for Windows, Android, and iOS/iPadOS platforms.

Each platform section includes instructions for creating Level 1, Level 2, and Level 3 app protection policies aligned with the Microsoft Data Protection Framework.

**Applies to:**
- Windows 10/11
- Android 8.0+
- iOS/iPadOS 15+

> [!NOTE]
> App protection policies provide data protection without requiring device enrollment, making them ideal for BYOD (Bring Your Own Device) scenarios and unmanaged devices.

## App protection policies for Windows

App protection policies for Windows provide secure and compliant access to work resources on personal computers by using Data Loss Prevention (DLP) controls.

> **Microsoft Documentation:**
> - [Windows App Protection Policies](app-protection-policies-configure-windows-10.md)
> - [App Protection Policy Settings for Windows](app-protection-policy-settings-windows.md)
> - [Microsoft Data Protection Framework](app-protection-framework.md)

> [!IMPORTANT]
> **Microsoft Data Protection Framework Compliance:**
> - **Level 1**: Fully compliant with Microsoft's "Enterprise Basic Data Protection" requirements
> - **Level 2**: Fully compliant with Microsoft's "Enterprise Enhanced Data Protection" requirements  
> - **Level 3**: Fully compliant with Microsoft's "Enterprise High Data Protection" requirements

**Prerequisites:** 
- Windows 10/11
- Company Portal installed
- Appropriate Intune license (APP support)
- Microsoft Edge sign-in with Microsoft Entra ID account

### Level 1 - Enterprise basic data protection (Windows)

Level 1 configuration provides the minimum data protection for a Windows device while minimizing effects to users.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App protection policies** > **Create policy** > **Windows**.

3. On the **Basics** step, set the following details:

    - **Name**: Level 1 - Enterprise basic data protection - Windows
    - **Description**: This policy provides Level 1 basic data protection for Microsoft Edge for Business on Windows devices.

4. Select **Next**.

5. For the **Apps** step, select **Select apps** > **Microsoft Edge** > **Select**.

6. Select **Next**.

7. For **Data protection**, configure the following Level 1 settings:

    - **Send org data to other apps**: Policy managed apps
    - **Receive data from other apps**: Policy managed apps
    - **Allow cut, copy, and paste for**: Policy managed apps
    - **Print org data**: Allow

8. Select **Next**.

9. For **Health checks**, configure the following Level 1 settings:

    - **Offline grace period**: 720 minutes, Block access
    - **Offline grace period**: 90 days, Wipe data
    - **Max allowed device threat level**: Not configured

10. Select **Next** through **Scope tags** and configure **Assignments** for the appropriate user groups.

11. Select **Create**.

### Level 2 - Enterprise enhanced data protection (Windows)

Level 1 configuration provides the minimum data protection for a Windows device while minimizing the effects to users.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App protection policies** > **Create policy** > **Windows**.

3. On the **Basics** step, set the following details:

    - **Name**: Level 1 - Enterprise basic data protection - Windows
    - **Description**: This policy provides Level 1 basic data protection for Microsoft Edge for Business on Windows devices.

4. Select **Next**.

5. For the **Apps** step, select **Select apps** > **Microsoft Edge** > **Select**.

6. Select **Next**.

7. For **Data protection**, configure the following Level 1 settings:

    - **Send org data to other apps**: Policy managed apps
    - **Receive data from other apps**: Policy managed apps
    - **Allow cut, copy, and paste for**: Policy managed apps
    - **Print org data**: Allow

8. Select **Next**.

9. For **Health checks**, configure the following Level 1 settings:

    - **Offline grace period**: 720 minutes, Block access
    - **Offline grace period**: 90 days, Wipe data
    - **Max allowed device threat level**: Not configured

10. Select **Next** through **Scope tags** and configure **Assignments** for the appropriate user groups.

11. Select **Create**.

### Level 2 - Enterprise enhanced data protection (Windows)

Level 2 configuration includes all Level 1 settings plus more controls for enhanced data protection.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App protection policies** > **Create policy** > **Windows**.

3. On the **Basics** step, set the following details:

    - **Name**: Level 2 - Enterprise enhanced data protection - Windows
    - **Description**: This policy provides Level 2 enhanced data protection for Microsoft Edge for Business on Windows devices.

4. Select **Next**.

5. For the **Apps** step, select **Select apps** > **Microsoft Edge** > **Select**.

6. Select **Next**.

7. For **Data protection**, configure the following Level 2 settings:

    - **Send org data to other apps**: Policy managed apps  
    - **Receive data from other apps**: Policy managed apps
    - **Allow cut, copy, and paste for**: Policy managed apps with paste in
    - **Print org data**: Block

8. Select **Next**.

9. For **Health checks**, configure the following Level 2 settings:

    - **Offline grace period**: 720 minutes, Block access
    - **Offline grace period**: 90 days, Wipe data
    - **Max allowed device threat level**: Medium, Block access

10. Select **Next** through **Scope tags** and configure **Assignments** for the appropriate user groups.

11. Select **Create**.

### Level 3 - Enterprise high data protection (Windows)

Level 3 configuration provides the highest level of data protection and is recommended for users accessing highly sensitive data.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App protection policies** > **Create policy** > **Windows**.

3. On the **Basics** step, set the following details:

    - **Name**: Level 3 - Enterprise high data protection - Windows
    - **Description**: This policy provides Level 3 high data protection for Microsoft Edge for Business on Windows devices.

4. Select **Next**.

5. For the **Apps** step, select **Select apps** > **Microsoft Edge** > **Select**.

6. Select **Next**.

7. For **Data protection**, configure the following Level 3 settings:

    - **Send org data to other apps**: No destinations
    - **Receive data from other apps**: No sources
    - **Allow cut, copy, and paste for**: No destination or source
    - **Print org data**: Block

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png" alt-text="Apps - App protection policies - Create policy - Data Protection in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png":::

8. Select **Next**.

9. For **Health checks**, configure the following Level 3 settings:

    - **Offline grace period**: 720 minutes, Block access
    - **Offline grace period**: 90 days, Wipe data
    - **Max OS version**: 10.0.22631.2715, Block access
    - **Max allowed device threat level**: Secured, Block access

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png" alt-text="Apps - App protection policies - Create policy - Health Checks in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png":::

10. Select **Next**.

11. For **Scope tags**, select the appropriate scope tag for your environment.

12. For **Assignments**, select **Add Group** and assign to the appropriate security group for Level 3 protection.

13. Select **Next**.

14. On **Review + create**, review the configuration and select **Create**.

## App protection policy for Microsoft Edge for Business (Mobile)

Incorporate Microsoft Edge for Business into your existing data security and management strategy. By securing the enterprise browser configuration for mobile devices, you can ensure safer and more efficient web browsing experiences.

Microsoft Edge for Business provide benefits for both management and security:

- **Management**: Microsoft Edge for Business is the only mobile browser natively supported by Microsoft Intune with seamless integration. To secure productivity for your organization, App level management allows IT to configure the right balance between data protection and access.
- **Security**: Data protection and leakage prevention are based on Conditional Access and user identities. Microsoft 365 security features extend to Microsoft Edge for Business mobile including Microsoft Entra Conditional Access, and Data Loss Prevention. For organizations utilizing VPN solutions, Microsoft Edge mobile offers support for identity-enlightened per-app VPN. This includes the integration of Microsoft Tunnel with Intune for a seamless and secure connection. Additionally, solutions that don't require a VPN are also available.

### App protection policies for mobile

App protection policies define which apps are allowed and the actions they can take with your organization's data. The choices available in app protection policies enable organizations to tailor the protection to their specific needs. For some, it might not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its app protection policies data protection framework for iOS and Android mobile app management.

The app protection policies data protection framework is organized into three distinct configuration levels, as mentioned earlier in **Step 2**. Each level builds off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN, encrypted, and allows selective wipe operations. For Android devices, this level validates Android device attestation.
- **Enterprise enhanced data protection** (Level 2) introduces app protection policies data leakage prevention mechanisms and minimum OS requirements. This is the configuration that's applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and app protection policies Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](../apps/app-protection-framework.md).

Next, you create a **Level 3** app protection policy for Microsoft Edge from Microsoft Intune admin center.

To create the app protection policy, follow these steps:

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **Protection** > **Create**.

2. Select **Create policy** > **Android** or **iOS/iPadOS**. Next, enter the following information:

    - **Name**: Level 3 secure enterprise browser.
    - **Description**: The following is a Level 3 app protection policy framework.

3.  **Selected apps** > **public apps**. Find **Microsoft Edge**.

4. Select **Data Protection** and configure the **settings** based on the following table:

    |     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
    |---|---|---|---|---|
    |     Data Transfer    |     Transfer   telecommunication data to    |     Any policy-managed   dialer app    |     Android    |     3    |
    |     Data Transfer    |     Transfer   telecommunication data to    |     A specific dialer app    |     iOS/iPadOS    |     3    |
    |     Data Transfer    |     Dialer App URL Scheme    |     replace_with_dialer_app_url_scheme    |     iOS/iPadOS    |     3    |
    |     Data transfer    |     Receive data from   other apps    |     Policy managed apps    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Open data into Org   documents    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Allow users to open   data from selected services    |     OneDrive,   SharePoint, Camera, Photo Library    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Third-party keyboards    |     Block    |     iOS/iPadOS    |     3    |
    |     Data transfer    |     Approved keyboards    |     Require    |     Android    |     3    |
    |     Data transfer    |     Select keyboards to   approve    |     add/remove keyboards    |     Android    |     3    |
    |     Data Transfer    |     Back up org data to…    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Send org data to other   apps    |     Policy managed apps    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Select apps to exempt    |     Default /   skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;    |     iOS/iPadOS    |     3    |
    |     Data Transfer    |     Save copies of org   data    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Allow users to save   copies to selected services    |     OneDrive,   SharePoint Online, Photo Library    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Transfer   telecommunication data to    |     Any dialer app    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Restrict cut, copy,   and paste between apps    |     Policy managed apps   with paste in    |     iOS/iPadOS, Android    |     3    |

5. Review the **Encryption** section **settings** based on the following table:

    |     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
    |---|---|---|---|---|
    |     Encryption    |     Encrypt org data    |     Require    |     iOS/iPadOS, Android    |     3    |

6. Review the **Functionality** section **settings** based on the following table:

    |     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
    |---|---|---|---|---|
    |     Functionality    |     Printing org data    |     Block    |     iOS/iPadOS, Android,   Windows    |     3    |
    |     Functionality    |     Sync app with native   contacts app    |     Allow    |     iOS/iPadOS, Android    |     3    |
    |     Functionality    |     Org data notifications    |     Block Org Data    |     iOS/iPadOS, Android    |     3    |
    |     Functionality    |     Restrict web content   transfer with other apps    |     Microsoft Edge    |     iOS/iPadOS, Android    |     3    |
    |     Functionality    |     Sync policy managed   app data with native apps or add-ins    |     Allow    |     iOS/iPadOS, Android    |     3    |

7. Once you complete all three sections, select **Next**.

8. Review the **Access Requirements** section **settings** based on the following table:

    |     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
    |---|---|---|---|---|
    |     Access requirements    |     Simple PIN    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Select Minimum PIN   length    |     6    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     PIN reset after number   of days    |     Yes    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Require device lock    |     High/Block Access    |     Android    |     3    |
    |     Access requirements    |     Jailbroken/rooted   devices    |     N/A / Wipe data    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Max OS version    |     Format: Major.Minor    |     Android    |     3    |
    |     Access requirements    |     Samsung Knox device   attestation    |     Wipe data    |     Android    |     3    |
    |     Access requirements    |     Back up org data to…    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Allow users to save   copies to selected services    |     OneDrive,   SharePoint Online, Photo Library    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Restrict cut, copy,   and paste between apps    |     Policy managed apps   with paste in    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Save copies of org   data    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Screen capture and   Google Assistant    |     Block    |     Android    |     3    |
    |     Access requirements    |     Select apps to exempt    |     Default /   skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;    |     iOS/iPadOS    |     3    |
    |     Access requirements    |     Send org data to other   apps    |     Policy managed apps    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     App PIN when device   PIN is set    |     Require    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Biometric instead of   PIN for access    |     Allow    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     SafetyNet device   attestation    |     Basic integrity and   certified devices / Block access    |     Android    |     3    |
    |     Access requirements    |     Require threat scan on   apps    |     N/A / Block access    |     Android    |     3    |
    |     Access requirements    |     Require device lock    |     Low/Warn    |     Android    |     3    |
    |     Access requirements    |     Min OS version    |     Format:   Major.MinorExample: 9.0 / Block access    |     Android    |     3    |
    |     Access requirements    |     Min patch version    |     Format: YYYY-MM-DD    |     Android    |     3    |
    |     Access requirements    |     Required SafetyNet   evaluation type    |     Hardware-backed key    |     Android    |     3    |
    |     Access requirements    |     Encrypt org data    |     Require    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Encrypt org data on   enrolled devices    |     Require    |     Android    |     3    |
    |     Access requirements    |     Sync app with native   contacts app    |     Allow    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Restrict web content   transfer with other apps    |     Microsoft Edge    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Org data notifications    |     Block Org Data    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Override biometrics   with PIN after timeout    |     Require    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     PIN for access    |     Require    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     PIN type    |     Numeric    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Recheck the access   requirements after (minutes of inactivity)    |     30    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Select number of   previous PIN values to maintain    |     0    |     Android    |     3    |
    |     Access requirements    |     Timeout (minutes of   activity)    |     720    |     iOS/iPadOS, Android    |     3    |
    |     Access requirements    |     Offline grace period    |     Allow    |     iOS/iPadOS    |     3    |
    |     Access requirements    |     Work or school account   credentials for access    |     Not required    |     iOS/iPadOS, Android    |     3    |

9. Select **Next**.

10. Review the **Conditional Launch** section **settings** based on the following table:

|     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
|---|---|---|---|---|
|     App conditions    |     Max allowed threat   level    |     Secured / Block access    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Max OS version    |     Format:   Major.Minor.Build    |     iOS/iPadOS    |     3    |
|     App conditions    |     Max PIN attempts    |     5 / Reset PIN    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Offline grace period    |     720 / Block access   (minutes)    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Offline grace period    |     90 / Wipe data (days)    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Disabled account    |     N/A / Block access    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Min OS version    |     Format:   Major.Minor.Build    |     iOS/iPadOS    |     3    |
|     App conditions    |     Max PIN attempts    |     5 / Reset PIN    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Offline grace period    |     90 / Wipe data (days)    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Disabled account    |     N/A / Block access    |     iOS/iPadOS, Android    |     3    |
|     App conditions    |     Offline grace period    |     720 / Block access   (minutes)    |     iOS/iPadOS, Android    |     3    |

11. Select **Next** after you've completed the **Conditional launch** step.

12. Review the **Scope Tags** step.
    For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

13. Select **Next**.

14. Review the **Assignments**.

15. Review the policy details in the **Review and Create** step.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business46.png" alt-text="Apps - App protection policies - Review + Create in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business46.png":::

16. Select **Create** and wait until the policy is created.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business47.png" alt-text="Apps - App protection policies - Policy successfully created in Microsoft Intune admin center." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business47.png":::

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-03.png" alt-text="Step 3 to integrate Mobile Threat Defense with Microsoft Edge for Business.":::](mamedge-3-scc.md)

Continue with [Step 3](mamedge-3-scc.md) to integrate Mobile Threat Defense with Microsoft Edge for Business.
