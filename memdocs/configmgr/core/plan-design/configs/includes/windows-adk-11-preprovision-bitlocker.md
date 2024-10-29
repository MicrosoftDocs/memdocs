---
author: banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 11/15/2021
ms.localizationpriority: medium
---

### Pre-provisioning BitLocker during task sequence doesn't own TPM

<!-- 11307733 -->

Applies to: _Windows ADK for Windows 11 (version 10.1.22000)_

When you use a Windows 11-based boot image with an OS deployment task sequence that includes the [Pre-provision BitLocker](../../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker) step, the step might fail. You'll see errors similar to the following strings in the smsts.log:

```log
'TakeOwnership' failed (2147942402)
pTpm->TakeOwnership(sOwnerAuth), HRESULT=80070002
Failed to take ownership of TPM. Ensure that Active Directory permissions are properly configured
The system cannot find the file specified. (Error: 80070002; Source: Windows)
Process completed with exit code 2147942402
Failed to run the action: Pre-provision BitLocker. Error -2147024894
```

To work around this issue, add a **Run Command Line** step to the task sequence before the **Pre-provision BitLocker** step. Run the following command:

`reg.exe add HKLM\SOFTWARE\Policies\Microsoft\TPM /v OSManagedAuthLevel /t REG_DWORD /d 2 /f`

For more information on this registry key, see [Change the TPM owner password](/windows/security/information-protection/tpm/change-the-tpm-owner-password).
