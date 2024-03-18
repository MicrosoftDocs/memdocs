---
# required metadata

title: Use App Protection Policies for Microsoft Edge for Business
titleSuffix:
description: Use App Protection Policies for Microsoft Edge for Business.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
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

# App Protection Policies for Microsoft Edge for Business

App protection policies (APP) are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move corporate data, or a set of actions that are prohibited or monitored when the user is inside the app. A managed app is an app that has app protection policies applied to it and can be managed by Intune.


## App protection policy framework

When configuring App protection policies, there are many various settings and options to enable organizations to tailor the protection to their specific needs. Due to this flexibility, it may not be obvious which combination of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening efforts, Microsoft has introduced a new taxonomy for security configurations in Windows, and Intune is using a similar taxonomy for its APP data protection framework for mobile app management.

The APP data protection configuration framework is organized into three distinct configuration scenarios:

1. **Level 1 enterprise basic data protection**
 Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

2. **Level 2 enterprise enhanced data protection**
    Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

3. **Level 3 enterprise high data protection**
    Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely elevated risk (users who oversee sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

### Data Protection Framework deployment methodology
With any deployment of new software, features or settings, Microsoft recommends investing in a ring methodology for testing validation prior to deploying the APP data protection framework. Defining deployment rings is a one-time event (or at least infrequent), but IT should revisit these groups to ensure that the sequencing is still correct.

For more information about Framework Settings, see [App protection framework](..\apps\app-protection-framework.md).

### App protection policy for Microsoft Edge for Business (Windows)

**App protection policies for Windows**: This feature provides secure and compliant access to work resources on personal computers with Data Loss Prevention (DLP) controls.

Having gained a comprehensive understanding of the app protection policy framework, we're now prepared to establish our initial app protection policy for Windows. In this instance, we'll be formulating a **Level 3** policy. As highlighted in this document, the framework allows for the creation of various levels to cater to our specific requirements. So, the forthcoming example may only be applicable to the **Level 3** policy that we have recommended. It's crucial to replicate these steps for each level, ensuring that the values are adjusted in accordance with the recommendations provided. This approach guarantees that each policy level is accurately configured to meet our distinct needs.

#### Apply the data protection framework

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

    :::image type="content" alt-text="Apps -- App protection policies -- Create policy -- Data Protection -- Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business11.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business11.png":::

10. Select **Next** to continue to the next step.

11. Following the recommendation from Level 3, configure this step with the following values:

    - **Offline grace period**: 720, Block access (minutes)
    - **Offline grace period**: 90, Wipe data (days)
    - **Max OS version**: 10.0.22631.2715, Block access
    - **Max allowed device threat level**: Secured, Block access

    :::image type="content" alt-text="Apps -- App protection policies -- Create policy -- Health Checks -- Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business12.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business12.png":::

12. Click **Next** to display the next step.

13. For the **Scope Tags** step, you must select the proper scope tag for your environment and the roles that have access to the this policy.

14. For the **Assignments** step, select **Add Group** and select the desired group. 
For this example, select all VPN Users. However, when you assign this policy in a production environment, you should create a new group of users that will best fit users that must adhere to **Level 3** app protection.

15. Click **Next** to continue to the next step.

16. On the **Review + create** step, review each item and ensure the **level 3** configuration is correct. After

17. Click **Next** to create the policy.

You have now created your first MAM for Windows Policy and it should be available within your Intune tenant.

:::image type="content" alt-text="Policy Successfully created message - Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business16.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business16.png":::
