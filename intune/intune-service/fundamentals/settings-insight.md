---
title: Settings insight
description: Settings insight provides peer benchmarking information during security baseline configuration, showing when organizations similar to yours use Microsoft's recommended default values.
author: BrenDuns
ms.author: brenduns
ms.date: 02/10/2026
ms.topic: article
ms.reviewer: Lavanya.lakshman
ms.collection:
- M365-identity-device-management
- highpri
---

# Settings insight

Settings insight provides peer benchmarking information during security baseline configuration. When you configure specific security baselines in Intune, you might see light bulb icons next to certain settings. These icons indicate that organizations with similar characteristics to yours—such as industry type and organization size—commonly use Microsoft's recommended default value for that setting.

This article explains what Settings insight shows, where it's available, and how the recommendations are determined.

## Applies to

Settings insight is available for the following security baselines:

- **Microsoft Edge Baseline**
- **Microsoft 365 Apps for Enterprise Security Baseline**

Settings insight isn't currently available for other security baselines, including the Security Baseline for Windows 10 and later or the Microsoft Defender for Endpoint baseline.

## What Settings insight provides

Settings insight offers context about peer behavior, not prescriptive guidance. The feature:

- Shows when similar organizations commonly use Microsoft's recommended default value for a setting
- Appears as light bulb icons next to settings during baseline configuration
- Functions as positive reinforcement when peer behavior aligns with Microsoft's security recommendations
- Doesn't suggest alternative values or configurations

Settings insight is informational. You remain responsible for evaluating each setting against your organization's security requirements, compliance obligations, and operational needs.

## Prerequisites

- **Licensing/Subscriptions**: You must have a Microsoft Intune Plan 1 license to use Settings insight. For more information, see [Licenses available for Microsoft Intune](../fundamentals/licenses.md)
- **Permissions**: Endpoint Security Administrators can create a profile using Baselines.

  To learn more about this Intune built-in role, see [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) and [Built-in role permissions for Intune](../fundamentals/role-based-access-control-reference.md).

## View insights during baseline configuration

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines** to view the list of available baselines.

3. Select **Microsoft Edge Baseline** or **Microsoft 365 Apps for Enterprise Security Baseline**, and then select **Create profile**.

4. On the **Basics** tab, specify the **Name** and **Description** properties.

5. Select **Next** to go to the **Configuration settings** tab.

6. Expand the groups of **Settings** to view individual configuration options. Light bulb icons appear next to settings where peer benchmarking data is available.

    :::image type="content" source="./media/settings-insight/createprofile-settingsinsight.png" alt-text="Settings insight shown while creating a profile" lightbox="./media/settings-insight/createprofile-settingsinsight.png":::

7. Insights are also visible when editing existing baseline profiles.

    :::image type="content" source="./media/settings-insight/editprofile-settingsinsight.png" alt-text="Settings insight shown while editing a profile" lightbox="./media/settings-insight/editprofile-settingsinsight.png":::

## Understanding the recommendations

When you see a light bulb icon, it indicates that organizations similar to yours commonly keep Microsoft's recommended default value for that setting. Settings insight only appears when:

- Sufficient peer data is available from similar organizations
- The peer behavior aligns with Microsoft's default recommendation for the baseline

Settings insight doesn't appear for settings where:

- There isn't enough data from similar organizations to make a reliable comparison
- Peer behavior doesn't align with Microsoft's recommended defaults
- The setting is new or rarely configured

The presence or absence of an insight doesn't indicate the importance of a setting. All settings in security baselines are recommended by Microsoft's security teams regardless of whether peer data is available.

## How recommendations are determined

Settings insight uses machine learning to identify organizations similar to yours and compare their configuration choices.

### Organization clustering

Similar organizations are identified using a K-means clustering model based on attributes such as:

- Industry type
- Organization size
- Other relevant characteristics

Clustering algorithms and key attributes are selected to ensure organizations are grouped appropriately. The model determines the optimal number of clusters at runtime based on clustering performance.

### Recommendation process

For organizations within the same cluster:

1. Healthy organizations are identified based on Endpoint Analytics scores
2. Common setting values used by these organizations are analyzed
3. When most similar organizations use Microsoft's default value for a setting, an insight appears
4. Insights only appear when peer behavior aligns with Microsoft's baseline recommendations (positive reinforcement)

### Privacy and data protection

Settings insight is designed with privacy and security safeguards:

- **No customer data is used** - The model uses aggregated usage data at the organization level only
- **Data is categorical** - Information is converted to categorical formats when possible (for example, Boolean attributes for feature usage, ranges instead of exact values)
- **Aggregation thresholds** - No recommendation appears if the number of similar organizations is below a minimum threshold
- **Minimum adoption requirements** - Settings must be configured by a minimum number of organizations before insights appear
- **Privacy reviews** - All data usage is reviewed and approved for privacy and security compliance
- **Secure storage** - Data is stored with appropriate protection and retention management

These safeguards protect the confidentiality of individual organizations and prevent inference about specific customers.

### Model monitoring

Model execution and performance are actively monitored to ensure quality and reliability:

- Live monitors track execution anomalies and key performance metrics
- Prompt investigation addresses any issues
- Regular maintenance ensures recommendation accuracy

## Next steps

Settings insight provides supplemental peer benchmarking information during baseline configuration. For comprehensive guidance on deploying and managing security baselines, see:

- [Security baselines overview](../protect/security-baselines.md)
- [Create and manage security baseline profiles in Microsoft Intune](../protect/security-baselines-configure.md)
