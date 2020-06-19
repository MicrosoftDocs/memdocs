---
title: Endpoint analytics data privacy
titleSuffix: Configuration Manager
description: Data privacy information for troubleshooting Endpoint analytics.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: reference
ms.assetid: 8036825c-1ae5-4bbe-b3be-3c09eabca19f
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW 
---

# <a name="bkmk_privacy"></a> Endpoint analytics data privacy

Endpoint analytics is fully committed to customer data privacy, centering on these tenets:

- **Transparency:** We fully document the Windows diagnostic events. Review them with your company's security and compliance teams. The Windows Diagnostic Data Viewer lets you see diagnostic data sent from a given device. For more information, see [Diagnostic Data Viewer Overview](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Control:** You control the level of diagnostic data to share with Microsoft. Windows 10, version 1709, adds a new policy to limit enhanced diagnostic data to the minimum required by Endpoint analytics.  

- **Security:** Microsoft protects your data with strong security and encryption.  

- **Trust:** Endpoint analytics supports the Microsoft [Privacy Statement](https://privacy.microsoft.com/privacystatement) and [Online Service Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

For more information, see [Windows services where Microsoft is the processor under the GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).

## Data flow

The following illustration shows how required functional data flows from individual devices through our data services, transient storage, and to your tenant. 

[![User experience data flow diagram](media/endpoint-analytics-dataflow.png)](media/endpoint-analytics-dataflow.png#lightbox)

1. An [Intune Service Administrator role](../../../intune/fundamentals/role-based-access-control.md) [starts gathering data](enroll-intune.md#bkmk_onboard).

    - For Intune-managed devices, this step configures the **Intune data collection** policy. By default, this policy is assigned to "All Devices". You can [change the assignment](settings.md#bkmk_set) at any time to a subset of devices or no devices at all.

    - For Configuration Manager-managed devices, enable [Endpoint analytics data collection and enroll devices](enroll-configmgr.md#bkmk_cm_enroll).

1. Devices send required functional data.

    - For Intune and co-managed devices with the assigned policy, devices send require functional data directly to the Microsoft Endpoint Management Service in the Microsoft public cloud where is processed in near real time. For more information, see [Endpoints required for Intune-managed devices](troubleshoot.md#bkmk_endpoints).

    - For Configuration Manager-managed devices, data flows to Microsoft Endpoint Management through the ConfigMgr connector. Devices don't need direct access to the Microsoft public cloud, but the ConfigMgr connector is cloud attached and requires connection to an Intune tenant. Devices send data to the Configuration Manager Server role every 24 hours, and the Configuration Manager connector sends data to the Gateway Service every hour.

1. The Microsoft Endpoint Management service processes data for each device and publishes the results for both individual devices and organizational aggregates in the admin console using MS Graph APIs. The maximum latency end to end is 25 hours and is gated by the time it takes to do the daily processing of insights and recommendations.

> [!Note]  
> When you first setup Endpoint analytics, add new clients to the [Intune data collection policy](settings.md#bkmk_profile), or [enable device upload](../configmgr/tenant-attach/device-sync-actions.md#enable-device-upload) for a new collection, the reports in endpoint analytics portal may not show complete data right away. The data required to compute the startup score for a device is generated during boot time. Depending on power settings and user behavior, it may take weeks after a device has been enrolled to show the startup score on the admin console.

## <a name="bkmk_datacollection"></a> Data collection

Currently, the basic functionality of Endpoint analytics collects information associated with boot performance records that falls into the [identified](../intune/protect/privacy-data-collect.md#identified-data) and [pseudonymized](../intune/protect/privacy-data-collect.md#pseudonymized-data) categories. As we add additional functionality over time, the data collected will vary as needed. The main datapoints currently being collected:

### Identified data

- Hardware inventory information
  - **make:** Device manufacturer
  - **model:** Device model
  - **deviceClass:** The device classification. For example, Desktop, Server, or Mobile.
  - **Country:** The device region setting
- Application inventory, like
  - **name:** Windows
  - **ver:** The version of the current OS.
  
### Pseudonymized data

- Diagnostic, performance, and usage data tied to a user and/or device
  - **logOnId**
  - **bootId:** The system boot ID
  - **coreBootTimeInMilliseconds:** Time for core boot
  - **totalBootTimeInMilliseconds:** Total boot time
  - **updateTimeInMilliseconds:** Time for OS updates to complete
  - **gpLogonDurationInMilliseconds**: Time for Group policies to process
  - **desktopShownDurationInMilliseconds:** Time for desktop (explorer.exe) to be loaded
  - **desktopUsableDurationInMilliseconds:** Time for desktop (explorer.exe) to be usable
  - **topProcesses:** List of processes loaded during boot with name, with cpu usage stats and app details (Name, publisher, version). For example *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Microsoft&reg; Windows&reg; Operating System\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- Device data not tied to a device or user (if this data is tied to a device or user, Intune treats it as identified data)
  - **ID:** Unique device ID used by Windows Update
  - **localId:** A locally defined unique ID for the device. This is not the human-readable device name. Most likely equal to the value stored at HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** Azure Active Directory device ID
  - **orgId:** Unique GUID representing the Microsoft O365 Tenant
  
> [!Important]  
> Our data handling policies are described in the [Microsoft Intune Privacy Statement](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). We only use your customer data to provide you the services you signed up for. As described during the onboarding process, we anonymize and aggregate the scores from all enrolled organizations to keep the **All organizations (median)** baseline up-to-date.

## <a name="bkmk_stop"></a> Stop gathering data

- If you're enrolling Intune managed devices only, delete the [Intune data collection policy](settings.md#bkmk_gen) created during sign-up.

- If you're enrolling devices that are managed by Configuration Manager, you’ll need to do the following steps to disable data upload in Configuration Manager:

   1. In the Configuration Manager console, go to **Administration** > **Cloud Services** > **Co-management**.
   1. Select **CoMgmtSettingsProd** then click **Properties**.
   1. On the **Configure upload** tab, uncheck the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager**.

- Disable Endpoint analytics data collection in Configuration Manager (optional):

   1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
   1. Right-click and select **Properties** then select the **Computer Agent** settings.
   1. Set **Enable Endpoint analytics data collection** to **No**.
   > [!Important]
   > If you have an existing custom client agent setting that's been deployed to your devices, you'll need to update the **Enable Endpoint analytics data collection** option in that custom setting then redeploy it to your machines for it to take effect.

## Resources

For more information about related privacy aspects, see the following articles:

- [Microsoft Intune Privacy Statement](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 and privacy compliance](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Security and privacy at Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)  
- [Confidence in the trusted cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Trust Center](https://www.microsoft.com/trustcenter)  
