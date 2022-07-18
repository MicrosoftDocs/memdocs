---
# required metadata

title: Software update errors and descriptions in Microsoft Intune
description: See a list of the Software Update agent error code in Microsoft Intune, including the error code, symbolic name, and error description.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:
ROBOTS: 

# optional metadata

#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Software update agent error codes and descriptions in Microsoft Intune

The following table lists the Intune **Update Agent** error codes. If you can't find a specific error code in this table, see [Windows Update error code list](https://support.microsoft.com/help/938205/windows-update-error-code-list).

|Error code|Symbolic name|More information|
|--------------|-----------------|--------------------|
|**0x00cf0001**|OM_S_SERVICE_STOP|The agent was successfully stopped.|
|**0x00cf0003**|OM_S_UPDATE_ERROR|The operation was completed successfully, but errors occurred during the application of updates.|
|**0x00cf0004**|OM_S_MARKED_FOR_DISCONNECT|A callback was marked to be disconnected later because the request to disconnect the operation occurred while a callback was running.|
|**0x00cf0005**|OM_S_REBOOT_REQUIRED|The system must be restarted to complete the update installation.|
|**0x00cf0006**|OM_S_ALREADY_INSTALLED|The update to be installed is already installed on the system.|
|**0x00cf0007**|OM_S_ALREADY_UNINSTALLED|The update to be removed is not installed on the system.|
|**0x00cf2015**|OM_S_UH_INSTALLSTILLPENDING|The update installation is in progress.|
|**0x80cf0001**|OM_E_NO_SERVICE|The agent could not provide the service.|
|**0x80cf0002**|OM_E_MAX_CAPACITY_REACHED|The maximum capacity of the service was exceeded.|
|**0x80cf0003**|OM_E_UNKNOWN_ID|An ID cannot be found.|
|**0x80cf0004**|OM_E_NOT_INITIALIZED|The object could not be initialized.|
|**0x80cf0007**|OM_E_INVALIDINDEX|The index to a collection is not valid.|
|**0x80cf0008**|OM_E_ITEMNOTFOUND|The key for the queried item could not be found.|
|**0x80cf0009**|OM_E_OPERATIONINPROGRESS|A conflicting operation was in progress. Some operations, like multiple installations cannot be performed simultaneously.|
|**0x80cf000B**|OM_E_CALL_CANCELLED|The operation was canceled.|
|**0x80cf000C**|OM_E_NOOP|No operation was required.|
|**0x80cf000D**|OM_E_XML_MISSINGDATA|The agent could not find required information in the update's XML data.|
|**0x80cf000E**|OM_E_XML_INVALID|The agent found information in the update's XML data that is not valid.|
|**0x80cf000F**|OM_E_CYCLE_DETECTED|Circular update relationships were detected in the metadata.|
|**0x80cf0010**|OM_E_TOO_DEEP_RELATION|The update relationships were too deeply nested to evaluate.|
|**0x80cf0011**|OM_E_INVALID_RELATIONSHIP|An update relationship was found that is not valid.|
|**0x80cf0012**|OM_E_REG_VALUE_INVALID|A registry value was read that is not valid.|
|**0x80cf0013**|OM_E_DUPLICATE_ITEM|The operation tried to add a duplicate item to a list.|
|**0x80cf0014**|OM_E_INVALID_INSTALL_REQUESTED|The caller cannot install updates that were requested for installation.|
|**0x80cf0016**|OM_E_INSTALL_NOT_ALLOWED|The operation tried to install while another installation was in progress, or the system was pending a mandatory restart.|
|**0x80cf0017**|OM_E_NOT_APPLICABLE|The operation was not performed because there are no applicable updates.|
|**0x80cf0018**|OM_E_NO_USERTOKEN|The operation failed because a required user token is missing.|
|**0x80cf0019**|OM_E_EXCLUSIVE_INSTALL_CONFLICT|An exclusive update cannot be simultaneously installed together with other updates.|
|**0x80cf001A**|OM_E_POLICY_NOT_SET|A policy value was not set.|
|**0x80cf001D**|OM_E_INVALID_UPDATE|An update contains metadata that is not valid.|
|**0x80cf001E**|OM_E_SERVICE_STOP|The operation could not be completed because the service or system was being shut down.|
|**0x80cf001F**|OM_E_NO_CONNECTION|The operation could not be completed because the network connection was not available.|
|**0x80cf0020**|OM_E_NO_INTERACTIVE_USER|The operation could not be completed because there is no logged-on interactive user.|
|**0x80cf0021**|OM_E_TIME_OUT|The operation could not be completed because it timed out.|
|**0x80cf0022**|OM_E_ALL_UPDATES_FAILED|The operation failed for all the updates.|
|**0x80cf0024**|OM_E_NO_UPDATE|There are no updates.|
|**0x80cf0025**|OM_E_USER_ACCESS_DISABLED|Group Policy settings prevented access to Windows Update.|
|**0x80cf0026**|OM_E_INVALID_UPDATE_TYPE|The update type is not valid.|
|**0x80cf0028**|OM_E_UNINSTALL_NOT_ALLOWED|The update could not be uninstalled because the request did not originate from a WSUS server.|
|**0x80cf0029**|OM_E_INVALID_PRODUCT_LICENSE|Search might have missed some updates, or there might be an unlicensed application on the system.|
|**0x80cf002C**|OM_E_BIN_SOURCE_ABSENT|A delta-compressed update could not be installed because it required the source.|
|**0x80cf002D**|OM_E_SOURCE_ABSENT|A full-file update could not be installed because it required the source.|
|**0x80cf002E**|OM_E_WU_DISABLED|Access to an unmanaged server is not allowed.|
|**0x80cf002F**|OM_E_CALL_CANCELLED_BY_POLICY|The operation could not be completed because the **DisableWindowsUpdateAccess** policy was set.|
|**0x80cf0030**|OM_E_INVALID_PROXY_SERVER|The proxy list format is not valid.|
|**0x80cf0031**|OM_E_INVALID_FILE|The file is in the wrong format.|
|**0x80cf0032**|OM_E_INVALID_CRITERIA|The search criteria string is not valid.|
|**0x80cf0034**|OM_E_DOWNLOAD_FAILED|The update failed to download.|
|**0x80cf0035**|OM_E_UPDATE_NOT_PROCESSED|The update was not processed.|
|**0x80cf0036**|OM_E_INVALID_OPERATION|The object's current state did not allow the operation.|
|**0x80cf0037**|OM_E_NOT_SUPPORTED|The operation is not supported.|
|**0x80cf0038**|OM_E_WINHTTP_INVALID_FILE|The downloaded file has an unexpected content type.|
|**0x80cf0039**|OM_E_TOO_MANY_RESYNC|The server asked the agent to resync too many times.|
|**0x80cf0043**|OM_E_NO_UI_SUPPORT|There is no support for WUA UI.|
|**0x80cf0044**|OM_E_PER_MACHINE_UPDATE_ACCESS_DENIED|Only administrators can perform this operation on per-computer updates.|
|**0x80cf0045**|OM_E_UNSUPPORTED_SEARCHSCOPE|A search was attempted with an unsupported scope.|
|**0x80cf0046**|OM_E_BAD_FILE_URL|The URL does not point to a file.|
|**0x80cf0047**|OM_E_NOTSUPPORTED|The requested operation is not supported.|
|**0x80cf0049**|OM_E_OUTOFRANGE|The data is out of range.|
|**0x80cf004A**|OM_E_INVALIDWUAVERSION|The data contains a version that is not valid.|
|**0x80cf004B**|OM_E_SEARCH_COMPLETED_WITH_SOME_FAILURES|The search call was completed, but failed to detect some of the updates.|
|**0x80cf004C**|OM_E_DOWNLOAD_COMPLETED_WITH_SOME_FAILURES|The download call was completed, but failed to download some of the updates.|
|**0x80cf004D**|OM_E_INSTALL_COMPLETED_WITH_SOME_FAILURES|The install call was completed, but failed to install some of the updates.|
|**0x80cf004E**|OM_E_WINUPDATE_CACHE_UNINITIALIZED|The Windows Update cache is empty because it has not been initialized.|
|**0x80cf0436**|OM_E_PT_CATALOG_SYNC_REQUIRED|The server does not support category-specific search. Full catalog search must be issued instead.|
|**0x80cf0437**|OM_E_PT_SECURITY_VERIFICATION_FAILURE|There was a problem authorizing with the service.|
|**0x80cf0438**|OM_E_PT_ENDPOINT_UNREACHABLE|There is no route or network connectivity to the endpoint.|
|**0x80cf0439**|OM_E_PT_INVALID_FORMAT|The data received does not meet the data contract expectations.|
|**0x80cf043A**|OM_E_PT_INVALID_URL|The URL is not valid.|
|**0x80cf043B**|OM_E_PT_NWS_NOT_LOADED|The NWS runtime cannot be loaded.|
|**0x80cf043C**|OM_E_PT_PROXY_AUTH_SCHEME_NOT_SUPPORTED|The proxy authentication scheme is not supported.|
|**0x80cf043D**|OM_E_SERVICEPROP_NOTAVAIL|The requested service property is not available.|
|**0x80cf043E**|OM_E_PT_ENDPOINT_REFRESH_REQUIRED|The endpoint provider plug-in requires an online refresh.|
|**0x80cf043F**|OM_E_PT_ENDPOINTURL_NOTAVAIL|A URL for the requested service endpoint is not available.|
|**0x80cf0440**|OM_E_PT_ENDPOINT_DISCONNECTED|The connection to the service endpoint terminated.|
|**0x80cf0441**|OM_E_PT_INVALID_OPERATION|The operation is not valid because protocol talker is in an inappropriate state.|
|**0x80cf0FFF**|OM_E_UNEXPECTED|An operation failed because of reasons that are not explained by another error code.|
|**0x80cf1001**|OM_E_MSI_WRONG_VERSION|Search might have missed some updates because the Windows Installer is an earlier version than version 3.1.|
|**0x80cf1002**|OM_E_MSI_NOT_CONFIGURED|Search might have missed some updates because the Windows Installer is not configured.|
|**0x80cf1003**|OM_E_MSP_DISABLED|Search might have missed some updates because policy has disabled Windows Installer patching.|
|**0x80cf1004**|OM_E_MSI_WRONG_APP_CONTEXT|An update could not be applied because the application is installed per user.|
|**0x80cf2000**|OM_E_UH_REMOTEUNAVAILABLE|A request for a remote update handler could not be completed because no remote process is available.|
|**0x80cf2001**|OM_E_UH_LOCALONLY|A request for a remote update handler could not be completed because the handler is local only.|
|**0x80cf2003**|OM_E_UH_REMOTEALREADYACTIVE|A remote update handler could not be created because one already exists.|
|**0x80cf2004**|OM_E_UH_DOESNOTSUPPORTACTION|A request for the handler to install (uninstall) an update could not be completed because the update does not support install (uninstall).|
|**0x80cf2005**|OM_E_UH_WRONGHANDLER|An operation could not be completed because the wrong handler was specified.|
|**0x80cf2006**|OM_E_UH_INVALIDMETADATA|A handler operation could not be completed because the update contains metadata that is not valid.|
|**0x80cf2007**|OM_E_UH_INSTALLERHUNG|An operation could not be completed because the installer exceeded the time limit. Check whether an update that requires user interaction was approved for deployment. In this case, you must revise the update installation parameters so that it can install silently.|
|**0x80cf2008**|OM_E_UH_OPERATIONCANCELLED|An operation that was being performed by the update handler was canceled.|
|**0x80cf2009**|OM_E_UH_BADHANDLERXML|An operation could not be completed because the handler-specific metadata is not valid.|
|**0x80cf200B**|OM_E_UH_INSTALLERFAILURE|The installer failed to install (uninstall) one or more updates.|
|**0x80cf200D**|OM_E_UH_NEEDANOTHERDOWNLOAD|The update handler did not install the update because it must be downloaded again.|
|**0x80cf200E**|OM_E_UH_NOTIFYFAILURE|The update handler failed to send notification of the status of the install (uninstall) operation.|
|**0x80cf2014**|OM_E_UH_POSTREBOOTSTILLPENDING|The post-reboot operation for the update is still in progress.|
|**0x80cf2015**|OM_E_UH_POSTREBOOTRESULTUNKNOWN|The result of the post-reboot operation for the update could not be determined.|
|**0x80cf2016**|OM_E_UH_POSTREBOOTUNEXPECTEDSTATE|The state of the update after its post-reboot operation was completed is unexpected.|
|**0x80cf2017**|OM_E_UH_NEW_SERVICING_STACK_REQUIRED|The operation system servicing stack must be updated before this update is downloaded or installed.|
|**0x80cf2018**|OM_E_UH_CALLED_BACK_FAILURE|A callback installer called back with an error.|
|**0x80cf2019**|OM_E_UH_CUSTOMINSTALLER_INVALID_SIGNATURE|The custom installer signature did not match the signature that the update requires.|
|**0x80cf201A**|OM_E_UH_UNSUPPORTED_INSTALLCONTEXT|The installer does not support the installation configuration.|
|**0x80cf201B**|OM_E_UH_INVALID_TARGETSESSION|The targeted session for the installation is not valid.|
|**0x80cf2FFF**|OM_E_UH_UNEXPECTED|An update handler error is not covered by another OM_E_UH_&#42; code.|
|**0x80cf3FFD**|OM_E_NON_UI_MODE|Cannot show UI when in non-UI mode. Windows Update client UI modules might not be installed.|
|**0x80cf3FFE**|OM_E_WUCLTUI_UNSUPPORTED_VERSION|This version of WU client UI exported functions is not supported.|
|**0x80cf3FFF**|OM_E_AUCLIENT_UNEXPECTED|A user interface error occurred that is not covered by another OM_E_AUCLIENT_&#42; error code.|
|**0x80cf4007**|OM_E_PT_SOAPCLIENT_SOAPFAULT|Same as **SOAPCLIENT_SOAPFAULT**. SOAP client failed because a SOAP fault of **OM_E_PT_SOAP_&#42;** error code type occurred.|
|**0x80cf4008**|OM_E_PT_SOAPCLIENT_PARSEFAULT|Same as **SOAPCLIENT_PARSEFAULT_ERROR**.  SOAP client failed to parse a SOAP fault error.|
|**0x80cf400A**|OM_E_PT_SOAPCLIENT_PARSE|Same as **SOAPCLIENT_PARSE_ERROR**.  SOAP client failed to parse the response from the server.|
|**0x80cf400B**|OM_E_PT_SOAP_VERSION|Same as **SOAP_E_VERSION_MISMATCH**. SOAP client found an unrecognizable namespace for the SOAP envelope.|
|**0x80cf400C**|OM_E_PT_SOAP_MUST_UNDERSTAND|Same as **SOAP_E_MUST_UNDERSTAND**. SOAP client could not interpret a header.|
|**0x80cf400D**|OM_E_PT_SOAP_CLIENT|Same as **SOAP_E_CLIENT**. SOAP client found the message was malformed. Correct before resending.|
|**0x80cf400E**|OM_E_PT_SOAP_SERVER|Same as **SOAP_E_SERVER**. The SOAP message could not be processed because of a server error. Resend later.|
|**0x80cf4010**|OM_E_PT_EXCEEDED_MAX_SERVER_TRIPS|The number of round trips to the server exceeded the maximum limit.|
|**0x80cf4012**|OM_E_PT_DOUBLE_INITIALIZATION|The initialization failed because the object was already initialized.|
|**0x80cf4013**|OM_E_PT_INVALID_COMPUTER_NAME|The computer name could not be determined.|
|**0x80cf4015**|OM_E_PT_REFRESH_CACHE_REQUIRED|The reply from the server indicates that the server was changed or the cookie was invalid. Refresh the internal cache and retry.|
|**0x80cf4016**|OM_E_PT_HTTP_STATUS_BAD_REQUEST|Same as **HTTP status 400**. The server could not process the request because the syntax is not valid.|
|**0x80cf4017**|OM_E_PT_HTTP_STATUS_DENIED|Same as **HTTP status 401**. The requested resource requires user authentication.|
|**0x80cf4018**|OM_E_PT_HTTP_STATUS_FORBIDDEN|Same as **HTTP status 403**. The server understood the request, but declined to fulfill it.|
|**0x80cf4019**|OM_E_PT_HTTP_STATUS_NOT_FOUND|Same as **HTTP status 404**. The server cannot find the requested URI (Uniform Resource Identifier).|
|**0x80cf401A**|OM_E_PT_HTTP_STATUS_BAD_METHOD|Same as **HTTP status 405**. The HTTP method is not allowed.|
|**0x80cf401B**|OM_E_PT_HTTP_STATUS_PROXY_AUTH_REQ|Same as **HTTP status 407**. Proxy authentication is required.|
|**0x80cf401C**|OM_E_PT_HTTP_STATUS_REQUEST_TIMEOUT|Same as **HTTP status 408**. The server timed out waiting for the request.|
|**0x80cf401D**|OM_E_PT_HTTP_STATUS_CONFLICT|Same as **HTTP status 409**. The request was not completed because of a conflict with the current state of the resource.|
|**0x80cf401E**|OM_E_PT_HTTP_STATUS_GONE|Same as **HTTP status 410**. The requested resource is no longer available at the server.|
|**0x80cf401F**|OM_E_PT_HTTP_STATUS_SERVER_ERROR|Same as **HTTP status 500**. An error internal to the server prevented the request from being fulfilled.|
|**0x80cf4020**|OM_E_PT_HTTP_STATUS_NOT_SUPPORTED|Same as **HTTP status 500**. The server does not support the functionality that is required to fulfill the request.|
|**0x80cf4021**|OM_E_PT_HTTP_STATUS_BAD_GATEWAY|Same as **HTTP status 502**. The server, while acting as a gateway or proxy, received an invalid response from the upstream server that it accessed while trying to fulfill the request.|
|**0x80cf4022**|OM_E_PT_HTTP_STATUS_SERVICE_UNAVAIL|Same as **HTTP status 503**. The service is temporarily overloaded.|
|**0x80cf4023**|OM_E_PT_HTTP_STATUS_GATEWAY_TIMEOUT|Same as **HTTP status 503**. The request was timed out waiting for a gateway.|
|**0x80cf4024**|OM_E_PT_HTTP_STATUS_VERSION_NOT_SUP|Same as **HTTP status 505**. The server does not support the HTTP protocol version that is used for the request.|
|**0x80cf4025**|OM_E_PT_FILE_LOCATIONS_CHANGED|The operation failed because of a changed file location. Refresh the internal state and resend.|
|**0x80cf4027**|OM_E_PT_NO_AUTH_PLUGINS_REQUESTED|The server returned an empty authentication information list.|
|**0x80cf4028**|OM_E_PT_NO_AUTH_COOKIES_CREATED|The agent could not create any valid authentication cookies.|
|**0x80cf4029**|OM_E_PT_INVALID_CONFIG_PROP|A configuration property value was wrong.|
|**0x80cf402A**|OM_E_PT_CONFIG_PROP_MISSING|A configuration property value was missing.|
|**0x80cf402B**|OM_E_PT_HTTP_STATUS_NOT_MAPPED|The HTTP request could not be completed, and the reason did not correspond to any of the **OM_E_PT_HTTP_&#42;** error codes.|
|**0x80cf402C**|OM_E_PT_WINHTTP_NAME_NOT_RESOLVED|Same as **ERROR_WINHTTP_NAME_NOT_RESOLVED**. The proxy server or destination server name cannot be resolved.|
|**0x80cf402F**|OM_E_PT_ECP_SUCCEEDED_WITH_ERRORS|The external .cab file processing was completed with some errors.|
|**0x80cf4030**|OM_E_PT_ECP_INIT_FAILED|The external .cab processor initialization was not completed.|
|**0x80cf4031**|OM_E_PT_ECP_INVALID_FILE_FORMAT|The format of a metadata file is not valid.|
|**0x80cf4032**|OM_E_PT_ECP_INVALID_METADATA|The external cab processor found metadata that is not valid.|
|**0x80cf4033**|OM_E_PT_ECP_FAILURE_TO_EXTRACT_DIGEST|The file digest could not be extracted from an external .cab file.|
|**0x80cf4034**|OM_E_PT_ECP_FAILURE_TO_DECOMPRESS_CAB_FILE|An external .cab file could not be decompressed.|
|**0x80cf4035**|OM_E_PT_ECP_FILE_LOCATION_ERROR|The external cab processor could not get the file locations.|
|**0x80cf4FFF**|OM_E_PT_UNEXPECTED|A communication error occurred that is not covered by another **OM_E_PT_&#42;** error code.|
|**0x80cf6001**|OM_E_DM_URLNOTAVAILABLE|A download manager operation could not be completed because the requested file does not have a URL.|
|**0x80cf6002**|OM_E_DM_INCORRECTFILEHASH|A download manager operation could not be completed because the file digest was not recognized.|
|**0x80cf6003**|OM_E_DM_UNKNOWNALGORITHM|A download manager operation could not be completed because the file metadata requested an unrecognized hash algorithm.|
|**0x80cf6005**|OM_E_DM_NONETWORK|A download manager operation could not be completed because the network connection was not available.|
|**0x80cf6007**|OM_E_DM_NOTDOWNLOADED|The update has not been downloaded.|
|**0x80cf6008**|OM_E_DM_FAILTOCONNECTTOBITS|A download manager operation failed because the download manager could not connect the Background Intelligent Transfer Service (BITS).|
|**0x80cf6009**|OM_E_DM_BITSTRANSFERERROR|A download manager operation failed because there was an unspecified Background Intelligent Transfer Service (BITS) transfer error.|
|**0x80cf600a**|OM_E_DM_DOWNLOADLOCATIONCHANGED|A download must be restarted because the download source location has changed.|
|**0x80cf600B**|OM_E_DM_CONTENTCHANGED|A download must be restarted because the update content changed in a new revision.|
|**0x80cf6FFF**|OM_E_DM_UNEXPECTED|A download manager error occurred that is not covered by another **OM_E_DM_&#42;** error code.|
|**0x80cf7003**|OM_E_INVALID_EVENT_PAYLOAD|An event payload was specified that is not valid.|
|**0x80cf7004**|OM_E_INVALID_EVENT_PAYLOADSIZE|The size of the event payload submitted is not valid.|
|**0x80cf7005**|OM_E_SERVICE_NOT_REGISTERED|The service is not registered.|
|**0x80cf8000**|OM_E_DS_SHUTDOWN|An operation failed because the agent is shutting down.|
|**0x80cf8001**|OM_E_DS_INUSE|An operation failed because the data store was in use.|
|**0x80cf8002**|OM_E_DS_INVALID|The current and expected states of the data store do not match.|
|**0x80cf8003**|OM_E_DS_TABLEMISSING|The data store is missing a table.|
|**0x80cf8004**|OM_E_DS_TABLEINCORRECT|The data store contains a table that has unexpected columns.|
|**0x80cf8005**|OM_E_DS_INVALIDTABLENAME|A table could not be opened because the table is not in the data store.|
|**0x80cf8006**|OM_E_DS_BADVERSION|The current and expected versions of the data store do not match.|
|**0x80cf8007**|OM_E_DS_NODATA|The information that is requested is not in the data store.|
|**0x80cf8008**|OM_E_DS_MISSINGDATA|The data store is missing required information or has a null in a table column that requires a non-null value.|
|**0x80cf8009**|OM_E_DS_MISSINGREF|The data store is missing required information or has a reference to missing license terms, file, localized property, or linked row.|
|**0x80cf800A**|OM_E_DS_UNKNOWNHANDLER|The update was not processed because its update handler was not recognized.|
|**0x80cf800B**|OM_E_DS_CANTDELETE|The update was not deleted because it is still referenced by one or more services.|
|**0x80cf800C**|OM_E_DS_LOCKTIMEOUTEXPIRED|The data store section could not be locked within the allotted time.|
|**0x80cf800E**|OM_E_DS_ROWEXISTS|The row was not added because an existing row has the same primary key.|
|**0x80cf800F**|OM_E_DS_STOREFILELOCKED|The data store could not be initialized because it was locked by another process.|
|**0x80cf8010**|OM_E_DS_CANNOTREGISTER|The data store is not allowed to be registered with COM in the current process.|
|**0x80cf8011**|OM_E_DS_UNABLETOSTART|An operation could not create a data store object in another process.|
|**0x80cf8013**|OM_E_DS_DUPLICATEUPDATEID|The server sent the same update to the client with two different revision IDs.|
|**0x80cf8014**|OM_E_DS_UNKNOWNSERVICE|An operation could not be completed because the service is not in the data store.|
|**0x80cf8015**|OM_E_DS_SERVICEEXPIRED|An operation could not be completed because the registration of the service has expired.|
|**0x80cf8016**|OM_E_DS_DECLINENOTALLOWED|A request to hide an update was declined because it is a mandatory update or because it was deployed with a deadline.|
|**0x80cf8017**|OM_E_DS_TABLESESSIONMISMATCH|A table was not closed because it is not associated with the session.|
|**0x80cf8018**|OM_E_DS_SESSIONLOCKMISMATCH|A table was not closed because it is not associated with the session.|
|**0x80cf8019**|OM_E_DS_NEEDWINDOWSSERVICE|The request to remove or unregister the service was declined because it is a built-in service or because Automatic Updates cannot fall back to another service.|
|**0x80cf801A**|OM_E_DS_INVALIDOPERATION|The request was declined because the operation is not allowed.|
|**0x80cf801B**|OM_E_DS_SCHEMAMISMATCH|The schema of the current data store and the schema of a table in a backup XML document do not match.|
|**0x80cf801C**|OM_E_DS_RESETREQUIRED|The data store requires a session reset. Release the session and retry with a new session.|
|**0x80cf801D**|OM_E_DS_IMPERSONATED|A data store operation could not be completed because it was requested with an impersonated identity.|
|**0x80cf8FFF**|OM_E_DS_UNEXPECTED|A data store error occurred that is not covered by another **OM_E_DS_&#42;** code.|
|**0x80cfA000**|OM_E_AU_NOSERVICE|Automatic Updates could not service incoming requests.|
|**0x80cfA004**|OM_E_AU_PAUSED|Automatic Updates could not process incoming requests because it was paused.|
|**0x80cfA005**|OM_E_AU_NO_REGISTERED_SERVICE|No unmanaged service is registered with Automatic Updates.|
|**0x80cfA006**|OM_E_AU_DETECT_SVCID_MISMATCH|The default service registered with Automatic Updates changed during the search.|
|**0x80cfA007**|OM_E_AU_ALREADY_PROMPTING_FOR_REBOOT|Automatic Updates is already prompting the user to restart.|
|**0x80cfAFFF**|OM_E_AU_UNEXPECTED|An Automatic Updates error occurred that is not covered by another **OM_E_AU &#42;** code.|
|**0x80cfE001**|OM_E_EE_UNKNOWN_EXPRESSION|An expression evaluator operation could not be completed because an expression was not recognized.|
|**0x80cfE002**|OM_E_EE_INVALID_EXPRESSION|An expression evaluator operation could not be completed because an expression was not valid.|
|**0x80cfE003**|OM_E_EE_MISSING_METADATA|An expression evaluator operation could not be completed because an expression contains an incorrect number of metadata nodes.|
|**0x80cfE004**|OM_E_EE_INVALID_VERSION|An expression evaluator operation could not be completed because the version of the serialized expression data is not valid.|
|**0x80cfE005**|OM_E_EE_NOT_INITIALIZED|The expression evaluator could not be initialized.|
|**0x80cfE006**|OM_E_EE_INVALID_ATTRIBUTEDATA|An expression evaluator operation could not be completed because an attribute is not valid.|
|**0x80cfE007**|OM_E_EE_CLUSTER_ERROR|An expression evaluator operation could not be completed because the cluster state of the computer could not be determined.|
|**0x80cfEFFF**|OM_E_EE_UNEXPECTED|An expression evaluator error occurred that is not covered by another **OM_E_EE_&#42;** error code.|
|**0x80cfF001**|OM_E_REPORTER_EVENTCACHECORRUPT|The event cache file was defective.|
|**0x80cfF002**|OM_E_REPORTER_EVENTNAMESPACEPARSEFAILED|The XML in the event namespace descriptor could not be parsed.|
|**0x80cfF003**|OM_E_INVALID_EVENT|The XML in the event namespace descriptor is not valid.|
|**0x80cfF004**|OM_E_SERVER_BUSY|The server rejected an event because the server was too busy.|
|**0x80cfFFFF**|OM_E_REPORTER_UNEXPECTED|A reporter error occurred that is not covered by another error code.|
|**0x80af0005**|OMC_E_INSTALL_NOT_ALLOWED_REBOOT_REQUIRED|Installation failed because there is a pending mandatory reboot.|
|**0x80af0006**|OMC_E_DOWNLOAD_CANCELLED|The download was canceled.|