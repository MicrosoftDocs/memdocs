---
title: include file
description: include file
author: ErikjeMS  
ms.service: cloudpc
ms.topic: include
ms.date: 07/14/2022
ms.author: erikje
ms.custom: include file
---

## Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC

When non-local admin users sign in to a Cloud PC by uinsg an iPad and the Microsoft Remote Desktop app, the start menu and task bar might be missing from the Windows 11 user interface.

**Troubleshooting steps**: Make sure that you have the latest version of Remote Desktop Client as found [here](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients).
In addition, you can also sign in to the Cloud PC by using [windows365.microsoft.com](https://windows365.microsoft.com).

## Restore and automatic rolling credentials

Many devices registered with Active Directory might have a machine account password that is automatically updated. By default, these passwords are updated every 30 days. This automation applies to hybrid joined PCs but not Azure Active Directory Native PCs.

The machine account password is maintained on the Cloud PC. If the Cloud PC is restored to a point that has a previous password stored, the Cloud PC won't be able to sign onto the domain.

For more information, see [Machine Account Password Process](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/machine-account-password-process/ba-p/396026).

## Cursor visible location offset from actual position

In a remote desktop session, when you select one position in a text file, the cursor in the Cloud PC has some offset with the real position.

**Possible cause**: In high DPI mode, both the server and Cloud PC browser scale the cursor. This conflict results in an offset between the visible cursor position and the actual cursor focus.

**Troubleshooting steps**: Turn off high DPI mode.

## Outlook only downloads one month of mail<!--39845820-->

Outlook only downloads one month of previous mail and this can't be changed in Outlook settings.

 **Troubleshooting steps**:

1. Launch registry editor.
2. Remove the **syncwindowsetting** regkey under the path \HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\office\16.0\outlook\cached mode.
3. Add the **syncwindowsetting** regkey with the value 1 under the path HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Cached Mode.

After you complete these steps, the default will be one month. However, the download period can be changed in Outlook settings.