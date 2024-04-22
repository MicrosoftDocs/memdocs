---
title: State messages
titleSuffix: Configuration Manager
description: Descriptions of state messages in Configuration Manager.
ms.date: 01/11/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# State messages in Configuration Manager

*Applies to: Configuration Manager (current branch)*

State messages contain concise information about conditions on the Configuration Manager client. The state messaging system is used by specific components of Configuration Manager, such as software updates and configuration settings.

Configuration Manager clients send state messages to the fallback status point or the management point to report the current state of operations. You can create reports to view state messages sent by clients.

Each Configuration Manager feature that uses state messages is identified by the topic type of the state message. The state message topic types listed in this article can be used to define the Configuration Manager feature that a state message relates to.

> [!NOTE]
> A state message ID value of zero (`0`) typically indicates that the topic type is in an unknown state.

## Software updates

### 300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Compliant                 |
| 2                | Non-compliant             |

### 301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

| State message ID | State message description                            |
|:-----------------|:-----------------------------------------------------|
| 1                | Installing updates                                   |
| 2                | Waiting for restart                                  |
| 3                | Waiting for another installation to complete         |
| 4                | Successfully installed updates                       |
| 5                | Pending system restart                               |
| 6                | Failed to install the updates                        |
| 7                | Downloading the updates                              |
| 8                | Downloaded updates                                   |
| 9                | Failed to download updates                           |
| 10               | Waiting for the maintenance window before installing |
| 11               | Waiting for orchestration                            |
| 12               | Waiting for superseding update                       |

### 302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Evaluation activated      |
| 2                | Evaluation  succeeded     |
| 3                | Evaluation  failed        |

### 400 STATE_TOPICTYPE_SUM_CI_DETECTION

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Not required              |
| 2                | Not detected              |
| 3                | Detected                  |

### 401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Compliant                 |
| 2                | Non-compliant             |
| 3                | Conflict detected         |
| 4                | Error                     |
| 5                | Unknown                   |
| 6                | Partial compliance        |
| 7                | Compliance not configured |

### 402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

| State message ID | State message description                            |
|:-----------------|:-----------------------------------------------------|
| 1                | Enforcement started                                  |
| 2                | Enforcement waiting for content                      |
| 3                | Waiting for another installation to complete         |
| 4                | Waiting for the maintenance window before installing |
| 5                | Restart required before installing                   |
| 6                | General failure                                      |
| 7                | Pending installation                                 |
| 8                | Installing update                                    |
| 9                | Pending system restart                               |
| 10               | Successfully installed update                        |
| 11               | Failed to install the update                         |
| 12               | Downloading update                                   |
| 13               | Downloaded update                                    |
| 14               | Failed to download the update                        |

### 500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Update isn't required    |
| 2                | Update is required        |
| 3                | Update is installed       |

### 501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

| State message ID | State message description   |
|:-----------------|:----------------------------|
| 1                | Scan is waiting for content |
| 2                | Scan is running             |
| 3                | Scan complete               |
| 4                | Scan is pending retry       |
| 5                | Scan failed                 |
| 6                | Scan completed with errors  |

## Client deployment

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 700 | STATE_TOPICTYPE_RESYNC_STATE_MSG |
| 701 | STATE_TOPICTYPE_SYSTEM_HEARTBEAT |
| 702 | STATE_TOPICTYPE_CKD_UPDATE |
| 801 | STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT |

### 800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

| State message ID | State message description                                                                                     |
|:-----------------|:--------------------------------------------------------------------------------------------------------------|
| 100              | Client deployment started                                                                                     |
| 101              | Waiting for download                                                                                          |
| 102              | Deployment Scheduled                                                                                          |
| 103              | Waiting for the window before deploying                                                                       |
| 104              | Deployment skipped                                                                                            |
| 301              | Unknown client deployment failure                                                                             |
| 302              | Failed to create the ccmsetup service                                                                         |
| 303              | Failed to delete the ccmsetup service                                                                         |
| 304              | Can't install over embedded OS with File-Based Write Filter (FBWF) enabled on the system drive               |
| 305              | Native security mode isn't valid on Windows 2000                                                             |
| 306              | Failed to start ccmsetup download process                                                                     |
| 307              | Non-valid ccmsetup command line                                                                               |
| 308              | Failed to download the file over WINHTTP at address                                                           |
| 309              | Failed to download the files through BITS at address                                                          |
| 310              | Failed to install BITS version                                                                                |
| 311              | Can't verify that prerequisite file is MS signed                                                              |
| 312              | Failed to copy the file because the disk is full                                                              |
| 313              | Client.msi installation failed with MSI error                                                                 |
| 314              | Failed to load ccmsetup.xml manifest file                                                                     |
| 315              | Failed to obtain a client certificate                                                                         |
| 316              | Prerequisite file isn't MS signed                                                                            |
| 317              | Reboot required to continue the installation                                                                  |
| 318              | Can't install the client on the MP because the MP and client versions do not match                           |
| 319              | Operating system or service pack not supported                                                                |
| 320              | Deployment not supported                                                                                      |
| 321              | Bits Missing                                                                                                  |
| 322              | Source folder is unavailable                                                                                  |
| 323              | App-V not supported                                                                                            |
| 324              | Incorrect Site Version                                                                                        |
| 325              | Prerequisite hash mismatch                                                                                    |
| 326              | MDM Deregistration Failed                                                                                     |
| 327              | MDM Registration Detected                                                                                     |
| 328              | Intune Detected                                                                                               |
| 329              | Metered Network Disallowed                                                                                    |
| 400              | Client deployment succeeded                                                                                   |
| 401              | Deployment Succeeded Reboot Required                                                                          |
| 402              | Deployment Succeeded Reboot Succeeded                                                                         |
| 500              | Client assignment started                                                                                     |
| 601              | Unknown client assignment failure                                                                             |
| 602              | The following site code is invalid                                                                            |
| 603              | Failed to assign to MP                                                                                        |
| 604              | Failed to discover default management point                                                                   |
| 605              | Failed to download site signing certificate                                                                   |
| 606              | Failed to auto discover site code                                                                             |
| 607              | Site assignment failed; client version higher than site version                                               |
| 608              | Failed to get Site Version from Active Directory Domain Services and SLP                                      |
| 609              | Failed to get client version                                                                                  |
| 700              | Client assignment succeeded                                                                                   |

### 810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

| State message ID | State message description                   |
|:-----------------|:--------------------------------------------|
| 100              | Enrollment status                           |
| 101              | Enrollment scheduled                        |
| 102              | Enrollment canceled                         |
| 105              | Enrollment started                          |
| 106              | Enrollment succeeded but isn't provisioned |
| 107              | Enrollment succeeded and is provisioned     |
| 108              | Enrollment no active user                   |
| 110              | Enrollment failed                           |

### 820 STATE_TOPICTYPE_CLIENT_WUFB

| State message ID | State message description                 |
|:-----------------|:------------------------------------------|
| 1                | Windows Update for Business client status |

## Content

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 901 | STATE_TOPICTYPE_REMOTE_DP_MONITORING |
| 902 | STATE_TOPICTYPE_PULL_DP_MONITORING |
| 903 | STATE_TOPICTYPE_DP_USAGE |

### 900 STATE_TOPICTYPE_BRANCH_DP

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Disk Space                |

## Client operations

### 1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

| State message ID | State message description                                      |
|:-----------------|:---------------------------------------------------------------|
| 1                | Client is successfully communicating with the management point |
| 2                | Client failed to communicate with the management point         |

### 1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

| State message ID | State message description                                                      |
|:-----------------|:-------------------------------------------------------------------------------|
| 1                | Client successfully retrieved the certificate from the local certificate store |
| 2                | Client failed to retrieve the certificate from the local certificate store     |

### 1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

| State message ID | State message description        |
|:-----------------|:---------------------------------|
| 1                | Client not ready for native mode |
| 2                | Client ready for native mode     |

### 1300 STATE_TOPICTYPE_CLIENT_HEALTH

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Success                   |
| 2                | Not successful            |

## Legacy device client

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 1002 | STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM |
| 1003 | STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL |
| 1004 | STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE |
| 1005 | STATE_TOPICTYPE_DEVICE_CLIENT_WIPE |
| 1006 | STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE |
| 1007 | STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE |
| 1008 | STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE |
| 1009 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK |
| 1010 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE |
| 1011 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET |
| 1012 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE |
| 1013 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM |
| 1014 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS |
| 1015 | STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE |

## Miscellaneous

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 1401 | STATE_TOPICTYPE_STATE_REPORT |
| 1500 | STATE_TOPICTYPE_CAL_TRACK_UT |
| 1502 | STATE_TOPICTYPE_CAL_TRACK_MT |
| 1503 | STATE_TOPICTYPE_CAL_TRACK_ML |

### 1600 STATE_TOPICTYPE_USER_AFFINITY

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | User affinity set         |
| 2                | User affinity removed     |

### 1660 STATE_TOPICTYPE_SENSOR_STATUS

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Sensor off                |
| 2                | Sensor on                 |

## Applications

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 1700 | STATE_TOPICTYPE_APP_CI_SCAN |
| 1701 | STATE_TOPICTYPE_APP_CI_COMPLIANCE |
| 1703 | STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATION |
| 1704 | STATE_TOPICTYPE_APP_CI_LAUNCH |

### 1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

| State message ID | State message description                                     |
|:-----------------|:--------------------------------------------------------------|
| 1000             | Configuration item succeeded                                  |
| 1001             | Configuration item succeeded already installed                |
| 1002             | Configuration item succeeded preflight                        |
| 1003             | Configuration item fast status succeeded                      |
| 2000             | Configuration item in progress                                |
| 2001             | Configuration item in progress waiting for content            |
| 2002             | Configuration item in progress installing                     |
| 2003             | Configuration item in progress waiting reboot                 |
| 2004             | Configuration item in progress waiting for maintenance window |
| 2005             | Configuration item in progress waiting schedule               |
| 2006             | Configuration item in progress downloading dependent content  |
| 2007             | Configuration item in progress installing dependencies        |
| 2008             | Configuration item in progress pending reboot                 |
| 2009             | Configuration item in progress content downloaded             |
| 2010             | Configuration item in progress pending update                 |
| 2011             | Configuration item in progress waiting user reconnect         |
| 2012             | Configuration item in progress waiting for user sign-out      |
| 2013             | Configuration item in progress waiting for user sign-in       |
| 2014             | Configuration item in progress waiting for install            |
| 2015             | Configuration item in progress waiting for retry              |
| 2016             | Configuration item in progress waiting for presentation mode  |
| 2017             | Configuration item in progress waiting for orchestration      |
| 2018             | Configuration item in progress waiting for network            |
| 2019             | Configuration item in progress pending update VE              |
| 2020             | Configuration item in progress updating VE                    |
| 3000             | Configuration item requirements not met                       |
| 3001             | Configuration item requirements not met host not applicable   |
| 4000             | Configuration item unknown                                    |
| 5000             | Configuration item error                                      |
| 5001             | Configuration item error evaluating                           |
| 5002             | Configuration item error installing                           |
| 5003             | Configuration item error retrieving content                   |
| 5004             | Configuration item error installing dependency                |
| 5005             | Configuration item error retrieving content dependency        |
| 5006             | Configuration item error rules conflict                       |
| 5007             | Configuration item error waiting for retry                    |
| 5008             | Configuration item error uninstalling supersedence            |
| 5009             | Configuration item error downloading superseded               |
| 5010             | Configuration item error updating VE                          |
| 5011             | Configuration item error installing license                   |
| 5012             | Configuration item error retrieving allow all trusted apps    |
| 5013             | Configuration item error no licenses available                |
| 5014             | Configuration item error OS not supported                     |
| 6000             | Configuration item launch succeeded                           |
| 6010             | Configuration item launch error                               |
| 6020             | Configuration item launch unknown                             |

## Events

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 1800 | STATE_TOPICTYPE_EVENT_INTRINSIC |
| 1801 | STATE_TOPICTYPE_EVENT_EXTRINSIC |

## Endpoint protection

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 1900 | STATE_TOPICTYPE_EP_AM_INFECTION |
| 1901 | State_Topictype_Ep_Am_Health |
| 1902 | STATE_TOPICTYPE_EP_MALWARE |
| 1950 | STATE_TOPICTYPE_ATP_HEALTH_STATUS |

### 2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

| State message ID | State message description               |
|:-----------------|:----------------------------------------|
| 1                | Endpoint Protection unmanaged           |
| 2                | Endpoint Protection waiting for install |
| 3                | Endpoint Protection managed             |
| 4                | Endpoint Protection installation failed |
| 5                | Endpoint Protection reboot pending      |
| 6                | Endpoint Protection not supported       |
| 7                | Endpoint Protection co-managed          |

### 2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

| State message ID | State message description                             |
|:-----------------|:------------------------------------------------------|
| 1                | Endpoint Protection policy application succeeded      |
| 2                | Endpoint Protection policy application failed         |

### 2003 STATE_TOPICTYPE_CLIENT_ACTION

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Not applicable            |
| 2                | Failed                    |
| 3                | Succeeded                 |

## Wake-up proxy

### 2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

| State message ID | State message description                |
|:-----------------|:-----------------------------------------|
| 1                | Wake-up proxy isn't installed            |
| 2                | Wake-up proxy is waiting for installation |
| 3                | Wake-up proxy is installed                |
| 4                | Wake-up proxy installation failed         |
| 5                | Wake-up proxy is waiting for reboot       |
| 6                | Wake-up proxy isn't supported on this OS |
| 7                | Wake-up proxy server opt-out              |
| 8                | Wake-up proxy uninstall failed            |
| 9                | Wake-up proxy runtime not supported       |

## Mobile device management

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 2200 | STATE_TOPICTYPE_FDM |
| 2201 | STATE_TOPICTYPE_CCM_CERT_BINDING |
| 2202 | STATE_TOPICTYPE_SERVER_STATISTIC |
| 4000 | STATE_TOPICTYPE_MDM_DEVICE_PROPERTY |
| 4002 | STATE_TOPICTYPE_MDM_CLIENT_IDENITITY |
| 4003 | STATE_TOPICTYPE_MDM_APPLICATION_REQUEST |
| 4004 | STATE_TOPICTYPE_MDM_APPLICATION_STATE |
| 4005 | STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION |
| 4006 | STATE_TOPICTYPE_MDM_LICENSE_KEYS |
| 4007 | STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT |
| 4008 | STATE_TOPICTYPE_MDM_ANDROID_COUNT |
| 4009 | STATE_TOPICTYPE_MDM_SLK_STATUS |
| 4010 | STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE |
| 4022 | STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS |
| 4023 | STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC |

### 3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

| State message ID | State message description                     |
|:-----------------|:----------------------------------------------|
| 0                | Windows Push Notification service channel set |

## Resource access

### 5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

| State message ID | State message description      |
|:-----------------|:-------------------------------|
| 1                | Challenge issued               |
| 2                | Challenge issue failed         |
| 3                | Request creation failed        |
| 4                | Request submit failed          |
| 5                | Challenge validation succeeded |
| 6                | Challenge validation failed    |
| 7                | Issue failed                   |
| 8                | Issue pending                  |
| 9                | Issued                         |
| 10               | Response processing failed     |
| 11               | Response pending               |
| 12               | Enrollment succeeded           |
| 13               | Enrollment not needed          |
| 14               | Revoked                        |
| 15               | Removed from collection        |
| 16               | Renew verified                 |
| 17               | Install failed                 |
| 18               | Installed                      |
| 19               | Delete failed                  |
| 20               | Deleted                        |
| 21               | Renewal requested              |

### 5001 STATE_TOPICTYPE_CERTIFICATE_CRP

| State message ID | State message description      |
|:-----------------|:-------------------------------|
| 1                | Challenge issued               |
| 2                | Challenge issue failed         |
| 3                | Request creation failed        |
| 4                | Request submit failed          |
| 5                | Challenge validation succeeded |
| 6                | Challenge validation failed    |
| 7                | Issue failed                   |
| 8                | Issue pending                  |
| 9                | Issued                         |
| 10               | Response processing failed     |
| 11               | Response pending               |
| 12               | Enrollment succeeded           |
| 13               | Enrollment not needed          |
| 14               | Revoked                        |
| 15               | Removed from collection        |
| 16               | Renew verified                 |
| 17               | Install failed                 |
| 18               | Installed                      |
| 19               | Delete failed                  |
| 20               | Deleted                        |
| 21               | Renewal requested              |

### 5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

| State message ID | State message description      |
|:-----------------|:-------------------------------|
| 1                | Status pin set up succeeded     |
| 2                | Status pin set up failed        |
| 3                | Status pin set up not supported |
| 4                | Status pin set up in progress   |

## Remote applications

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 6000 | STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS |
| 6001 | STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS |
| 6002 | STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS |
| 6003 | STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS |
| 6004 | STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT |

## Compliance settings

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 7000 | STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE |

### 7001 STATE_TOPICTYPE_PFX_CERTIFICATE

| State message ID | State message description      |
|:-----------------|:-------------------------------|
| 1                | Challenge issued               |
| 2                | Challenge issue failed         |
| 3                | Request creation failed        |
| 4                | Request submit failed          |
| 5                | Challenge validation succeeded |
| 6                | Challenge validation failed    |
| 7                | Issue failed                   |
| 8                | Issue pending                  |
| 9                | Issued                         |
| 10               | Response processing failed     |
| 11               | Response pending               |
| 12               | Enrollment succeeded           |
| 13               | Enrollment not needed          |
| 14               | Revoked                        |
| 15               | Removed from collection        |
| 16               | Renew verified                 |
| 17               | Install failed                 |
| 18               | Installed                      |
| 19               | Delete failed                  |
| 20               | Deleted                        |
| 21               | Renewal requested              |

### 7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

| State message ID | State message description     |
|:-----------------|:------------------------------|
| 1                | Compliance success            |
| 2                | Compliance fail at MP         |
| 3                | Compliance fail at the client |
| 4                | Compliance fail at Intune     |
| 5                | Compliance fail at Microsoft Entra ID   |
| 6                | Compliance comgmt Intune      |

## Peer caching

### 7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

| State message ID | State message description |
|:-----------------|:--------------------------|
| 1                | Peer Cache Source added   |
| 2                | Peer Cache Source removed |

### 7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

| State message ID | State message description     |
|:-----------------|:------------------------------|
| 1                | Peer Cache Source deactivated |
| 2                | Peer Cache Source is active   |

### 7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA

| State message ID | State message description      |
|:-----------------|:-------------------------------|
| 1                | Download aggregate data upload |

### 7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

| State message ID | State message description         |
|:-----------------|:----------------------------------|
| 1                | Peer source rejection data upload |

## Proxy

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 7300 | STATE_TOPICTYPE_PROXY_TRAFFIC |
| 7301 | STATE_TOPICTYPE_PROXY_CONNECTION |
| 7302 | STATE_TOPICTYPE_SRS_USAGE_DATA |
| 7303 | STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY |

## Health attestation

### 8001 STATE_TOPICTYPE_HAS_REPORT

| State message ID | State message description           |
|:-----------------|:------------------------------------|
| 1                | Health attestation is supported     |
| 2                | Health attestation isn't supported |

## Client actions

The following topic types have no state IDs:

| Topic type | Description |
|:--|:--|
| 8002 | STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG |
| 8003 | STATE_TOPICTYPE_ENABLE_LOSTMODE |
| 8004 | STATE_TOPICTYPE_DISABLE_LOSTMODE |
| 8005 | STATE_TOPICTYPE_LOCATE_DEVICE |
| 8006 | STATE_TOPICTYPE_REBOOT_DEVICE |
| 8007 | STATE_TOPICTYPE_LOGOUTUSER |
| 8008 | STATE_TOPICTYPE_USERSLIST |
| 8009 | STATE_TOPICTYPE_DELETEUSER |
| 8010 | STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA |
| 8011 | STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA |
| 8012 | STATE_TOPICTYPE_SETDEVICENAME |
| 9000 | STATE_TOPICTYPE_BOOK_CI_COMPLIANCE |
| 9001 | STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT |

## Next steps

[Description of state messaging in Configuration Manager](/troubleshoot/mem/configmgr/state-messaging-description)
