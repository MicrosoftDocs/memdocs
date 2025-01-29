---
# required metadata

title: Step 2. Create app protection policies for Microsoft Edge for Business
titleSuffix:
description: Step 2. Create app protection policies for Microsoft Edge for Business.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/26/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 2. Create app protection policies for Microsoft Edge for Business

App protection policies (APP) are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move corporate data, or a set of actions that are prohibited or monitored when the device user is using the app. A managed app is an app that has app protection policies applied to it and is managed by an enterprise management solution, such as Intune.

## App protection policy framework

When configuring app protection policies, there are various settings and options that enable organizations to tailor their data protection to their specific needs. Due to this flexibility, it may not be obvious which combination of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening efforts, Microsoft has introduced a taxonomy for security configurations in Windows, and Intune is using a similar taxonomy for its APP data protection framework for mobile app management.

The APP data protection configuration framework is organized into three distinct configuration scenarios:

1. **Level 1 enterprise basic data protection:** Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

2. **Level 2 enterprise enhanced data protection:** Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

3. **Level 3 enterprise high data protection:** Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely elevated risk (users who oversee sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

### Data Protection Framework deployment methodology
With any deployment of new software, features or settings, Microsoft recommends investing in a ring methodology for testing validation prior to deploying the APP data protection framework. Defining deployment rings is a one-time event (or at least infrequent), but IT should revisit these groups to ensure that the sequencing is still correct.

For more information about Framework Settings, see [App protection framework](..\apps\app-protection-framework.md).

## App protection policy for Microsoft Edge for Business (Windows)

The app protection policies for Windows provide secure and compliant access to work resources on personal computers by using Data Loss Prevention (DLP) controls.

Having gained a comprehensive understanding of the app protection policy framework, you're now prepared to establish your initial app protection policy for Windows. In this instance, you are formulating a app protection policy. As highlighted in this document, the framework allows for the creation of various levels to cater to your specific requirements. The following example may only be applicable to the **Level 3** policy that Microsoft recommends. It's crucial to replicate these steps for each level, ensuring that the values are adjusted in accordance with the recommendations provided. This approach guarantees that each policy level is accurately configured to meet your organization's distinct needs.

### Apply the data protection framework

Use the following steps to apply the data protection framework.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App protection policies** > **Create policy** > **Windows**.

3. On the **Create policy** step, set the following details:

    - **Name**: Levels 3 secure enterprise browser policy
    - **Description**: This policy is a Level 3 App Protection Framework policy for secure enterprise browser.
    - **Platform**: Windows

4. Select **Next** to display the next step.

5. For the **Apps** step, click **Select apps** to display the **Select apps to target** pane.

6. Find and select **Microsoft Edge**.

7. Click **Select** to select the app.

8. Select **Next** to display the next step.

9. Following the recommendation from Level 3, configure this step with the following values:

    - **Receive data from**: No sources
    - **Send org data to**: No destinations
    - **Allow cut, copy, and paste for**: No destination or source
    - **Print org data**: Block

    :::image type="content" alt-text="Apps - App protection policies - Create policy - Data Protection - Microsoft Intune admin center" source="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business11.png":::

10. Select **Next** to continue to the next step.

11. Following the recommendation from Level 3, configure this step with the following values:

    - **Offline grace period**: 720, Block access (minutes)
    - **Offline grace period**: 90, Wipe data (days)
    - **Max OS version**: 10.0.22631.2715, Block access
    - **Max allowed device threat level**: Secured, Block access

    :::image type="content" alt-text="Apps - App protection policies - Create policy - Health Checks - Microsoft Intune admin center" source="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business12.png":::

12. Click **Next** to display the next step.

13. For the **Scope Tags** step, you must select the proper scope tag for your environment and the roles that have access to this policy.

14. For the **Assignments** step, select **Add Group** and select the desired group. 
For this example, select all VPN Users. However, when you assign this policy in a production environment, you should create a new group of users that will best fit users that must adhere to **Level 3** app protection.

15. Click **Next** to continue to the next step.

16. On the **Review + create** step, review each item and ensure the **level 3** configuration is correct. After

17. Click **Next** to create the policy.

You have now created your first MAM for Windows Policy and it should be available within your Intune tenant.

## App protection policy for Microsoft Edge for Business (Mobile)

Incorporate Microsoft Edge for Business into your existing data security and management strategy. By securing the enterprise browser configuration for mobile devices, you can ensure safer and more efficient web browsing experiences.

Microsoft Edge for Business provide benefits for both management and security:

- **Management**: Microsoft Edge for Business is the only mobile browser natively supported by Microsoft Intune with seamless integration. To secure productivity for your organization, App level management allows IT to configure the right balance between data protection and access.
- **Security**: Data protection and leakage prevention are based on Conditional Access and user identities. Microsoft 365 security features extend to Microsoft Edge for Business mobile including Microsoft Entra Conditional Access, and Data Loss Prevention. For organizations utilizing VPN solutions, Microsoft Edge mobile offers support for identity-enlightened per-app VPN. This includes the integration of Microsoft Tunnel with Intune for a seamless and secure connection. Additionally, solutions that don't require a VPN are also available.

### App protection policies for mobile

App protection policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, as mentioned earlier in **Step 2**. Each level builds off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN, encrypted, and allows selective wipe operations. For Android devices, this level validates Android device attestation.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](../apps/app-protection-framework.md).

Next, you create a **Level 3** app protection policy for Microsoft Edge from Microsoft Intune admin center.

To create the app protection policy, follow these steps:

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **App protection policies** > **Create policy**.

2. Select **Create policy** > **Android** or **iOS/iPadOS**. Next, enter the following information:

    - **Name**: Level 3 secure enterprise browser.
    - **Description**: The following is a Level 3 app protection policy framework.

3. Click **Selected apps** > **public apps**. Find **Microsoft Edge**.

4. Select **Data Protection** and configure the **settings** based on the following table:

    |     Setting    |     Setting description    |     Value    |     Platform    |     Level    |
    |---|---|---|---|---|
    |     Data Transfer    |     Transfer   telecommunication data to    |     Any policy-managed   dialer app    |     Android    |     3    |
    |     Data Transfer    |     Transfer   telecommunication data to    |     A specific dialer app    |     iOS/iPadOS    |     3    |
    |     Data Transfer    |     Dialer App URL Scheme    |     replace_with_dialer_app_url_scheme    |     iOS/iPadOS    |     3    |
    |     Data transfer    |     Receive data from   other apps    |     Policy managed apps    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Open data into Org   documents    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Allow users to open   data from selected services    |     OneDrive for Business,   SharePoint, Camera, Photo Library    |     iOS/iPadOS, Android    |     3    |
    |     Data transfer    |     Third-party keyboards    |     Block    |     iOS/iPadOS    |     3    |
    |     Data transfer    |     Approved keyboards    |     Require    |     Android    |     3    |
    |     Data transfer    |     Select keyboards to   approve    |     add/remove keyboards    |     Android    |     3    |
    |     Data Transfer    |     Back up org data to…    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Send org data to other   apps    |     Policy managed apps    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Select apps to exempt    |     Default /   skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;    |     iOS/iPadOS    |     3    |
    |     Data Transfer    |     Save copies of org   data    |     Block    |     iOS/iPadOS, Android    |     3    |
    |     Data Transfer    |     Allow users to save   copies to selected services    |     OneDrive for Business,   SharePoint Online, Photo Library    |     iOS/iPadOS, Android    |     3    |
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
    |     Functionality    |     Sync policy managed   app data with native apps or add ins    |     Allow    |     iOS/iPadOS, Android    |     3    |

7. Once you've completed all three sections, select **Next**.

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
    |     Access requirements    |     Allow users to save   copies to selected services    |     OneDrive for Business,   SharePoint Online, Photo Library    |     iOS/iPadOS, Android    |     3    |
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
    For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

13. Select **Next**.

14. Review the **Assignments**.

15. Review the policy details in the **Review and Create** step.

    :::image type="content" alt-text="Apps  -  App protection policies  -  Review + Create - Microsoft Intune admin center" source="./media/securing-data-edge-for-business/securing-data-edge-for-business46.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business46.png":::

16. Select **Create** and wait until the policy is created.

    :::image type="content" alt-text="Apps - App protection policies - Policy successfully created - Microsoft Intune admin center." source="./media/securing-data-edge-for-business/securing-data-edge-for-business47.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business47.png":::

## Next step

[![Step 3 to integrate Mobile Threat Defense with Microsoft Edge for Business.](./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-03.png)](mamedge-3-scc.md)

Continue with [Step 3](mamedge-3-scc.md) to integrate Mobile Threat Defense with Microsoft Edge for Business.
