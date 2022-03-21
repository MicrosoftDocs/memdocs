---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/04/2021
ms.localizationpriority: medium
---

<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 is enabled by default. Therefore, no change to these keys is needed to enable it. You can make changes under `Protocols` to disable TLS 1.0 and TLS 1.1 after you've followed the rest of the guidance in these articles and you've verified that the environment works when only TLS 1.2 enabled.

Verify the `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols` registry subkey setting, as shown in [Transport layer security (TLS) best practices with the .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).
