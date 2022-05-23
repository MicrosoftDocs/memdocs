---
title: include file
description: include file
author: MandiOhlinger
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/14/2022
ms.author: mandia
ms.custom: include file
ms.collection: M365-identity-device-management
---

<!-- This include file is used in the VPN settings lists for all platforms in /configuration. -->

Some Microsoft 365 services, such as Outlook, may not perform well using third party or partner VPNs. If you're using a third party or partner VPN, and experience a latency or performance issue, then remove the VPN.

If removing the VPN resolves the behavior, then you can:

- Work with the third party or partner VPN for possible resolutions. Microsoft doesn't provide technical support for third party or partner VPNs.
- Don't use a VPN with Outlook traffic.
- If you need to use a VPN, then [use a split-tunnel VPN, such as Microsoft Tunnel](../protect/microsoft-tunnel-overview.md). And, allow the Outlook traffic to bypass the VPN.

For more information, go to:

- [Overview: VPN split tunneling for Microsoft 365](/microsoft-365/enterprise/microsoft-365-vpn-split-tunnel)
- [Using third-party network devices or solutions with Microsoft 365](/office365/troubleshoot/miscellaneous/office-365-third-party-network-devices)
- [Alternative ways for security professionals and IT to achieve modern security controls in today’s unique remote work scenarios blog](https://www.microsoft.com/security/blog/2020/03/26/alternative-security-professionals-it-achieve-modern-security-controls-todays-unique-remote-work-scenarios/)
- [Microsoft 365 network connectivity principles](/microsoft-365/enterprise/microsoft-365-network-connectivity-principles)
