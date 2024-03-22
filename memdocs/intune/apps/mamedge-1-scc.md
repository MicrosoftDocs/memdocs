---
# required metadata

title: Integrate Windows Security Center with Microsoft Edge for Business
titleSuffix:
description: Integrate Windows Security Center with Microsoft Edge for Business.
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

# Integrate Windows Security Center with Microsoft Edge for Business

Mobile Application Management (MAM) threat detection can be integrated with Windows Security Center. This integration provides a client device health assessment to Intune Application Protection Policies (APP) via a service-to-service connector. This assessment supports gating of the flow and access to organizational data on personal unmanaged devices.

The health state includes the following details:

- **User, app, and device identifiers**
- **A predefined health state**
- **The time of last health state update**

Only users enrolled in Mobile Application Management send health state data. If end users want to stop sending data, they can sign out of their organization account in the protected applications. Similarly, administrators can stop data transmission by removing the Windows Security Connector from Microsoft Intune.

#### Intune app protection policies
Intune app protection policies help secure organizational data and ensure the client device is healthy. It also can perform additional client health verification via Windows Security Center. This includes designating the Windows Security Center risk level for allowing end users to access corporate resources and setting up tenant-based connector to Microsoft Intune for Windows Security Center.

- **Apps**: Select the apps you want to target app protection policies. For this feature set, these apps are blocked or selectively wiped based on device risk assessment from your chosen Mobile Threat Defense vendor.

- **Health Checks**: Below *Device conditions* use the drop-down box to select **Max allowed device threat level**.

    :::image type="content" alt-text="Health Check - App protection policy for Windows." source="./media/securing-data-edge-for-business/securing_data_edge_for_business1.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business1.png":::

#### Options for the threat level

You can select one of the following threat level values:

- **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.

- **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.

- **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.

- **High**: This level is the least secure and allows all threat levels, using Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

#### Options for Action

You can select one of the following **Action** options:

- **Block access:** Will prevent the users from performing any activity until they're back in compliance.

- **Wipe data:** Will remove any information stored in the application related to the corporate or user data.

- **Assignments**: Assign the policy to groups of users. The devices used by the group's members are evaluated for access to corporate data on targeted apps via Intune app protection.

> [!IMPORTANT]
> If you create an app protection policy for any protected app, the device's threat level is assessed. Depending on the configuration, devices that do not meet an acceptable level are either blocked or selectively wiped through conditional launch. If blocked, they are prevented from accessing corporate resources until the threat on the device is resolved and reported to Intune by the chosen MTD vendor.

## Mobile Threat Defense Connector

The Microsoft Mobile Threat Defense (MTD) connector is a feature in Microsoft Intune that creates a channel of communication between Intune and your chosen MTD vendor. It integrates data from a Mobile Threat Defense vendor as an information source for device compliance policies and device Conditional Access rules. This information can help protect corporate resources like Exchange and SharePoint by blocking access from compromised mobile devices.

### Configure the MTD Connector

Use the following steps to configure the MTD Connector.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant Administrator** > **Connectors and tokens** > **Mobile Threat Defense**.

    :::image type="content" alt-text="Connectors and tokens - Mobile Threat Defense - Microsoft Intune admin center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business3.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business3.png":::

3. Select **Add** to display the **Add Connector** pane.

4. From the **Select the Mobile Threat Defense connector to setup** dropdown box, select **Windows Security Center**.

    :::image type="content" alt-text="Connectors and tokens - Mobile Threat Defense - Add Connector - Microsoft Intune admin center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business4.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business4.png":::
    
5. >  select **Create** to create the connector.

The connector is now created. It's important to note that the **Connection status** remains **Unavailable** until the first MAM policy arrives to the user or the first MAM user is enrolled to your Intune tenant.

## Next step

[![Step 2 to understand App Protection Policies for Microsoft Edge for Business.](../media/securing-data-edge-for-business/securing_data_edge_for_business_steps-02.png)](mamedge-2-app.md)

Continue with [Step 2](mamedge-2-app.md) to understand App Protection Policies for Microsoft Edge for Business.