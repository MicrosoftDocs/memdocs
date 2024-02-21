---
author: Banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 06/29/2020
---

### <a name="ki_auth"></a> Microsoft Entra authentication doesn't work
<!--7569264-->
Configuration Manager's use of the Microsoft Entra security token service doesn't work. The **CCM_STS.log** on the management point contains an entry similar to the following error: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` It also includes the HRESULT 0x80131040.

Another symptom is issues with a cloud management gateway (CMG). If you run the CMG connection analyzer, it fails testing the CMG channel for management point with the following error: `Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

This issue is because of a version discrepancy with a supporting library.

To work around the issue, copy **System.IdentityModel.Tokens.JWT.dll** from the \bin\X64 folder of the installation directory on the site server to the SMS_CCM\CCM_STS\bin folder on the management point.
