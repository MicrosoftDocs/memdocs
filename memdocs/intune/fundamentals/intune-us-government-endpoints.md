---
# required metadata

title: Network endpoints for US government deployments
titleSuffix: Microsoft Intune
description: Review US government endpoints for Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 1/16/2025  
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: srink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# US government endpoints for Microsoft Intune

This page lists the US Government, US Government Community (GCC) High, and Department of Defense (DoD) endpoints needed for proxy settings in your Intune deployments.

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

- The proxy server must support both **HTTP (80)** and **HTTPS (443)** because Intune clients use both protocols
- For some tasks (like downloading software updates), Intune requires unauthenticated proxy server access to manage.microsoft.us

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.

Managed devices require configurations that let **All Users** access services through firewalls.

> [!NOTE]
> The inspection of SSL traffic is not supported on '*.manage.microsoft.us', or 'has.spserv.microsoft.com' endpoint.

For more information about Windows 10 auto-enrollment and device registration for US government customers, see [Set up automatic enrollment for Windows](../enrollment/windows-enroll.md).  

The following tables list the ports and services that the Intune client accesses:

| Endpoint | IP address |
|---------------------|-----------|
|*.manage.microsoft.us | 52.227.99.114 <br> 20.141.108.112 <br> 13.72.17.166 <br> 52.126.185.115 <br> 52.227.211.91 <br> 23.97.10.212 <br> 52.227.29.124 <br> 52.247.174.16 <br> 52.227.29.244 <br> 52.227.208.144 <br> 52.227.1.233 <br> 20.141.104.221 <br> 52.247.134.218 <br> 20.141.78.227 <br> 13.77.236.201 <br> 62.10.86.128/25 <br> 62.10.87.128/25 <br> 20.159.110.0/25 <br> 20.159.111.0/25 <br>|
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## US Government customer designated endpoints

- Azure portal: https:\//portal.azure.us/ 
- Microsoft 365: https:\//portal.office365.us/ 
- Intune Company Portal: https:\//portal.manage.microsoft.us/ 
- Microsoft Intune admin center: https:\//intune.microsoft.us/

## Network requirements for PowerShell scripts and Win32 apps  

If you're using Intune to deploy PowerShell scripts or Win32 apps, you'll also need to grant access to endpoints in which your tenant currently resides.

|Azure Scale Unit (ASU) | Storage name | CDN |
| --- | --- |--- |
|FXPASU01 | sovereignprodimedatapri<br>sovereignprodimedatasec<br>sovereignprodimedatahotfix | sovereignprodimedatapri.azureedge.net<br>sovereignprodimedatasec.azureedge.net<br>sovereignprodimedatahotfix.azureedge.net |

## Microsoft Defender for Endpoint

For more information about configuring Defender for Endpoint connectivity, see [Connectivity Requirements](../protect/mde-security-integration.md#connectivity-requirements).

To support Defender for Endpoint security settings management, allow the following hostnames through your firewall.
For communication between clients and the cloud service:

- \*.dm.microsoft.us - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

  > [!IMPORTANT]
  > SSL Inspection is not supported on endpoints required for Microsoft Defender for Endpoint.

## Partner service endpoints that Intune depends on

- Azure AD Sync service: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Directory Proxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- Azure AD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## Next steps

[Network endpoints for Microsoft Intune](intune-endpoints.md)

