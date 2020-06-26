---
title: Azure AD authentication workflow
titleSuffix: Configuration Manager
description: Details of the Configuration Manager client installation process on a Windows 10 device with Azure Active Directory authentication
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual


ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Azure AD authentication workflow

*Applies to: Configuration Manager (current branch)*


This article is a technical reference for the Configuration Manager client installation and registration process on a Windows 10 device that is joined to Azure Active Directory (Azure AD). It details the workflow process for the device authentication.

> [!NOTE]
> Windows 10 clients get WPJ certificate when they are joined to an Azure AD Tenant. If the certificate isn't found, the client can not request AAD tokens and thus can not use Security Token Service communication channel (CCM_STS) for AAD authentication with Configuration Manager Site systems.

## Client installation

In this workflow sample, the Configuration Manager client has been installed on a windows 10 device from the internet running next command line:

 ccmsetup command line: `CCMHOSTNAME="CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/981" SMSSITECODE="MEM"`
 
 ![Azure AD CCMSetup workflow diagram](media/AADAuthCCMSetup.png)

### 1. AAD Info request from ccmsetup

Clients installed from internet, need AAD parameters for being able to use the AAD auth capability. This parameters can be included in the command line for [internet ccmsetup](<https://docs.microsoft.com/mem/configmgr/comanage/how-to-prepare-win10#install-the-configuration-manager-client>) but are not longer required (since 1810). When AAD parameters are not supplied, ccmsetup requests the parameters (*AADCLIENTAPPID* and *AADRESOURCEURI*) to the CMG using the device Azure AD TenantID as reference. If Client´s TenantID is not onboarded in Configuration Manager, CMG will not allow ccmsetup to continue client installation.

   ```log
   Getting AAD info from CMG 'CMG.CLOUDAPP.NET'
   SMS CCM 5.0: Host=CMG.CLOUDAPP.NET, Path=/CCM_Proxy_ServerAuth/AADAuthInfo?TenantID=c%c8254%-203c-4%f%-%9d8-%fd4dae67e%0, Port=443, Protocol=https, CcmTokenAuth=0, Flags=0x1304, Options=0xe0
   Created connection on port 443
   Enabled SSL revocation check.
   ```

> [!IMPORTANT]
> During the ccmsetup the device has to validate the CMG Server Auth certificate. The Root CA certificate for the CMG Server Auth certificate needs to be available for the chain validation. When PKI Root CA is not published on internet, add the Root CA certificate under the devices Root CAs Store.  
> If Root CA CRL is neither published on internet, add the /nocrlcheck parameter in the ccmsetup command line.

### 2. Azure AD token request (AAD Token)

On a Windows 10 Azure AD domain-joined device ccmsetup uses the Azure AD parameters to request an AAD token calling the ADALOperation provider. The following entries are logged in **ccmsetup.log**:

   ``` Log
    Getting AAD (device) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8b, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
   ```

If device token has not been enabled for the Web Application Registration (from Azure Active Directory Tenants node on Configuration Manager console), the Device token request fails and ccmsetup falls back to User Azure AD token request. If device is not able to get AAD Token, neither the device or user token, ccmsetup will not continue (unless a valid certificate is found. In this case client is installed as PKI client and not over AAD Auth).

   ``` Log
   WAM token request failed. Status 5, Details 'AAD WAM extension error'
   Failed to get AAD token..
   Unknown error (Error: D0090016; Source: Unknown)
   Failed to get AAD token for 'S-1-5-18' from WAM API. Error 0xd0090016
   Falling back to get user 'S-1-5-21-1527250992-855612568-2252598708-1604' token for system...
   Getting AAD (user) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
   Retrieved AAD token for AAD user 'e8838041-db7a-42d5-b9ae-78813910e4cc'
  ```

### 3. Configuration Manager client token request (CCM Token)

The Azure AD token is only used to request the CCM token. Operational communications between ccmsetup and Site uses the CCM token as authorization token (CcmTokenAuth=1).

#### 3.1 Client sends CCM Token request to CMG

The following entries are logged in **ccmsetup.log** of windows 10 device:

   ``` Log
   Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/981'
   Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/981/CCM_STS
   ```

#### 3.2 CMG forwards to CMG connection point

The following entries are logged in **CMGService.log** on the CMG VM instance.

   ``` Log
   RequestUri: /CCM_PROXY_SERVERAUTH/72057594037937981/CCM_STS  RequestCount: 1  RequestSize: 1974 Bytes  ResponseCount: 1  ResponseSize: 1566 Bytes  AverageElapsedTime: 218 ms~~  $$<CMGService><06-24-2020 15:31:46.376+00><thread=4992 (0x1380)>
   ```

> !Note:
> CMGService.log is synced to Site Server logs folder every 5 minutes as *CMG-<CMGname>-ProxyService_IN_<%>-CMGService.log*).

#### 3.3 CMG connection point transforms CMG client request to management point client request

The following entries are logged in **SMS_CLOUD_PROXYCONNECTOR.log** (verbose mode):

   ``` Log
   SMS_CLOUD_PROXYCONNECTOR    Switched to internal URL. Replaced 'https://CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/981/CCM_STS' in   'https://CMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/981/CCM_STS' with 'https://MP.MYCORP.COM/CCM_STS' and got 'https:///MP.MYCORP.COM/CCM_STS~~
   ```

#### 3.4 Management point verifies user token in site database

The following entries are logged in **CCM_STS.log**:

   ``` Log
   ProcessRequest - Start
   Incoming request URL: https://MP.MYCORP.COM/CCM_STS
   Validated AAD token. TokenType: UDA TenantId: c%c8254%-203c-4%f%-%9d8-%fd4dae67e%0 UserId: e8838041-db7a-42d5-b9ae-78813910e4cc DeviceId: 8d2b4ff9-0172-4998-9851-b5324303385f OnPrem_UserSid: S-1-5-21-1527250992-855612568-2252598708-1604 OnPrem_DeviceSid:  
   TokenType is UDA
   Created SCCM token, token type: UDA, hierarchyId: f%ca6d0%-3%%0-%%c3-bc%%-635ab1%%0%46, userId: 23bbbba2-702e-4db4-8fd9-3b4fe3a5175d, deviceId: GUID:13E80CEF-5698-4C63-9ED6-E58FBFF78C38
   Issued token
   Return token to client
   ```

### 4. Content location request

Once the client gets the CCM token, it caches and uses it to request site information and client bits content location (ccmsetup.cab). Once device downloads the client content,  starts the client installation. The following entries are logged in **ccmsetup.log**:

   ``` Log
   Cached encrypted token for 'S-1-5-18'. Will expire at '06/25/2020 08:29:35'
   ccmsetup: Host=CMG.cloudapp.net, Path=/CCM_Proxy_ServerAuth7981/ccm_system_tokenauth/request, Port=443, Protocol=https, CcmTokenAuth=1, Flags=0x4100, Options=0xe0
   Created connection on port 443
   Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/981' with payload '< Request >
   Appending CCM Token to the header.
   Received message '<SiteInfoReply SchemaVersion="1.00">  < reply > </SiteInfoReply>'
        ...
   Checking the URL 'https://CMG.cloudapp.net/CCM_PROXY_MUTUALAUTH/981/CCM_Client/ccmsetup.cab
   ccmsetup: Host=CMG.cloudapp.net, Path=/CCM_Proxy_ServerAuth/72057594037937995/CCM_Client
   Appending CCM Token to the header.
   Found a valid online MP 'https://CMG.cloudapp.net/CCM_PROXY_MUTUALAUTH/981
   Searching for DP locations from MP(s)...
   CCMSETUP bootstrap from Internet: 1
   Sending message body '<ContentLocationRequest SchemaVersion="1.00"  BGRVersion="1"> ...
   The location 'https://CMG.cloudapp.net/downloadrestservice.svc/getcontentxmlsecure?pid=CS100001&cid=CS100001
        ...
   Installing version 5.00.8968.1000 of the client with product code {66653948-0717-4D50-B0B9-ED66FDED2DDB}
   Running installation package
   Package:     C:\WINDOWS\ccmsetup\{E6F27809-FF66-4BAA-B0FB-E4A154A6A388}\client.msi
   ```

   > !NOTE:
   > If client bit are found in storage account (Cloud DP) ccmsetup will download from Cloud DP. If client bits on latest version are not avaible on the Cloud DP, the bits will be downloaded from the MP via CMG request.

## Client registration

![Azure AD registration workflow diagram](media/AADAuthRegistration.png)  

### 1. Configuration Manager client request registration

Once ccmsetup successfully installs the Configuration Manager Client, registration initializes. The following entries are logged in **ClientIDManagerStartup.log**:

   ``` Log
   AADJoinStatusTask: Client hasn't been registered yet.
   RegEndPoint: Event notification: CCM_RemoteClient_Reassigned
   RegEndPoint: Received notification for site assignment change from '<none>' to 'MEM'.
        ...
   [RegTask] - Starting registration, attempt 1.
   [RegTask] - Client is not registered. Sending registration request for GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139 ...
   Registering client using AAD auth.
   ```

### 2. Configuration Manager request Azure AD token to register client

Client request new AAD token to register the mew client using AAD Auth. Device token is preferred but if not available, client fallback to AAD user token request. The following entries are logged in **ADALOperationProvider.log**:

   ``` Log
   Getting AAD (user) token with: ClientId = 0b7c8ab3-9ea1-4ffa-b2b9-8ffdd944bd8, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
   Retrieved AAD token for AAD user 'e8838041-db7a-42d5-b9ae-78813910e4cc'
   ```

### 3. Registration Request

Registration process is handled by the Registration component on the Management Point. Client will send registration message to the *MP_ClientRegistration* endpoint.

#### 3.1 Registration request is forwarded from Client to MP through CMG

The following entries are logged **MP_RegistrationManager.log**:

   ``` Log  
    Registering device using AAD auth: DeviceId='8d2b4ff9-0172-4998-9851-b5324303385f ', TenantId='c8c82542-203c-4df9-9d86-cdd4dae67e0a'
    Processing Registration request from Client 'GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139'
   ```

#### 3.2 Configuration Manager client is registered  

If registration succeeds, client gets confirmation message of registration with **Approval 3** (AAD auth registration). The following entries are logged in **ClientIDManagerStartup.log**:

   ``` Log
   [RegTask] - Client is registered. Server assigned ClientID is GUID:C66EE0FD-08E7-4B38-B282-7E6954B71139. Approval status 3
   ```

### 4. Configuration Manager client token request

Once server confirms the client registration and reply message processed by the client, a new CCM token is requested and cached. The following entries are logged in **ClientIDManagerStartup.log**:

   ``` Log
   Getting CCM Token from STS server 'MP.MYCORP.COM'
   Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
        ...
   Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
   ```

#### 4.1 CMG gets and forwards CCM_Token request to CMG connection point

The following entries are logged in **CMGService.log**:

   ``` Log
   RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
   ```

#### 4.2 CMG connection point transforms CMG client request to management point client request

The following entries are logged in **SMS_CLOUD_PROXYCONNECTOR.log**:

   ``` Log
   MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
   ```

#### 4.3 Management point verifies user token in site database

The following entries are logged in **CCM_STS.log**:

   ``` Log
   ProcessRequest - Start
   Incoming request URL: https://MP.MYCORP.COM/CCM_STS
   Validated AAD token. TokenType: UDA TenantId: c%c8254%-203c-4%f%-%9d8-%fd4dae67e%0 UserId: e8838041-db7a-42d5-b9ae-78813910e4cc DeviceId: 8d2b4ff9-0172-4998-9851-b5324303385f OnPrem_UserSid: S-1-5-21-1527250992-855612568-2252598708-1604 OnPrem_DeviceSid:  
   TokenType is UDA
   Created SCCM token, token type: UDA, hierarchyId: f%ca6d0%-3%%0-%%c3-bc%%-635ab1%%0%46, userId: 23bbbba2-702e-4db4-8fd9-3b4fe3a5175d, deviceId: GUID:13E80CEF-5698-4C63-9ED6-E58FBFF78C38
   Issued token
   Return token to client
   ```

Token is returend to client for the rest of client to site communications.
   
> [!NOTE]  
> During client registration, certificate validation always runs. This process happens even if you're using the Azure AD authentication method to register the client, as fallback option, in case AAD auth does not succeed.

### CCM Token Renewal

CCM token has a lifetime of 8 hours. When the client detects the CCM token is expired or close to expire, send a new CCM token request. This renewal process is handled by CCMMessagin. The following entries are logged in **CCMessagin.log**

   ``` Log
   Sending remote sync message '{BD03DEED-D09A-4E63-ADAD-596376FFB0DA}' to host 'SALABCMG.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037927939' endpoint 'MP_PolicyManager'. Flags 0x280, sender account S-1-5-21-1721254763-462695806-1538882281-3289177
       ...
   CCM Token for 'S-1-5-8-1721254763-462695806-1538882281-3289177' (12/23/2019 21:47:24) is already expired or close to expire
   Getting CCM Token from https://SALABCMG.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72057594037927939/CCM_STS
   Cached encrypted token for 'S-1-5-21-1721254763-462695806-1538882281-3289177'. Will expire at '01/10/2020 17:14:54'
       ...
   ccmhttp: Host=SALABCMG.CLOUDAPP.NET, Path=/CCM_Proxy_ServerAuth/72057594037927939/ccm_system_tokenauth/request, Port=443, Protocol=https, CcmTokenAuth=1, Flags=0x4200, Options=0x1e0
   Target URL scheme is HTTPS: SALABCMGhttps://.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72057594037927939/ccm_system_tokenauth/request
   Appending CCM Token to the header.
        ...
   Message '{BD03DEED-D09A-4E63-ADAD-596376FFB0DA}' got reply message '{36EE3A78-8F6E-425F-BF5C-8460E8E56C33}' to endpoint 'dummy'
   ```

### Common issues

- Root CA not present: Provide clients with needed Root CA certificate to validate CMG Server Auth certificate.

- CRL check enabled: Publish the CRL on the internet. As a alternative, use the /NoCRLCheck parameter for ccmsetup bootstrap and disable the Client settings option *"Clients check the certificate revocation lsit (CRL) for site systems*" under Site's properties *Communication Security tab*.

- WPJ certificate not found: Ensure device is Azure AD join (you can use [dsregcmd.exe](<https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd>).

- Device token is not enabled and logged on user is not a valid AAD user: Enable Device token for Web Server Application Registration, or log in the device with a valid AAD user.

> [!TIP] **Communication validation**
>
> Client communication via CMG, CMG connection point and MP runs over SSL (eHTTP or HTTPs).
>
> - Client verifies CMG Server Auth certificate:
>
>   - PKI certificate: Client requires root certificate authority (CA) of the CMG certificate on local store.
>   - Third-party certificate: Clients automatically validate a certificate with its root CA published on the internet.
>
> - Site systems (CMG, CMG Connection Point and MP) validates AAD and CCM tokens.
>
> - Communication between CMG connection Point and MP is also secured in both ends.
>
>   - CMG CP uses client auth certificate.
>   - MP uses PKI (HTTPs) or Self signed (eHTTP) certificate.
