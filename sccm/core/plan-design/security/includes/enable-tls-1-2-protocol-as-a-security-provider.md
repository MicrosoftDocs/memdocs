---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.collection: M365-identity-device-management
---

<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 is enabled by default. Therefore, no change to these keys is needed to enable it. You can make changes under `Protocols` to disable TLS 1.0 and TLS 1.1 after you've followed the rest of the guidance in these articles, and you've verified that the environment works when only TLS 1.2 enabled.

Verify the `\SecurityProviders\SCHANNEL\Protocols` registry subkey setting, as shown in [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

