---
title: How to enable Transport Layer Security (TLS) 1.2 on clients 
titleSuffix: Configuration Manager
description: Information about how to enable TLS 1.2 for Configuration Manager clients.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
---

# How to enable TLS 1.2 on clients

*Applies to: Configuration Manager (Current Branch)*

When enabling TLS 1.2 for your Configuration Manager environment, start by ensuring the clients are capable and properly configured to use TLS 1.2 before enabling TLS 1.2 and disabling the older protocols on the site servers and remote site systems. There are three tasks for enabling TLS 1.2 on clients:

- Update Windows and WinHTTP
- Ensure that TLS 1.2 is enabled as a protocol for SChannel at the Operating System level
- Update and configure the .NET Framework to support TLS 1.2

For more information about dependencies for specific Configuration Manager features and scenarios, see [About enabling TLS 1.2](/sccm/core/plan-design/security/enable-tls-1-2).

## <a name="bkmk_winhttp"></a> Update Windows and WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016, and later versions of Windows natively support TLS 1.2 for client-server communications over WinHTTP. 

Earlier versions of Windows, such as Windows 7 or Windows Server 2012, do not enable TLS 1.1 or TLS 1.2 by default for secure communications using WinHTTP. For these earlier versions of Windows, install [Update 3140245](https://support.microsoft.com/help/3140245) to enable the registry value below, which can be set to add TLS 1.1 and TLS 1.2 to the default secure protocols list for WinHTTP. With the patch installed, create the following registry values:

> [!IMPORTANT]
> Enable these settings on all clients running earlier versions of Windows *before* enabling TLS 1.2 and disabling the older protocols on the Configuration Manager servers. Otherwise, you can inadvertently orphan them.

Verify the value of the `DefaultSecureProtocols` registry setting, for example:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

If you change this value, restart the computer.

The example above shows the value of `0xAA0` for the WinHTTP `DefaultSecureProtocols` setting. [KB 3140245: Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/help/3140245) lists the hexidecimal value for each protocol. By default in Windows, this value is `0x0A0` to enable SSL 3.0 and TLS 1.0 for WinHTTP. The above example keeps these defaults, and also enables TLS 1.1 and TLS 1.2 for WinHTTP. This configuration ensures that the change doesn't break any other application that might still rely on SSL 3.0 or TLS 1.0. You can use the value of `0xA00` to only enable TLS 1.1 and TLS 1.2. Configuration Manager supports the most secure protocol that Windows negotiates between both devices.

 If you want to completely disable SSL 3.0 and TLS 1.0, use the SChannel disabled protocols setting in Windows. For more information, see [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="bkmk_protocol"></a> Ensure that TLS 1.2 is enabled as a protocol for SChannel at the Operating System level

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-as-a-security-provider.md)]

## <a name="bkmk_net"></a> Update and configure the .NET Framework to support TLS 1.2

[!INCLUDE [Update .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## Next steps

- [Enable TLS 1.2 on the site servers and remote site systems](/sccm/core/plan-design/security/enable-tls-1-2-server)
- [Common issues when enabling TLS 1.2](/sccm/core/plan-design/security/enable-tls-1-2-troubleshoot)

