---
title: State messages
titleSuffix: Configuration Manager
description: Descriptions of state messages in the supported versions of Configuration Manager.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# State messages in Configuration Manager 

*Applies to: Configuration Manager (current branch)*

State messages contain concise information about conditions on the Configuration Manager client. The state messaging system is used by specific components of Configuration Manager, such as software updates and configuration settings.

Configuration Manager clients send state messages to fallback status point or management point site systems to report the current state of operations. You can create reports to view state messages sent by Configuration Manager clients.

Each Configuration Manager feature that uses state messages is identified by the topic type of the state message. The state message topic types listed in this article can be used to define the Configuration Manager feature that a state message relates to.

> [!NOTE]  
> A state message ID value of zero (0) typically indicates topic type is in an unknown state.

## 300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      State Message ID     |  State Message Description |
|:-------------|:------|
| 0 | Compliance state unknown|
| 1 | Compliant | 
| 2 | Non-compliant | 

## 301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       State Message ID     |  State Message Description |
|:-------------|:------|
| 0  | Enforcement state unknown |
| 1  | Installing update(s)        | 
| 2  | Waiting for restart          | 
| 3  | Waiting for another installation to complete         | 
| 4  | Successfully installed update(2)          | 
| 5  | Pending system restart         | 
| 6  | Failed to install the update(s)         | 
| 7  | Downloading the update(s)   | 
| 8  | Downloaded update(s)    | 
| 9  | Failed to download update(s)     | 
| 10 | Waiting for the maintenance window before installing         | 
| 11 | Waiting for orchestration         | 

## 302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     State Message ID     |  State Message Description |
|:-------------|:------|      
| 0 | Evaluation state unknown|                 
| 1 |Evaluation activated      |
| 2 |Evaluation  succeeded      |
| 3 |Evaluation  failed      |


## 400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0 | Detection state unknown|
| 1 | Not required   |
| 2 | Not detected    |
| 3 | Detected   |

## 401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0 | Compliance state unknown|
| 1 |Compliant     |
| 2 |Non-compliant     |
| 3 |Conflict detected    |
| 4 |Error      |
| 5 |Unknown     |
| 6 |Partial compliance   |
| 7 |Compliance not configured    |

## 402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0  | Enforcement state unknown|
| 1  |Enforcement started          |
| 2  |Enforcement waiting for content         |
| 3  | Waiting for another installation to complete        |
| 4  |Waiting for the maintenance window before installing         |
| 5  |Restart required before installing         |
| 6  |General failure        |
| 7  |Pending installation         |
| 8  |Installing update          |
| 9  |Pending system restart        |
| 10 |Successfully installed update         |
| 11 |Failed to install the update        |
| 12 |Downloading update        |
| 13 | Downloaded update        |
| 14 |Failed to download the update        |

## 500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     State Message ID     |  State Message Description |
|:-------------|:------|
|0 |Detection state unknown|
| 1 | Update is not required  |
| 2 | Update is required   |
| 3 | Update is installed  |

## 501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0 |Scan state unknown|
| 1 | Scan is waiting for content   |
| 2 | Scan is running    |
| 3 | Scan complete    |
| 4 | Scan is pending retry   |
| 5 | Scan failed   |
| 6 | Scan completed with errors |

## 700 STATE_TOPICTYPE_RESYNC_STATE_MSG

No State IDs.

## 701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

No State IDs.

## 702 STATE_TOPICTYPE_CKD_UPDATE
 
No State IDs.

## 800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 100 |Client deployment started      |       
| 101 |Waiting for download       |       
| 102 |Deployment Scheduled       |       
| 103 | Waiting for the window before deploying |
| 104 |Deployment skipped       |       
| 301 |Unknown client deployment failure |       
| 302 |Failed to create the ccmsetup service  |       
| 303 |Failed to delete the ccmsetup service |       
| 304 |Cannot install over embedded operating system with File-Based Write Filter (FBWF) enabled on the system drive |       
| 305 |Native security mode is not valid on Windows 2000  |       
| 306 |Failed to start ccmsetup download process  |       
| 307 |Non-valid ccmsetup command line |       
| 308 |Failed to download the file over WINHTTP at address |       
| 309 |Failed to download the files through BITS at address |       
| 310 |Failed to install BITS version |       
| 311 |Can't verify that prerequisite file is MS signed  |       
| 312 |Failed to copy the file because the disk is full |       
| 313 |Client.msi installation failed with MSI error |       
| 314 |Failed to load ccmsetup.xml manifest file |       
| 315 |Failed to obtain a client certificate  |       
| 316 |Prerequisite file is not MS signed |       
| 317 |Reboot required to continue the installation  |       
| 318 |Cannot install the client on the MP because the MP and client versions do not match |       
| 319 |Operating system or service pack not supported  |       
| 320 |Deployment not supported       |       
| 321 |Bits Missing        |       
| 322 |Source folder is unavailable       |       
| 323 |Appv not supported              |       
| 324 |Incorrect Site Version              |       
| 325 |Prerequisite hash mismatch       |       
| 326 |MDM Deregistration Failed      |       
| 327 |MDM Registration Detected      |       
| 328 |Intune Detected       |       
| 329 |Metered Network Disallowed      |       
| 400 |Client deployment succeeded |  
| 401 |Deployment Succeeded Reboot Required     |       
| 402 |Deployment Succeeded Reboot Succeeded     |
| 500 |Client assignment started|
| 601 |Unknown client assignment failure|
| 602 |The following site code is invalid|
| 603 |Failed to assign to MP|
| 604 |Failed to discover default management point|
| 605 |Failed to download site signing certificate|
| 606 |Failed to auto discover site code|
| 607 |Site assignment failed; client version higher than site version|
| 608 |Failed to get Site Version from Active Directory Domain Services and SLP|
| 609 |Failed to get client version|
| 700 |Client assignment succeeded|

## 801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

No State IDs.

## 810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 100 | Enrollment status   |
| 101 | Enrollment scheduled   |
| 102 | Enrollment canceled   |
| 105 | Enrollment started   |
| 106 | Enrollment succeeded but is not provisioned
| 107 | Enrollment succeeded and is provisioned
| 108 | Enrollment no active user   |
| 110 | Enrollment failed   |


## 820  STATE_TOPICTYPE_CLIENT_WUFB

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Windows Update for Business client status| 

## 900 STATE_TOPICTYPE_BRANCH_DP

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Disk Space   | 

## 901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

No State IDs.

## 902 STATE_TOPICTYPE_PULL_DP_MONITORING

No State IDs.

## 903 STATE_TOPICTYPE_DP_USAGE

No State IDs.

## 1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Client is successfully communicating with the management point |
| 2 | Client failed to communicate with the management point |

## 1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Client successfully retrieved the certificate from the local certificate store    |
| 2 |Client failed to retrieve the certificate from the local certificate store |

## 1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

No State IDs.

## 1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

No State IDs.

## 1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

No State IDs.

## 1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

No State IDs.

## 1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

No State IDs.

## 1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

No State IDs.

## 1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

No State IDs.

## 1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

No State IDs.

## 1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

No State IDs.

## 1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

No State IDs.

## 1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

No State IDs.

## 1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

No State IDs.

## 1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

No State IDs.

## 1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

No State IDs.

## 1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Client not ready for native mode  |
| 2 |Client ready for native mode     |


## 1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Success|
| 2 | Not successful |

## 1401 STATE_TOPICTYPE_STATE_REPORT

No State IDs.

## 1500 STATE_TOPICTYPE_CAL_TRACK_UT

No State IDs.

## 1502 STATE_TOPICTYPE_CAL_TRACK_MT

No State IDs.

## 1503 STATE_TOPICTYPE_CAL_TRACK_ML

No State IDs. 

## 1600 STATE_TOPICTYPE_USER_AFFINITY

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |User affinity set       |
| 2 |User affinity removed       |

## 1700 STATE_TOPICTYPE_APP_CI_SCAN

No State IDs.

## 1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

No State IDs.

## 1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1000  |Configuration Item succeeded           |
| 1001 |Configuration Item succeeded already installed         |
| 1002 |Configuration Item succeeded preflight          |
| 1003 |Configuration Item fast status succeeded          |
| 2000 |Configuration Item in progress           |
| 2001 |Configuration Item in progress waiting for content         |
| 2002 |Configuration Item in progress installing          |
| 2003 |Configuration Item in progress waiting reboot         |
| 2004 |Configuration Item in progress waiting for maintenance window        |
| 2005 |Configuration Item in progress waiting schedule         |
| 2006 |Configuration Item in progress downloading dependent content     |
| 2007 |Configuration Item in progress installing dependencies        |
| 2008 |Configuration Item in progress pending reboot         |
| 2009 |Configuration Item in progress content downloaded         |
| 2010 |Configuration Item in progress pending update         |
| 2011 |Configuration Item in progress waiting user reconnect        |
| 2012 |Configuration Item in progress waiting for user sign out         |
| 2013 |Configuration Item in progress waiting for user sign in         |
| 2014 |Configuration Item in progress waiting for install         |
| 2015 |Configuration Item in progress waiting for retry         |
| 2016 |Configuration Item in progress waiting for presmode         |
| 2017 |Configuration Item in progress waiting for orchestration        |
| 2018 |Configuration Item in progress waiting for network         |
| 2019 |Configuration Item in progress pending update VE         |
| 2020 |Configuration Item in progress updating VE         |
| 3000 |Configuration Item requirements not met           |
| 3001 |Configuration Item requirements not met host not applicable        |
| 4000 |Configuration Item unknown           |
| 5000 |Configuration Item error            |
| 5001 |Configuration Item error evaluating          |
| 5002 |Configuration Item error installing          |
| 5003 |Configuration Item error retrieving content         |
| 5004 |Configuration Item error installing dependency         |
| 5005 |Configuration Item error retrieving content dependency        |
| 5006 |Configuration Item error rules conflict          |
| 5007 |Configuration Item error waiting for retry          |
| 5008 |Configuration Item error uninstalling supersedence        |
| 5009 |Configuration Item error downloading superseded         |
| 5010 |Configuration Item error updating VE          |
| 5011 |Configuration Item error installing license         |
| 5012 |Configuration Item error retrieving allow all trusted apps       |
| 5013 |Configuration Item error no licenses available         |
| 5014 |Configuration Item error OS not supported          |
| 6000 |Configuration Item launch succeeded            |
| 6010 |Configuration Item launch error            |
| 6020 |Configuration Item launch unknown|

## 1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

No State IDs.

## 1704 STATE_TOPICTYPE_APP_CI_LAUNCH

No State IDs.

## 1800 STATE_TOPICTYPE_EVENT_INTRINSIC

No State IDs.

## 1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

No State IDs.

## 1900 STATE_TOPICTYPE_EP_AM_INFECTION

No State IDs.

## 1901 State_Topictype_Ep_Am_Health

No State IDs.

## 1902 STATE_TOPICTYPE_EP_MALWARE

No State IDs.

## 1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

No State IDs.

## 2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Endpoint Protection unmanaged   |
| 2 |Endpoint Protection waiting for install  |
| 3 |Endpoint Protection managed   |
| 4 |Endpoint Protection installation failed  |
| 5 |Endpoint Protection reboot pending  |
| 6 |Endpoint Protection not supported   |
| 7 |Endpoint Protection co-managed   |

## 2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0 |Endpoint Protection policy application status unknown    |
| 1 |Endpoint Protection policy application succeeded    |
| 2 |Endpoint Protection policy application failed    |

## 2003 STATE_TOPICTYPE_CLIENT_ACTION

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 0 |  Unknown    |
| 1 |  Active    |
| 2 |  Inactive    |

## 2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Wakeup Proxy is not installed    |
| 2 | Wakeup Proxy is waiting for installation   |
| 3 | Wakeup Proxy is installed    |
| 4 | Wakeup Proxy installation failed   |
| 5 | Wakeup Proxy is waiting for reboot   |
| 6 | Wakeup Proxy is not supported on this OS  |
| 7 | Wakeup Proxy server opt out   |
| 8 | Wakeup Proxy uninstall failed   |
| 9 | Wakeup Proxy runtime not supported   |

## 2200 STATE_TOPICTYPE_FDM

No State IDs.

## 2201 STATE_TOPICTYPE_CCM_CERT_BINDING

No State IDs.

## 2202 STATE_TOPICTYPE_SERVER_STATISTIC

No State IDs.

## 3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     State Message ID     |  State Message Description |
|:-------------|:------|
|0 | Windows Push Notification service channel set|

## 4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

No State IDs.

## 4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

No State IDs.

## 4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

No State IDs.

## 4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

No State IDs.

## 4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

No State IDs.

## 4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

No State IDs.

## 4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

No State IDs.

## 4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

No State IDs.

## 4009 STATE_TOPICTYPE_MDM_SLK_STATUS

No State IDs.

## 4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

No State IDs.

## 4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

No State IDs.

## 4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

No State IDs.

## 5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Challenge issued         |
| 2 |Challenge issue failed        |
| 3 |Request creation failed        |
| 4 |Request submit failed        |
| 5 |Challenge validation succeeded       |
| 6 |Challenge validation failed       |
| 7 |Issue failed         |
| 8 |Issue pending         |
| 9 |Issued          |
| 10 |Response processing failed       |
| 11 |Response pending         |
| 12 |Enrollment succeeded         |
| 13 |Enrollment not needed         |
| 14 |Revoked          |
| 15 |Removed from collection        |
| 16 |Renew verified         |
| 17 |Install failed        |
| 18 |Installed         |
| 19 |Delete failed         |
| 20 |Deleted         |
| 21 |Renewal requested        |


## 5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Challenge issued         |
| 2 |Challenge issue failed        |
| 3 |Request creation failed        |
| 4 |Request submit failed        |
| 5 |Challenge validation succeeded       |
| 6 |Challenge validation failed       |
| 7 |Issue failed         |
| 8 |Issue pending         |
| 9 |Issued          |
| 10 |Response processing failed       |
| 11 |Response pending         |
| 12 |Enrollment succeeded         |
| 13 |Enrollment not needed         |
| 14 |Revoked          |
| 15 |Removed from collection        |
| 16 |Renew verified         |
| 17 |Install failed        |
| 18 |Installed         |
| 19 |Delete failed         |
| 20 |Deleted         |
| 21 |Renewal requested        |

## 5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 | Status pin setup succeeded       |
| 2 | Status pin setup failed       |
| 3 | Status pin setup not supported      |
| 4 | Status pin setup in progress      |

## 6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

No State IDs.

## 6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

No State IDs.

## 6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

No State IDs.

## 6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

No State IDs.

## 6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

No State IDs.

## 7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

No State IDs.

## 7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Challenge issued    |
| 2 |Challenge issue failed   |
| 3 |Request creation failed   |
| 4 |Request submit failed   |
| 5 |Challenge validation succeeded  |
| 6 |Challenge validation failed  |
| 7 |Issue failed    |
| 8 |Issue pending    |
| 9 |Issued     |
| 10 |Response processing failed  |
| 11 |Response pending    |
| 12 |Enrollment succeeded    |
| 13 |Enrollment not needed    |
| 14 |Revoked     |
| 15 |Removed from collection   |
| 16 |Renew verified    |
| 17 |Install failed   |
| 18 |Installed    |
| 19 |Delete failed    |
| 20 |Deleted    |
| 21 |Renewal requested   |

## 7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     State Message ID     |  State Message Description |
|:-------------|:------|
|| 1 | Compliance success    |
| 2 | Compliance fail at mp   |
| 3 | Compliance fail at the client   |
| 4 | Compliance fail at Intune   |
| 5 | Compliance fail at AAD   |
| 6 | Compliance comgmt Intune   |

## 7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Peer Cache Source added       |
| 2 |Peer Cache Source removed      |

## 7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Peer Cache Source deactivated       |
| 2 |Peer Cache Source is active       |

## 7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Download aggregate data upload       |

## 7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Peer source rejection data upload     |

## 7300 STATE_TOPICTYPE_PROXY_TRAFFIC

No State IDs.

## 7301 STATE_TOPICTYPE_PROXY_CONNECTION

No State IDs.

## 7302 STATE_TOPICTYPE_SRS_USAGE_DATA

No State IDs.

## 7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

No State IDs.

## 8001 STATE_TOPICTYPE_HAS_REPORT

|     State Message ID     |  State Message Description |
|:-------------|:------|
| 1 |Health attestation is supported      |
| 2 |Health attestation is not supported      |

## STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

No State IDs.

## 8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

No State IDs.

## 8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

No State IDs.

## 8005 STATE_TOPICTYPE_LOCATE_DEVICE

No State IDs.

## 8006 STATE_TOPICTYPE_REBOOT_DEVICE

No State IDs.

## 8007 STATE_TOPICTYPE_LOGOUTUSER

No State IDs.

## 8008 STATE_TOPICTYPE_USERSLIST

No State IDs.

## 8009 STATE_TOPICTYPE_DELETEUSER

No State IDs.

## 8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

No State IDs.

## 8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

No State IDs.

## 8012 STATE_TOPICTYPE_SETDEVICENAME

No State IDs.

## 9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

No State IDs.

## 9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

No State IDs.

## Next steps

- [Description of state messaging in Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Software updates management whitepaper for Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
