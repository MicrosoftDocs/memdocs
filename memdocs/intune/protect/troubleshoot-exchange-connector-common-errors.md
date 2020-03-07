---
# required metadata

title: Troubleshoot common errors for the Intune Exchange connector
titleSuffix: Microsoft Intune
description: Troubleshoot and resolve common errors for the on-premises Microsoft Intune Exchange Connector 
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:  
# optional metadata

#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Resolve common Errors for the Intune Exchange Connector

This article can help the Intune administrator resolve specific errors and messages about the operation of the Intune Exchange Connector.  

## Configuration failed and returned error code 0x0000001

**Issue**:  
When you try to configure the Microsoft Intune Exchange Connector, you receive the following error message:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

This problem can occur if the Internet proxy settings are misconfigured.

**Resolution**:  
Configure proxy settings:
1. Contact the local network administrator to make sure that the proxy settings are configured correctly. 
2. Use the **Netsh winhttp** command to configure the proxy server and add the required exclusion list. For example:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## Configuration failed and returned error code 0x000000b	

**Issue**:  
When you try to configure the Microsoft Intune Exchange Connector, you receive the following error message:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
This problem can occur if the account that you used to sign in to Intune isn't an Intune Global Administrator account.

**Resolution**:  
Sign in to Intune with an account that is a Global Administrator, or add your account to the Global Admin group. For more information, see [Role-based administration control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Configuration failed and returned error code 0x0000006

**Issue**:  
When you try to configure the Microsoft Intune Exchange Connector, you receive the following error message:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
This error can occur if a proxy server is used to connect to the Internet and is blocking traffic to the Intune Service. To determine whether a proxy is in use, go to **Control Panel** > **Internet Options**, select the **Connection** tab, and then click **LAN Settings**.

**Resolution**:  

- **Option 1** - Remove the proxy settings to allow the computer to connect to the Internet without going through the proxy.  

- **Option 2** - Configure your proxy server to allow communication to the Intune service, as documented in [Intune Exchange Connector requirements](exchange-connector-install.md#intune-exchange-connector-requirements).



## Event 7000 or 7041: Microsoft Intune Exchange Connector Service won't start

**Issue**:  
An iOS device fails to enroll in Intune and generates one of the following error messages:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
This problem can occur if the **WIEC_User** account doesn't have the **Log on as service** user right in the local policy.

**Resolution**:  
On the computer that runs the Intune Exchange Connector, assign the **Log on as a service** user right to the **WIEC_User** service account. If the computer is a node in a cluster, make sure to assign the *Log on as a service* user right to the cluster service account on all nodes in the cluster.  

To assign the **Log on as a service** user right to the **WIEC_User** service account on the computer, follow these steps:

1. Log on to the computer as an administrator or as a member of the Administrators group.
2. Run **secpol.msc** to open the Local Security Policy.
3. Go to **Security settings** > **Local policies**, and then select **User Rights Assignment**.
4. In the right pane, double-click **Log on as a service**.
5. Select **Add User or Group**, add **WIEC_USER** to the policy, and then select **OK** two times.

If the **Log on as a service** user right was assigned to **WIEC_User** but was later removed, contact the domain administrator to determine whether a Group Policy setting is overwriting it.  

## Next steps  

The following article can help resolve specific errors:
- [Resolve common problems for the Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).git 

Seek assistance from support or the Intune community.
- See [Get Support](../fundamentals/get-support.md) to use the Intune Console to help troubleshoot the issue, or to open a support case with Microsoft. 
- Post your issue in the [Microsoft Intune forums](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
