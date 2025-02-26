---
title: Token-based authentication for CMG
titleSuffix: Configuration Manager
description: Register a client on the internal network for a unique token or create a bulk registration token for internet-based devices.
ms.date: 02/16/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Token-based authentication for cloud management gateway

*Applies to: Configuration Manager (current branch)*

<!--5686290-->

The cloud management gateway (CMG) supports many types of clients, but even with [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md), these clients require a [client authentication certificate](../manage/cmg/configure-authentication.md#pki-certificate). This certificate requirement can be challenging to provision on internet-based clients that don't often connect to the internal network, aren't able to join Microsoft Entra ID, and don't have a method to install a PKI-issued certificate.

To overcome these challenges, Configuration Manager extends its device support by issuing its own authentication tokens to devices. To take full advantage of this feature, after you update the site, also update clients to the latest version. The complete scenario isn't functional until the client version is also the latest. If necessary, make sure you [promote the new client version to production](../manage/upgrade/test-client-upgrades.md#promote-a-new-client-to-production).

Clients initially register for these tokens using one of the following two methods:

- Internal network

- Bulk registration

The Configuration Manager client together with the management point manage this token, so there's no OS version dependency at client level. This feature is available for any [supported client OS version](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> These methods only support device-centric management scenarios.
>
> Microsoft recommends joining devices to Microsoft Entra ID. Internet-based devices can use Microsoft Entra ID to authenticate with Configuration Manager. It also enables both device and user scenarios whether the device is on the internet or connected to the internal network. For more information, see [Install and register the client using Microsoft Entra identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

Make sure to **Enable clients to use a cloud management gateway** in the **Cloud services** group of client settings. Even with a site token, clients can't communicate with a CMG if client settings don't allow it. For more information, see [About client settings: Cloud services](about-client-settings.md#cloud-services).<!-- MEMDocs #540 -->

## Internal network registration

This method requires the client to first register with the management point on the internal network. Client registration typically happens right after installation. The management point gives the client a unique token that shows it's using a self-signed certificate. When the client roams onto the internet, to communicate with the CMG it pairs its self-signed certificate with the management point-issued token.

This behavior is enabled by default on the Hierarchy.

> [!NOTE]
> With an HTTPS management point, the client needs to first register regardless of internet/intranet management point. The client needs to present a valid PKI-issued certificate, a Microsoft Entra token, or a bulk registration token.

## Bulk registration token

If you can't install and register clients on the internal network, create a bulk registration token. Use this token when the client installs on an internet-based device, and registers through the CMG. The bulk registration token has a short-validity period, and isn't stored on the client or the site. It allows the client to generate a unique token, which paired with its self-signed certificate, lets it authenticate with the CMG.

> [!NOTE]
> Don't confuse bulk registration tokens with those that Configuration Manager issues to individual clients. The bulk registration token enables the client to initially install and communicate with the site. This initial communication is long enough for the site to issue the client its own, unique client authentication token. The client then uses its authentication token for all communication with the site while it's on the internet. Beyond the initial registration, the client doesn't use or store the bulk registration token.

To create a bulk registration token for use during client installation on internet-based devices, complete the following actions:

1. Sign in to the top-level site server in the hierarchy with local administrator privileges.

1. Open a command prompt as an administrator.

1. Run the tool from the `\bin\X64` folder of the Configuration Manager installation directory on the site server: `BulkRegistrationTokenTool.exe`. Create a new token with the `/new` parameter. For example, `BulkRegistrationTokenTool.exe /new`. For more information, see [Bulk registration token tool usage](#bulk-registration-token-tool-usage).

1. Copy the token and save it in a secure location.

1. Install the Configuration Manager client on an internet-based device. Include the client installation parameter: [`/regtoken`](about-client-installation-properties.md#regtoken). The following example command line includes the other required setup parameters and properties:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > For more information on this command line, see [Install and register the client using Microsoft Entra identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). This process is similar, just doesn't use the Microsoft Entra properties.

To verify, review the following log file for a similar entry:<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

To troubleshoot installation, review `%WinDir%\ccmsetup\logs\ccmsetup.log` on the client. After installation, review `%WinDir%\ccm\logs\ClientIDManagerStartup.log`.

On the server, review the following logs:

- [CMG logs](../../plan-design/hierarchy/log-files.md#cloud-management-gateway)
- Management point
  - CCM_STS.log
  - MP_RegistrationManager.log
  - ClientAuth.log

### Bulk registration token tool usage

The `BulkRegistrationTokenTool.exe` tool is in the `\bin\X64` folder of the Configuration Manager installation directory on the site server. Sign in to the site server, and run it as an administrator. It supports the following command-line parameters:

- `/?`
- `/new`
- `/lifetime`

#### `/?`

Display this usage information.

Example: `BulkRegistrationTokenTool.exe /?`

#### `/new`

Create a new bulk registration token.

Example: `BulkRegistrationTokenTool.exe /new`

The tool displays the following information:
  
- A GUID that the site uses to track issued tokens
- The token validity period, which is three days by default.
- The bulk registration token.

The token isn't stored on the client or the site. Make sure to copy the token from the command prompt, and store in a secure location.

#### `/lifetime`

Use with `/new` parameter to specify the token validity period of the token. Specify an integer value in minutes. The default value is 4,320 (three days). The maximum value is 10,080 (seven days).

Example: `BulkRegistrationTokenTool.exe /lifetime 4320`

### Bulk registration token management

You can see previously created bulk registration tokens and their lifetimes in the Configuration Manager console and block their usage if necessary. The site database doesn't, however, store bulk registration tokens.

### Review a bulk registration token

1. In the Configuration Manager console, go to the **Administration** workspace.

2. Expand **Security**, and select the **Certificates** node. The console lists all site-related certificates and bulk registration tokens in the details pane.

3. Select the bulk registration token to review.

You can filter or sort on the **Type** column. Identify specific bulk registration tokens based on their GUID. When you create a bulk registration token, the tool displays the GUID.

### Block a bulk registration token

1. In the Configuration Manager console, go to the **Administration** workspace.

2. Expand **Security**, select the **Certificates** node, and select the bulk registration token to block.

3. On the **Home** tab of the ribbon bar or the right-click context menu, select **Block**. To unblock previously blocked bulk registration tokens, select the **Unblock** action.

## Token Signing

The token the client gets the from Management Point (when registered internally) or when installed using the Bulk token is signed by the *SMS Token Signing Certificate*. 
This is a Self-Signed certificates created by Certificate Manager component using the **SMS Issuing** root certificate. Configuration Manager-issued token includes the reference of the SMS Token Signing Certificate, apart from other auth headers when sending request to the Management Point via Cloud Management Gateway.

While it's not usual the SMS Issuing or the SMS Token Signing Certificate needs to be renewed, There are some uncertaing scenarios that can require the certificate be renewed:
    - Certificate is corrupted
    - SMS issuing certificate is renewed
    - Site Operating system Upgrade -where [SHA-1 hash algorithm](/azure/security/fundamentals/ocsp-sha-1-sunset) was used to sign the certificate.

> [!NOTE]
> If the SMS Token Signing Certificate is renewed, clients using Configuration Manager-issued token wont be able to authenticate till new token, signed with the newer certificate, is provided.


## Token renewal

The client renews its unique, Configuration Manager-issued token once a month, and it's valid for 90 days. A client doesn't need to connect to the internal network to renew its token. As long as the token is still valid, connecting to the site using a CMG is sufficient. If the token isn't renewed within 90 days, the client must directly connect to a management point on an internal network to receive a new token.

> [!NOTE]
> The token will only renew during the startup of the Configuration Manager Client. Therefore, the SMS Agent Host (CCMExec) Service or the client machine must restart at least every 90 days.

You can't renew a bulk registration token. Once a bulk registration token expires, generate a new one for internet-based device registration using a CMG.

## See also

- [Overview of cloud management gateway](../manage/cmg/overview.md)

- [Install and assign Configuration Manager clients using Microsoft Entra ID for authentication](deploy-clients-cmg-azure.md)
