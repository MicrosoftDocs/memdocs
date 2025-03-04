---
# required metadata

title: Network endpoints for China deployments - Microsoft Intune
titleSuffix: 
description: Review China endpoints for Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 12/19/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

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

# China endpoints for Microsoft Intune

This page lists the China endpoints needed for proxy settings in your Intune deployments.

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

- The proxy server must support both **HTTP (80)** and **HTTPS (443)** because Intune clients use both protocols
- For some tasks (like downloading software updates), Intune requires unauthenticated proxy server access to manage.microsoft.com

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.

Managed devices require configurations that let **All Users** access services through firewalls.

For more information about Windows 10 auto-enrollment and device registration for U.S. customers, see [Windows auto enrollment and device registration ](../enrollment/windows-enrollment-create-cname.md#windows-auto-enrollment-and-device-registration).  

The following tables list the ports and services that the Intune client accesses:

|**Endpoint**|**IP address**|
|---------------------|-----------|
|*.manage.microsoftonline.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 <br> 143.64.196.128/25 <br> 40.162.2.128/25 <br> 139.219.250.128/25 <br> 163.228.221.128/25 <br>|

## Intune customer designated endpoints in China

- Azure portal: https:\//portal.azure.cn/
- Microsoft 365: https:\//portal.partner.microsoftonline.cn/
- Intune Company Portal: https:\//portal.manage.microsoftonline.cn/
- Microsoft Intune admin center: https:\//intune.microsoftonline.cn/

## Network requirements for PowerShell scripts and Win32 apps  

If you're using Intune to deploy PowerShell scripts or Win32 apps, you'll also need to grant access to endpoints in which your tenant currently resides.

|Azure Scale Unit (ASU) | Storage name | CDN |
| --- | --- |--- |
|CNPASU01 | sovereignprodimedatapri<br>sovereignprodimedatasec<br>sovereignprodimedatahotfix | sovereignprodimedatapri.azureedge.net<br>sovereignprodimedatasec.azureedge.net<br>sovereignprodimedatahotfix.azureedge.net |

## Partner service endpoints

Intune operated by 21Vianet depends on the following partner service endpoints:

- Azure AD Sync service: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## Next steps

[Learn more about Intune operated by 21Vianet in China](china.md)

