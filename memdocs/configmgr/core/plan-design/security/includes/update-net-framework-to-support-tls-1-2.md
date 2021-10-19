---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 09/01/2021
ms.localizationpriority: medium
---

<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### Determine .NET version

First, determine the installed .NET versions. For more information, see [Determine which versions and service pack levels of .NET Framework are installed](/troubleshoot/dotnet/framework/determine-dotnet-versions-service-pack-levels).

### Install .NET updates

Install the .NET updates so you can enable strong cryptography. Some versions of .NET Framework might require updates to enable strong cryptography. Use these guidelines:

- NET Framework 4.6.2 and later supports TLS 1.1 and TLS 1.2. Confirm the registry settings, but no additional changes are required.

  > [!NOTE]
  > Starting in version 2107, Configuration Manager requires Microsoft .NET Framework version 4.6.2 for site servers, specific site systems, clients, and the console.<!--10402814--> If possible in your environment, install the latest version of .NET version 4.8.

- Update NET Framework 4.6 and earlier versions to support TLS 1.1 and TLS 1.2. For more information, see [.NET Framework versions and dependencies](/dotnet/framework/migration-guide/versions-and-dependencies).

- If you're using .NET Framework 4.5.1 or 4.5.2 on Windows 8.1, Windows Server 2012 R2, or Windows Server 2012, it's highly recommended that you install the latest security updates for the .Net Framework 4.5.1 and 4.5.2 to ensure TLS 1.2 can be enabled properly.
  
  For your reference, TLS 1.2 was first introduced into .Net Framework 4.5.1 and 4.5.2 with the following hotfix rollups:
   - For Windows 8.1 and Server 2012 R2: [Hotfix rollup 3099842](https://support.microsoft.com/topic/hotfix-rollup-3099842-for-the-net-framework-4-5-2-and-the-net-framework-4-5-1-on-windows-7b629c7e-bea4-4838-2512-e22e8bad368a)
   - For Windows Server 2012: [Hotfix rollup 3099844](https://support.microsoft.com/topic/hotfix-rollup-3099844-for-the-net-framework-4-5-2-4-5-1-and-4-5-on-windows-ee48ac0d-79be-28f7-563d-e7bd46040dd3) 

### Configure for strong cryptography

Configure .NET Framework to support strong cryptography. Set the `SchUseStrongCrypto` registry setting to `DWORD:00000001`. This value disables the RC4 stream cipher and requires a restart. For more information about this setting, see [Microsoft Security Advisory 296038](/security-updates/SecurityAdvisories/2015/2960358).

Make sure to set the following registry keys on any computer that communicates across the network with a TLS 1.2-enabled system. For example, Configuration Manager clients, remote site system roles not installed on the site server, and the site server itself.

For 32-bit applications that are running on 32-bit OSs and for 64-bit applications that are running on 64-bit OSs, update the following subkey values:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

For 32-bit applications that are running on 64-bit OSs, update the following subkey values:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!NOTE]
> The `SchUseStrongCrypto` setting allows .NET to use TLS 1.1 and TLS 1.2. The `SystemDefaultTlsVersions` setting allows .NET to use the OS configuration. For more information, see [TLS best practices with the .NET Framework](/dotnet/framework/network-programming/tls).
