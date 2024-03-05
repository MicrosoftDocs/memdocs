---
# required metadata

title: Understand Microsoft Edge for Business Mobile
titleSuffix:
description: Understand Microsoft Edge for Business Mobile.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:

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

# Microsoft Edge for Business Mobile

Incorporate Microsoft Edge for Business into your existing data security and management strategy. By securing the enterprise browser configuration for mobile devices, you can ensure safer and more efficient web browsing experiences.

**Management**

Microsoft Edge for Business is the only mobile browser natively supported by Microsoft Intune with seamless integration.

To secure productivity for your organization, App level management allows IT to configure the right balance between data protection and access.

**Security**

Data protection and leakage prevention are based on conditional access and user identities.

Microsoft 365 security features extend to Microsoft Edge for Business mobile including Microsoft Entra Conditional Access, and Data Loss Prevention.

For organizations utilizing VPN solutions, Microsoft Edge mobile offers support for identity-enlightened per-app VPN. This includes the integration of Microsoft Tunnel with Intune for a seamless and secure connection. Additionally, solutions that don't require a VPN are also available.

### App protection policies for Mobile

App protection policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, as mentioned earlier in the whitepaper. Each level builds off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN, encrypted, and allows selective wipe operations. For Android devices, this level validates Android device attestation.

- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.

- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](https://docs.microsoft.com/mem/intune/apps/app-protection-framework).

During this example, we'll create a **Level 3** App protection policy for Microsoft Edge from Microsoft Intune admin center.

To create the app protection policy, follow these steps:

1. Go to <https://intune.microsoft.com/> \> select on **Apps**
\> **App protection policies** \> **Create policy.**


:::image type="content" alt-text="Apps - App protection policies - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business30.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business30.png":::

2. Select on **Create policy** \> **Android** or **iOS/iPadOS** \> **Enter information.**

- **Name:** Level 3 secure enterprise browser.

- **Description:** The following is a Level 3 app protection policy framework.


:::image type="content" alt-text="Apps - App protection policies - Create policy - Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business31.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business31.png":::

:::image type="content" alt-text="Apps - App protection policies - Create policy - iOS - Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business32.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business32.png":::

3. Select Selected **apps** > select **public apps** and type **Microsoft Edge.**

:::image type="content" alt-text="Apps - App protection policies - Create policy - Select apps to target - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business33.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business33.png":::

4. Select **Data Protection** and configure the following **settings**.


:::image type="content" alt-text="Apps - App protection policies - Data Transfer iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business34.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business34.png":::

:::image type="content" alt-text="Apps - App protection policies - Data Transfer iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business35.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business35.png":::

5. Review the **Encryption** section.


:::image type="content" alt-text="Apps - App protection policies - Data Encryption Android - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business36.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business36.png":::


:::image type="content" alt-text="Apps - App protection policies - Encryption iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business37.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business37.png":::

6.**. **Review the Functionality**.

:::image type="content" alt-text="Apps - App protection policies - Functionality Android - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business38.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business38.png":::

:::image type="content" alt-text="Apps - App protection policies - Functionality iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business39.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business39.png":::

7.**: Once completed all three sections select **Next.**

8. Review the **Access Requirements.**

:::image type="content" alt-text="Apps - App protection policies - Access Requirements Android Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business40.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business40.png":::

:::image type="content" alt-text="Apps - App protection policies - Access Requirements iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business41.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business41.png":::

9. Select Next** after reviewing both sections.

10. Review the **Conditional Launch**

:::image type="content" alt-text="Apps - App protection policies - Conditional Launch Android - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business42.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business42.png":::

:::image type="content" alt-text="Apps - App protection policies - Conditional Launch iOS - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business43.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business43.png":::


11. Select **Next** after **Conditional launch** is completed.

12. Review the **Scope Tags.**

> [!NOTE]
> Scope tag should match what has been designed before or use the default.

:::image type="content" alt-text="Apps - App protection policies - scope tags - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business44.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business44.png":::

13. Select **Next** Once completed.

14. Review the **Assignments.**

:::image type="content" alt-text="Apps  -  App protection policies  -  Assignments - Microsoft 365 admin center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business45.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business45.png":::

15. Review the last section of **Review and Create.**

:::image type="content" alt-text="Apps  -  App protection policies  -  Review + Create - Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business46.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business46.png":::

16. Select **Create** and wait until the policy is created.

:::image type="content" alt-text="Apps - App protection policies - Policy successfully created - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business47.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business47.png":::
