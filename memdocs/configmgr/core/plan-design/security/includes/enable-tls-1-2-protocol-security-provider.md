---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/04/2021
ms.localizationpriority: medium
---

<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

Usually, protocol usage is controlled at three levels, the operating system level, the framework or platform level, and the application level. TLS 1.2 is enabled by default at the operating system level. Once you ensure that the .NET registry values are set to enable TLS 1.2 and verify the environment is properly utilizing TLS 1.2 on the network, you may want to edit the `SChannel\Protocols` registry key to disable the older, less secure protocols. For more information on disabling TLS 1.0 and 1.1, see [Configuring Schannel protocols in the Windows Registry](/dotnet/framework/network-programming/tls#configuring-schannel-protocols-in-the-windows-registry).
