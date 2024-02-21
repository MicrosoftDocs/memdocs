---
title: Configure clients for CMG
titleSuffix: Configuration Manager
description: Understand how to configure clients to use the cloud management gateway (CMG).
ms.date: 02/16/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure clients for cloud management gateway

*Applies to: Configuration Manager (current branch)*

Once the cloud management gateway (CMG) and the supporting site system roles are operational, you may need to make configuration changes on Configuration Manager clients.

Clients that can communicate with the management point automatically get the location of the CMG service on the next location request. The polling cycle for location requests is every 24 hours. If you don't want to wait for the normally scheduled location request, you can force the request. To force the request, restart the SMS Agent Host service (ccmexec.exe) on the computer.

For devices that aren't connected to the internal network, there are several options to configure them with a CMG location. For more information, see [Install off-premises clients using a CMG](#install-off-premises-clients-using-a-cmg).

> [!NOTE]
> By default all clients receive CMG policy. Control this behavior with the client setting, **Enable clients to use a cloud management gateway**. For more information, see [About client settings](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

## Client location

The Configuration Manager client automatically determines whether it's on the intranet or the internet. If the client can contact a domain controller or an on-premises management point, it sets its connection type to **Currently intranet**. Otherwise, it switches to **Currently Internet**, and uses the location of the CMG service to communicate with the site.

> [!NOTE]
> You can force the client to always use the CMG regardless of whether it's on the intranet or internet. This configuration is useful for testing purposes, or for clients that you want to force to always use the CMG. Set the following registry key on the client:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> You can also specify this setting during client installation using the [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) property.
>
> This setting will always apply, even if the client roams into a location where boundary group configurations would otherwise leverage local resources.

To verify that clients have the policy specifying the CMG, open a Windows PowerShell command prompt as an administrator on the client computer, and run the following command:

```powershell
Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}
```

This command displays any internet-based management points the client knows about. While the CMG isn't technically an internet-based management point, clients view it as one.

> [!NOTE]
> To troubleshoot CMG client traffic, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

## Install off-premises clients using a CMG

There are two methods to install the Configuration Manager client on devices that aren't currently connected to your intranet. Both require a local administrator account on the target system.

- The first method is to use a bulk registration token to install the client on a device. For more information on this method, see [Create a bulk registration token](../../deploy/deploy-clients-cmg-token.md#bulk-registration-token).

- For the second method, when you run **ccmsetup.exe**, use the `/mp` parameter to specify the CMG's URL. For more information, see [About client installation parameters and properties](../../deploy/about-client-installation-properties.md#mp). This method requires one of the following conditions:

  - The Configuration Manager site is properly configured to use PKI certificates for client authentication. Additionally, the client systems each have a valid, unique, and trusted client authentication certificate previously issued to them.

  - The systems are Microsoft Entra domain-joined or hybrid Microsoft Entra domain-joined.

## Configure off-premises clients for CMG

You can connect devices to a recently configured CMG where the following conditions are true:

- They already have the Configuration Manager client installed.

- They aren't connected and can't be connected to your intranet.

- They meet one of the following conditions:

  - A valid, unique, and trusted client authentication certificate previously issued to it.

  - Microsoft Entra domain-joined

  - Hybrid Microsoft Entra domain-joined

- You don't want to or can't completely reinstall the existing client.

- You have a method to change a machine registry value and restart the **SMS Agent Host** service using a local administrator account.

To force the connection on these devices, create the **REG_SZ** registry entry `CMGFQDNs` in the key `HKLM\Software\Microsoft\CCM`. Set its value to the URL of the CMG, for example, `https://GraniteFalls.contoso.com`. Then restart the **SMS Agent Host** Windows service on the device.

If the Configuration Manager client doesn't have a current CMG or internet-facing management point set in the registry, it automatically checks the `CMGFQDNs` registry value. This check occurs every 25 hours, when the **SMS Agent Host** service starts, or when it detects a network change. When the client connects to the site and learns of a CMG, it automatically updates this value.

## Next steps

Your CMG is now set up and functional with clients communicating to the site. Next, understand how to monitor the CMG service and clients:
  
> [!div class="nextstepaction"]
> [Monitor CMG](monitor-clients-cloud-management-gateway.md)
