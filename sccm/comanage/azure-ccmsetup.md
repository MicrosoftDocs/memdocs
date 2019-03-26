---
title: Azure AD authentication workflow
titleSuffix: Configuration Manager
description: Details of the Configuration Manager client installation process on a Windows 10 device with Azure Active Directory authentication
ms.date: 03/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Azure AD authentication workflow


*Applies to: System Center Configuration Manager (Current Branch)*

This article is a technical reference for the Configuration Manager client installation process on a Windows 10 device that's joined to Azure Active Directory (Azure AD). It details the workflow process for the device authentication and client installation.  
 


## 1. Azure AD token request

A Windows 10 Azure AD domain-joined client uses Azure AD parameters to request a token. The following entries are logged in **ccmsetup.log**:

- Request Azure AD device token:

    ```
    Getting AAD (device) token with: ClientId = 22ed38d9-ba21-4036-be67-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- If it can't get a device token, it requests an Azure AD user token:

    ```
    Getting AAD (user) token with: ClientId = f1f9b14e-55b8-4f17-8c54-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = 649FC29A-ECE3-4A3B-A3C1-680A2F035A6E
    ```

> [!NOTE] 
> If a WPJ certificate isn't found, it doesn't try to request an Azure AD token. This behavior is because the client isn't properly joined to Azure AD.
> 
> The cloud management gateway (CMG) doesn't forward requests from clients with an invalid token.


## 2. Configuration Manager client token request

Once the client has an Azure AD token, it requests a Configuration Manager client (CCM) token. 

The following entries are logged in **ccmsetup.log**:

    ```
    Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
    Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
    ```

### 2.1 CMG gets request

<!--what should be here?--> 

### 2.2 CMG forwards request to CMG connection point

The following entries are logged in **CMGService.log**:

    ```
    RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
    ```

### 2.3 CMG connection point transforms CMG client request to management point client request

The following entries are logged in **SMS_CLOUD_PROXYCONNECTOR.log**:

    ```
    MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms 
    ```

### 2.4 Management point verifies user token in site database 

The following entries are logged in **CCM_STS.log**:

    ```
    Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0aebad80-77d2-4f0a-9639-676ee4764bb7 OnPrem_UserSid:  OnPrem_DeviceSid: 

    Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX	
    ```


## 3. Content location request

Once the client gets a response with the CCM token, it caches and uses it to request site information and content location through the CMG. The following entries are logged in **ccmsetup.log**:

    ```
    Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
    Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
    Appending CCM Token to the header.
    ```


## 4. Client installation

The device downloads the client content and starts the installation.

### Communication validation

- CMG validates client token via CMG, CMG connection point and HTTP(S), and management point database request.
- Client verifies CMG service certificate or management certificate
- PKI for CMG service certificate: Client requires root certificate authority (CA) of the CMG certificate on local store
- Third-party CMG service certificate: Clients automatically validates certificate with root CA published on internet


## Azure AD token request workflow

![Azure AD CCMSetup workflow diagram](media/AADInstallWF.png)  


## Common issues

- Root CA not present
- CRL check enabled: use the **/NoCRLcheck** option in command line, or publish CRL on internet
- WPJ cert not found: client Azure regsitered, not Azure AD joined

Using /NoCRLCheck is only good for ccmsetup bootstrap. For the clients to be fully functional, you need to disable CRL check on that site's client communication page. Otherwise after the security settings are refreshed by location service, the clients stop communicating with the server.

