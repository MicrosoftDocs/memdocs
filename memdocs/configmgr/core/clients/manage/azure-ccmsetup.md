---
title: Microsoft Entra authentication workflow
titleSuffix: Configuration Manager
description: Details of the Configuration Manager client installation process on a Windows device with Microsoft Entra authentication.
ms.date: 02/16/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: reference
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Microsoft Entra authentication workflow

*Applies to: Configuration Manager (current branch)*

This article is a technical reference for the Configuration Manager client installation and registration process on a Windows device that is joined to Microsoft Entra ID. It details the workflow process for the device authentication.

> [!NOTE]
> Windows clients get a workplace join (WPJ) certificate when they join a Microsoft Entra tenant. If the certificate isn't found, the Configuration Manager client can't request Microsoft Entra tokens. Without a token, the client can't use the Configuration Manager security token service (CCM_STS) communication channel for Microsoft Entra authentication with Configuration Manager site systems.

## Client installation

In this workflow sample, you installed the Configuration Manager client on a Windows device over the internet with the following ccmsetup command-line properties:

`CCMHOSTNAME="CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500" SMSSITECODE="MEM"`

:::image type="content" source="media/azure-ad-auth-ccmsetup.png" alt-text="Workflow diagram of CcmSetup with Microsoft Entra authentication" lightbox="media/azure-ad-auth-ccmsetup.png":::

<a name='1-azure-ad-info-request-from-ccmsetup'></a>

### 1. Microsoft Entra info request from ccmsetup

Clients installed from internet need specific command-line properties to use Microsoft Entra authentication. You can include these properties in the command line for [internet ccmsetup](../../../comanage/how-to-prepare-win10.md#install-the-configuration-manager-client), but they aren't required. When you don't use Microsoft Entra properties, ccmsetup requests the `AADCLIENTAPPID` and `AADRESOURCEURI` properties from the cloud management gateway (CMG). It uses the device's Microsoft Entra TenantID as a reference. If you haven't onboarded the client's TenantID in Configuration Manager, the CMG doesn't give the required properties to ccmsetup to continue client installation.

The following entries are logged in **ccmsetup.log** of the client:

```log
Getting AAD info from CMG 'CMG.CLOUDAPP.NET'
SMS CCM 5.0: Host=CMG.CLOUDAPP.NET, Path=/CCM_Proxy_ServerAuth/AADAuthInfo?TenantID=9aaf466a-3f40-4468-b3cd-f0010f21f05a, Port=443, Protocol=https, CcmTokenAuth=0, Flags=0x1304, Options=0xe0
Created connection on port 443
Enabled SSL revocation check.
```

> [!IMPORTANT]
> During ccmsetup, the device has to validate the CMG server authentication certificate. The root certificate authority (CA) certificate for the CMG server authentication certificate needs to be available on the client for the chain validation. If you use PKI, when the root CA isn't published on the internet, add the root CA certificate to the device's root CAs store.
>
> If the root CA certificate revocation list (CRL) isn't published on internet, add the `/nocrlcheck` parameter in the ccmsetup command line.

<a name='2-azure-ad-token-request'></a>

### 2. Microsoft Entra token request

On a Windows Azure AD domain-joined device, ccmsetup uses the Microsoft Entra properties to request a Microsoft Entra token calling the ADALOperation provider. The following entries are logged in **ccmsetup.log** on the client:

``` Log
Getting AAD (device) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8b, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
```

If the device token request fails, ccmsetup falls back to try requesting a Microsoft Entra user token. If the device can't get either a Microsoft Entra device or user token, ccmsetup doesn't continue.

> [!NOTE]
> If the device has a valid PKI client authentication certificate, ccmsetup always prefers the certificate. In this case, the client installs as a PKI client and doesn't use Microsoft Entra authentication.

``` Log
WAM token request failed. Status 5, Details 'AAD WAM extension error'
Failed to get AAD token..
Unknown error (Error: D0090016; Source: Unknown)
Failed to get AAD token for 'S-1-5-18' from WAM API. Error 0xd0090016
Falling back to get user 'S-1-5-21-1527250992-855612568-2252598708-1604' token for system...
Getting AAD (user) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8, ResourceUrl = https://ConfigMgrService, AccountId = 149FC29A-ECE3-123-A3C1-123456F035A6E
Retrieved AAD token for AAD user 'e8838041-db7a-42d5-b9ae-78813910e4cc'
```

### 3. Configuration Manager client token request

The client uses the Microsoft Entra token to request the Configuration Manager client (CCM) token. Operational communication between ccmsetup and the site uses the CCM token as authorization token (CcmTokenAuth=1).

#### 3.1 Client sends CCM token request to CMG

The following entries are logged in **ccmsetup.log** on the client:

``` Log
Getting CCM Token from STS server 'cmg.cloudapp.net/CCM_PROXY_MutualAuth/72186325152220500'
Getting CCM Token from https://cmg.cloudapp.net/CCM_PROXY_MutualAuth/72186325152220500/CCM_STS
```

#### 3.2 CMG forwards to CMG connection point

The following entries are logged in **CMGService.log** on the CMG VM instance.

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/72057594037937981/CCM_STS  RequestCount: 1  RequestSize: 1974 Bytes  ResponseCount: 1  ResponseSize: 1566 Bytes  AverageElapsedTime: 218 ms~~  $$<CMGService><06-24-2020 15:31:46.376+00><thread=4992 (0x1380)>
```

> [!TIP]
> Configuration Manager synchronizes the **CMGService.log** to the site server logs folder every five minutes as `CMG-<CMGname>-ProxyService_IN_<%>-CMGService.log`.

#### 3.3 CMG connection point transforms CMG client request to management point client request

The following entries are logged in **SMS_CLOUD_PROXYCONNECTOR.log** (verbose mode) of the site system that hosts the CMG connection point role:

``` Log
SMS_CLOUD_PROXYCONNECTOR    Switched to internal URL. Replaced 'https://CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500/CCM_STS' in   'https://CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500/CCM_STS' with 'https://MP.MYCORP.COM/CCM_STS' and got 'https:///MP.MYCORP.COM/CCM_STS~~
```

#### 3.4 Management point verifies user token in site database

The following entries are logged in **CCM_STS.log** of the site system that hosts the management point that handles the client request:

``` Log
ProcessRequest - Start
Incoming request URL: https://MP.MYCORP.COM/CCM_STS
Validated AAD token. TokenType: UDA TenantId: 2ca9a796-a1a6-43ec-88f1-5935b32155c5 UserId: e8838041-db7a-42d5-b9ae-78813910e4cc DeviceId: 8d2b4ff9-0172-4998-9851-b5324303385f OnPrem_UserSid: S-1-5-21-1527250992-855612568-2252598708-1604 OnPrem_DeviceSid:  
TokenType is UDA
Created SCCM token, token type: UDA, hierarchyId: 8ed3174b-e814-41b5-b51c-fb368f0d4003, userId: 23bbbba2-702e-4db4-8fd9-3b4fe3a5175d, deviceId: GUID:13E80CEF-5698-4C63-9ED6-E58FBFF78C38
Issued token
Return token to client
```

### 4. Content location request

Once the client gets the CCM token, it caches and uses it to request site information and content location of ccmsetup.cab. Once the device downloads the client content, it starts the installation. The following entries are logged in **ccmsetup.log** on the client:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '06/25/2020 08:29:35'
ccmsetup: Host=CMG.cloudapp.net, Path=/CCM_Proxy_ServerAuth7981/ccm_system_tokenauth/request, Port=443, Protocol=https, CcmTokenAuth=1, Flags=0x4100, Options=0xe0
Created connection on port 443
Sending location request to 'cmg.cloudapp.net/CCM_PROXY_MutualAuth/72186325152220500' with payload '< Request >
Appending CCM Token to the header.
Received message '<SiteInfoReply SchemaVersion="1.00">  < reply > </SiteInfoReply>'
     ...
Checking the URL 'https://CMG.cloudapp.net/CCM_PROXY_MutualAuth/72186325152220500/CCM_Client/ccmsetup.cab
ccmsetup: Host=CMG.cloudapp.net, Path=/CCM_Proxy_ServerAuth/72057594037937995/CCM_Client
Appending CCM Token to the header.
Found a valid online MP 'https://CMG.cloudapp.net/CCM_PROXY_MutualAuth/72186325152220500
Searching for DP locations from MP(s)...
CCMSETUP bootstrap from Internet: 1
Sending message body '<ContentLocationRequest SchemaVersion="1.00"  BGRVersion="1"> ...
The location 'https://CMG.cloudapp.net/downloadrestservice.svc/getcontentxmlsecure?pid=CS100001&cid=CS100001
     ...
Installing version 5.00.8968.1000 of the client with product code {66653948-0717-4D50-B0B9-ED66FDED2DDB}
Running installation package
Package:     C:\WINDOWS\ccmsetup\{E6F27809-FF66-4BAA-B0FB-E4A154A6A388}\client.msi
```

> [!NOTE]
> If the client finds the content from a content-enabled CMG, ccmsetup downloads the content from the cloud storage. If the latest client version isn't available on the cloud, it downloads the content from the management point via a CMG request.

## Client registration

:::image type="content" source="media/azure-ad-auth-registration.png" alt-text="Workflow diagram of client registration with Microsoft Entra authentication" lightbox="media/azure-ad-auth-registration.png":::

### 1. Configuration Manager client request registration

Once ccmsetup successfully installs the Configuration Manager client, registration initializes. The following entries are logged in **ClientIDManagerStartup.log** of the client:

``` Log
AADJoinStatusTask: Client hasn't been registered yet.
RegEndPoint: Event notification: CCM_RemoteClient_Reassigned
RegEndPoint: Received notification for site assignment change from '<none>' to 'MEM'.
     ...
[RegTask] - Starting registration, attempt 1.
[RegTask] - Client is not registered. Sending registration request for GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139 ...
Registering client using AAD auth.
```

<a name='2-configuration-manager-requests-azure-ad-token-to-register-client'></a>

### 2. Configuration Manager requests Microsoft Entra token to register client

The client requests a new Microsoft Entra token to register using Microsoft Entra authentication. It prefers a device token, but if it's not available, the client falls back to request a Microsoft Entra user token. The following entries are logged in **ADALOperationProvider.log** of the client:

``` Log
Getting AAD (user) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8, ResourceUrl = https://ConfigMgrService, AccountId = 9756a359-f76a-47d5-8662-9a837012fc35
Retrieved AAD token for AAD user 'e8838041-db7a-42d5-b9ae-78813910e4cc'
```

### 3. Registration request

The registration component on the management point handles the client registration process. The client sends a registration message to the **MP_ClientRegistration** endpoint.

#### 3.1 CMG forwards the client registration request to the management point

The following entries are logged in the **MP_RegistrationManager.log** of the site system that hosts the management point that handles the client request:

``` Log  
Registering device using AAD auth: DeviceId='8d2b4ff9-0172-4998-9851-b5324303385f ', TenantId='c8c82542-203c-4df9-9d86-cdd4dae67e0a'
Processing Registration request from Client 'GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139'
```

#### 3.2 Configuration Manager client is registered  

If registration succeeds, the client gets a confirmation message of registration with **Approval 3** for Microsoft Entra ID-based registration. The following entries are logged in **ClientIDManagerStartup.log** of the client:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139. Approval status 3
```

### 4. Configuration Manager client token request

Once the server confirms the client registration, the client processes the reply message. The client then requests and caches a new CCM token. The following entries are logged in **ClientIDManagerStartup.log** of the client:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
     ...
Cached encrypted token for 'S-1-5-18'. Will expire at '08/12/2020 18:55:40'
```

#### 4.1 CMG gets and forwards CCM_Token request to CMG connection point

The following entries are logged in **CMGService.log** of the CMG VM and the site system that hosts the CMG connection point role:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/72057594037937981/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### 4.2 CMG connection point transforms CMG client request to management point client request

The following entries are logged in **SMS_CLOUD_PROXYCONNECTOR.log** of the site system that hosts the CMG connection point role:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### 4.3 Management point verifies user token in site database

The following entries are logged in **CCM_STS.log** of the site system that hosts the management point that handles the client request:

``` Log
ProcessRequest - Start
Incoming request URL: https://MP.MYCORP.COM/CCM_STS
Validated AAD token. TokenType: UDA TenantId: 2ca9a796-a1a6-43ec-88f1-5935b32155c5 UserId: e8838041-db7a-42d5-b9ae-78813910e4cc DeviceId: 8d2b4ff9-0172-4998-9851-b5324303385f OnPrem_UserSid: S-1-5-21-1527250992-855612568-2252598708-1604 OnPrem_DeviceSid:  
TokenType is UDA
Created SCCM token, token type: UDA, hierarchyId: 8ed3174b-e814-41b5-b51c-fb368f0d4003, userId: 23bbbba2-702e-4db4-8fd9-3b4fe3a5175d, deviceId: GUID:13E80CEF-5698-4C63-9ED6-E58FBFF78C38
Issued token
Return token to client
```

The server returns the CCM token to the client for the rest of client-to-site communication.

> [!NOTE]
> During client registration, certificate validation always runs. This process happens even if you're using the Microsoft Entra authentication method to register the client. This behavior is a fallback option, in case Microsoft Entra authentication doesn't succeed.

### CCM token renewal

The CCM token has a lifetime of eight hours. When the client detects the CCM token is expired or close to expiration, it sends a new CCM token request. The CcmMessaging component handles this renewal process. The following entries are logged in **CcmMessaging.log** of the client:

``` Log
Sending remote sync message '{BD03DEED-D09A-4E63-ADAD-596376FFB0DA}' to host 'CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500' endpoint 'MP_PolicyManager'. Flags 0x280, sender account S-1-5-21-1721254763-462695806-1538882281-3289177
    ...
CCM Token for 'S-1-5-8-1721254763-462695806-1538882281-3289177' (12/23/2019 21:47:24) is already expired or close to expire
Getting CCM Token from https://CMG.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72186325152220500/CCM_STS
Cached encrypted token for 'S-1-5-21-1721254763-462695806-1538882281-3289177'. Will expire at '01/10/2020 17:14:54'
    ...
ccmhttp: Host=CMG.CLOUDAPP.NET, Path=/CCM_Proxy_ServerAuth/72186325152220500/ccm_system_tokenauth/request, Port=443, Protocol=https, CcmTokenAuth=1, Flags=0x4200, Options=0x1e0
Target URL scheme is HTTPS: https://CMG.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72186325152220500/ccm_system_tokenauth/request
Appending CCM Token to the header.
     ...
Message '{BD03DEED-D09A-4E63-ADAD-596376FFB0DA}' got reply message '{36EE3A78-8F6E-425F-BF5C-8460E8E56C33}' to endpoint 'dummy'
```

### Common issues

- Root CA not present: Clients need the root CA certificate to validate the CMG server authentication certificate.

- CRL check is enabled: Publish the CRL on the internet. As an alternative, use the `/NoCRLCheck` parameter for ccmsetup. You can also disable the following option: **Clients check the certificate revocation list (CRL) for site systems**. Find this setting on the **Communication Security** tab of the site properties.

- The WPJ certificate isn't found: Make sure the device is Microsoft Entra joined. Use [dsregcmd.exe](/azure/active-directory/devices/troubleshoot-device-dsregcmd). For example, `dsregcmd /status` and look at the **Device State** section.

> [!TIP]
>
> Client communication via CMG, CMG connection point, and management point runs over HTTPS. If you configure the site for enhanced HTTP, you can still configure the management point for HTTP.
>
> - Client verifies the CMG server authentication certificate:
>
>   - PKI certificate: Client requires the root CA of the CMG certificate in its local store.
>   - Third-party certificate: Clients automatically validate a certificate with its root CA published on the internet.
>
> - CMG, CMG connection point, and management point validate Microsoft Entra ID and CCM tokens.
>
> - Communication between CMG connection point and management point is also secured in both ends:
>
>   - CMG connection point uses client auth certificate.
>   - MP uses a PKI certificate for HTTPS configuration, or a self-signed certificate for enhanced HTTP.
