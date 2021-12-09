---
title: How to enable Transport Layer Security (TLS) 1.2 on clients
titleSuffix: Configuration Manager
description: Information about how to enable TLS 1.2 for Configuration Manager clients.
ms.date: 05/04/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# How to enable TLS 1.2 on clients

*Applies to: Configuration Manager (Current Branch)*

When enabling TLS 1.2 for your Configuration Manager environment, start by ensuring the clients are capable and properly configured to use TLS 1.2 before enabling TLS 1.2 and disabling the older protocols on the site servers and remote site systems. There are three tasks for enabling TLS 1.2 on clients:

- Update Windows and WinHTTP
- Ensure that TLS 1.2 is enabled as a protocol for SChannel at the operating system level
- Update and configure the .NET Framework to support TLS 1.2

For more information about dependencies for specific Configuration Manager features and scenarios, see [About enabling TLS 1.2](enable-tls-1-2.md).

## <a name="bkmk_winhttp"></a> Update Windows and WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016, and later versions of Windows natively support TLS 1.2 for client-server communications over WinHTTP. 

Earlier versions of Windows, such as Windows 7 or Windows Server 2012, don't enable TLS 1.1 or TLS 1.2 by default for secure communications using WinHTTP. For these earlier versions of Windows, install [Update 3140245](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392) to enable the registry value below, which can be set to add TLS 1.1 and TLS 1.2 to the default secure protocols list for WinHTTP. With the patch installed, create the following registry values:

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

The example above shows the value of `0xAA0` for the WinHTTP `DefaultSecureProtocols` setting. [Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392) lists the hexadecimal value for each protocol. By default in Windows, this value is `0x0A0` to enable SSL 3.0 and TLS 1.0 for WinHTTP. The above example keeps these defaults, and also enables TLS 1.1 and TLS 1.2 for WinHTTP. This configuration ensures that the change doesn't break any other application that might still rely on SSL 3.0 or TLS 1.0. You can use the value of `0xA00` to only enable TLS 1.1 and TLS 1.2. Configuration Manager supports the most secure protocol that Windows negotiates between both devices.

 If you want to completely disable SSL 3.0 and TLS 1.0, use the SChannel disabled protocols setting in Windows. For more information, see [Restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](/troubleshoot/windows-server/windows-security/restrict-cryptographic-algorithms-protocols-schannel).

## <a name="bkmk_protocol"></a> Ensure that TLS 1.2 is enabled as a protocol for SChannel at the operating system level

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="bkmk_net"></a> Update and configure the .NET Framework to support TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## Next steps

- [Enable TLS 1.2 on the site servers and remote site systems](enable-tls-1-2-server.md)
- [Common issues when enabling TLS 1.2](enable-tls-1-2-troubleshoot.md)
