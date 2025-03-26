---
title: Cloud attach overview
titleSuffix: Configuration Manager
description: Cloud attach for Configuration Manager overview
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: overview
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: high
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Cloud attach your Configuration Manager environment
<!--9251060-->
*Applies to: Configuration Manager (current branch)*

Attaching your Configuration Manager environment to the cloud allows you to continue to modernize and streamline your management solution. Cloud attach allows you to transform your existing environment without having to worry about much disruption or risk. A Configuration Manager environment is considered cloud attached when it uses at least one of the three primary cloud attach features. You can enable these three features in any order you wish, or all at once.

- [Tenant attach](#tenant-attach)
- [Endpoint analytics](#endpoint-analytics)
- [Co-management](#co-management)

## Tenant attach

Tenant attach provides immediate value by having your device records in the cloud and being able to take actions on these devices from the cloud-based console. You can get real-time data from Configuration Manager clients including clients connected from the internet. In addition to device actions, Tenant attach allows you to manage endpoint security for the attached devices from Intune admin center for both Windows Servers and Client devices along with reports on Antivirus status and detected malware.

### Endpoint Security Reports in Intune for Tenant Attached devices:
Starting with Configuration Manager version 2303, you can now opt for Endpoint Security reports in Intune admin center for tenant attached devices.  Once you opt in, Unhealthy endpoints and Active malware operational reports under Endpoint security node in Intune admin center will start showing data from tenant attached devices. Also, Antivirus agent status and Detected malware organizational reports under Microsoft Defender Antivirus in Reports section will show data from tenant attached devices.

:::image type="content" source="../tenant-attach/media/9220597-org-antivirus-agent-status-report.png" alt-text="Screenshot of Antivirus agent status organizational report in Intune admin center." lightbox="../tenant-attach/media/9220597-org-antivirus-agent-status-report.png":::

:::image type="content" source="../tenant-attach/media/9220597-org-detected-malware-report.png" alt-text="Screenshot of detected malware organizational report in Intune admin center." lightbox="../tenant-attach/media/9220597-org-detected-malware-report.png":::

For more information, see [Tenant attach - Create and deploy Antivirus policies from the admin center](../tenant-attach/deploy-antivirus-policy.md).

### Remote Actions:
When you upload your clients to Microsoft Intune admin center, you can take CM Client specific actions like sync machine policy, sync user policy and sync app evaluation cycle. Apart from the actions, some of the features you may want to use include:
- Run PowerShell [scripts](../tenant-attach/scripts.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Install [applications](../tenant-attach/applications.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Query devices with [CMPivot](../tenant-attach/cmpivot-samples-attached.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Display a [timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) of events from the device
View [software updates](../tenant-attach/software-updates.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
View [Bitlocker recovery keys](../tenant-attach/bitlocker-recovery-keys.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)

:::image type="content" source="media/tenant-attach-actions.png" alt-text="Screenshot of remote actions for tenant attached devices in Intune admin center." lightbox="media/tenant-attach-actions.png":::

## Endpoint analytics

Endpoint analytics gives you insights for measuring the quality of the experience you're delivering to your users. Endpoint analytics can help identify policies or hardware issues that may be slowing down devices and help you proactively make improvements before end users generate a help desk ticket. Each of the reports provides scores for your organization's user experience. There are built-in baseline scores for the median of all other organizations, which allows you to compare your scores to a typical enterprise. You'll be given **Insights and recommendations** for improving your organization's user experience and your score. Endpoint analytics includes the following reports:

- [Work from anywhere](../../analytics/work-from-anywhere.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) - The ability for employees to work from anywhere productively is essential in today’s world. This report offers insights into how prepared your workforce is to be productive from anywhere.

:::image type="content" source="../../analytics/media/8668496-work-from-anywhere-score.png" alt-text="Screenshot of endpoint analytics work from anywhere report in Intune admin center." lightbox="../../analytics/media/8668496-work-from-anywhere-score.png":::

- [Startup performance](../../analytics/startup-performance.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) - The startup performance score helps IT get users from power-on to productivity quickly, without lengthy boot and sign-in delays.

:::image type="content" source="../../analytics/media/8529842-startup-performance-metrics.png" alt-text="Screenshot of endpoint analytics startup performance report in Intune admin center." lightbox="../../analytics/media/8529842-startup-performance-metrics.png":::

- [Application reliability](../../analytics/app-reliability.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) - The application reliability report provides insight into potential issues for desktop applications on managed devices.

:::image type="content" source="../../analytics/media/8529842-application-reliability.png" alt-text="Screenshot of endpoint analytics application reliability report in Intune admin center." lightbox="../../analytics/media/8529842-application-reliability.png":::

- [Restart Frequency](../../analytics/restart-frequency.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) – provides insights into restart frequencies within your organization to help you identify problematic devices.

:::image type="content" source="../../analytics/media/restart-frequency-tab.png" alt-text="Screenshot of endpoint analytics restart frequency report in Intune admin center." lightbox="../../analytics/media/restart-frequency-tab.png":::

## Remediations

[Remediations](../../intune-service/fundamentals/remediations.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) - Remediations helps you fix common support issues before end-users notice issues. You can use Remediations to help increase your [User experience score](../../analytics/scores.md#bkmk_per-device)

:::image type="content" source="../../intune-service/fundamentals/media/remediations/remediations-create.png" alt-text="Screenshot of Remediations in Intune admin center." lightbox="../../intune-service/fundamentals/media/remediations/remediations-create.png":::

## Co-management

Co-management transforms your on-premises Configuration Manager environment without having to go through a large migration effort. Co-management helps simplify device management by giving you the ability to manage workloads from the cloud.

:::image type="content" source="media/comanagement-workloads.png" alt-text="Screenshot of comanagement workload tab in cloud attach properties in configuration manager admin console." lightbox="media/comanagement-workloads.png":::

Once you co-manage the devices, you can specify which workloads to move, such as compliance policy to enable Conditional Access. [Conditional Access](../comanage/quickstart-conditional-access.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) combines granular control over organizational data while maintaining a consistent user experience on any device from any location. Enforcing compliance policy from Intune is a critical part of developing your [Zero Trust](/security/zero-trust/) architecture. Additionally, you can Use [Windows Autopilot](/autopilot/overview) with co-management to simplify the complex process of provisioning devices from the cloud.

## <a name="bkmk_cmg"></a> Cloud management gateway (CMG)

[Cloud management gateway (CMG)](../core/clients/manage/cmg/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) is an additional cloud feature that allows you to manage internet-based clients using your established workflows and processes. CMG helps minimize the management traffic from Configuration Manager to clients through your VPN. When you enable CMG, you maintain a connection to your devices wherever they are on the internet. This connection enables you to keep up with your usual software deployments, device configuration, and software updates processes for internet clients without having to make large infrastructure investments.

## Benefits of Cloud Attaching Configuration Manager with Intune:

1. Enhanced Security: Cloud attaching Configuration Manager with Intune brings advanced security features to your organization's device management strategy. With Intune's cloud-powered security capabilities, such as Conditional Access, Microsoft Entra authentication, and threat detection, combined with Configuration Manager's robust endpoint protection, compliance settings, and software updates, you can ensure that your devices are protected against emerging threats and vulnerabilities.

1. Modern Management: By cloud attaching Configuration Manager with Intune, you can unlock the power of modern management for your organization's devices. Intune allows for cloud-based management of Windows, macOS, iOS, and Android devices, providing a unified and consistent management experience across platforms. You can take advantage of modern management features like zero-touch provisioning, remote device management, app deployment, and device enrollment, making it easier to manage devices from anywhere, at any time.

1. Simplified Device Management: Cloud attaching Configuration Manager with Intune enables a simplified and streamlined device management experience. You can leverage the cloud-based Intune console to manage your devices without the need for complex on-premises infrastructure. This results in reduced maintenance efforts, simplified administration, and improved scalability, making it easier to manage devices in large or geographically dispersed organizations.

1. Greater Flexibility and Agility: With Configuration Manager cloud attach, you can leverage the scalability and flexibility of the cloud to adapt to changing business needs. Intune allows you to dynamically assign policies, apps, and settings to devices based on user groups, device location, or other criteria, making it easy to adapt your device management strategy on-the-go. This agility enables your organization to respond to evolving business requirements, such as remote work scenarios or changing compliance regulations, with ease.

1. Comprehensive Device Lifecycle Management: Cloud attaching Configuration Manager with Intune provides end-to-end device lifecycle management. From provisioning to retirement, you can manage the entire device lifecycle seamlessly. Intune enables you to automate device enrollment, configuration, app deployment, compliance settings, and retire devices when they are no longer needed, ensuring efficient device management throughout their lifecycle.

## Next steps

[Enable cloud attach](enable.md)
