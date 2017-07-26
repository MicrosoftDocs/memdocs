---
title: "Monitor clients - Use Windows Analytics with Configuration Manager | Microsoft Docs"
description: "Windows Analytics is a set of solutions that run on Operations Management Suite that allow you do draw valuable insights into the current state of your environment by leveraging the Windows telemetry data that is reported by devices in your environment."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---

# Use Windows Analytics with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) is a set of solutions that run on [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). The solutions allow you to form insight into the current state of your environment. Devices in your environment report Windows telemetry data. This data can be accessed and analyzed through solutions in the [Operations Management Suite web portal](https://mms.microsoft.com). In the case of [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) the data can also be made directly available in the monitoring node of the Configuration Manager console by connecting Upgrade Readiness to Configuration Manager.

The Windows telemetry data used by Windows Analytics is not transferred directly to the Configuration Manager site server. Client computers send Windows telemetry data to the telemetry service. The relevant data is then transferred to Windows Analytics solutions hosted in one of your organization's OMS workspaces. Configuration Manager can then either direct you to relevant data in the web portal with in-context links or directly display data that is part of solutions that you have connected to Configuration Manager. You can also directly query the data from Operation Management Suite web portal.

>[!Important]
>[Configuration Manager diagnostic and usage data](../../plan-design/diagnostics/diagnostics-and-usage-data.md), which is reported to Microsoft from the Configuration Manager site server, is completely separate from Windows Analytics and Windows telemetry.

## Configure Clients to report data to Windows Analytics

In order for client devices to report data to Windows Analytics, devices must be configured with a Commercial ID key associated with the Operations Management Suite workspace that hosts the Windows Analytics Data for your organization. The devices must also be configured to report telemetry at a telemetry level appropriate for the specific solution or solutions that you want to use. 

### Configure Windows Analytics client settings
To configure Windows Analytics, in the Configuration Manager console choose **Administration** > **Client Settings**, double-click **Create Custom Device Client Settings**, and then check **Windows Analytics**.  

After navigating to the **Windows Analytics** settings tab, configure the following:
  -  **Commercial ID**  
The commercial ID key maps information from devices you manage to the OMS workspace that hosts your organization's Windows Analytics data. If you have already configured a commercial ID key for use with Upgrade Readiness, use that ID. If you do not yet have a commercial ID key, see [Generate your commercial ID key]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Telemetry level for Windows 10 devices**   
For information about what is collected by each Windows 10 telemetry level, see  [Configure Windows telemetry in your organization](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Opt in to commercial data collection on Windows 7, 8 and 8.1 devices**   
For information about data collected from these operating systems when you opt-in, see download  the [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) pdf file from Microsoft.

  -  **Configure Internet Explore data collection**  
On devices running Windows 8.1 or earlier, Internet Explorer data collection can allow Upgrade Readiness to detect web application incompatibilities that could prevent a smooth upgrade to Windows 10. Internet Explorer data collection can be enabled on a per internet zone basis. For more information about internet zones, see [About URL Security Zones](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx).

## Use Upgrade Readiness to identify Windows 10 compatibility issues

Upgrade Readiness (formerly Upgrade Analytics) enables you to analyze device readiness and compatibility with Windows 10. This assessment allows for smoother upgrades. After connecting Configuration Manager to Upgrade Readiness, you can access this client upgrade compatibility data directly in the Configuration Manager console. You'll then be able to target devices for upgrade or remediation from the device list.

For more information and details on how to configure and connect to Upgrade Readiness, see [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## Use Windows Analytics to identify gaps in Windows Information Protection Policies

Windows 10 version 1703 and later devices that are configured with a [Windows Information Protection](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) policy report telemetry on applications that access corporate data in your environment but that aren't accounted for in the WIP policy application rules. These are potentially applications that users in your environment need to stay productive but that are being blocked access, so knowledge that they are accessing corporate data can be useful in the maintenance of your Windows Information Protection policies in Configuration Manager. 

This Windows Information Protection data can be accessed using this [Operations Management Suite query](https://go.microsoft.com/fwlink/?linkid=849952).