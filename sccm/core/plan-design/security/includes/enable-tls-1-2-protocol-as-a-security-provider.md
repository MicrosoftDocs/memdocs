---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.collection: M365-identity-device-management
---

## Enable TLS 1.2 protocol as a security provider 

TLS 1.2 is enabled by default. Therefore, no change to these keys is required to enable it. You can make changes under Protocols to disable TLS 1.0 and TLS 1.1 after you have followed the rest of the guidance in this article, and you've verified that the environment works by having only TLS 1.2 enabled.

Verify the `\SecurityProviders\SCHANNEL\Protocols` registry subkey setting, as shown in [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).


