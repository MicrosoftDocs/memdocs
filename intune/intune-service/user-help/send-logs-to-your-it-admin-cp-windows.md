---
title: Report problems in Company Portal app for Windows
description: Share app diagnostics with your support person to diagnose a problem with the Company Portal app for Windows.
ms.date: 11/08/2024
ms.reviewer: scottduf
---

# Report a problem in Company Portal for Windows

**Applies to Intune Company Portal for Windows**

Report a problem or error that occurs in the Intune Company Portal app for Windows. This article describes how to share app diagnostic logs with your support person.

> [!NOTE]
> App logs are also shared with Microsoft Support in case the problem requires additional help. Your support person will reach out to Microsoft Support with your incident ID to work with them.

## Report problem to support person
Complete the following steps to upload Company Portal app logs.

1. Open the **Company Portal** app.
1. Go to **Help & support**.
1. Select **Upload logs**.

   > [!Note]
   > After you select **Upload logs**, the Company Portal sends your logs to Microsoft's support team. This step is a proactive one that makes it easier to troubleshoot and resolve problems that are escalated to Microsoft support.

1. When prompted to choose a program, select the Mail app or another preferred email app.

1. The email app opens an email template for you to fill in. Describe the problem and the steps you took leading up to the problem. Then send the email to your IT support person so that they can follow up on the issue.

1. Follow up with your support person as needed.

### Collect logs manually


Alternatively, complete the following steps to download Company Portal app logs manually.

1. Navigate to the following path using **File Explorer**: **%localappdata%\Packages\Microsoft.CompanyPortal_8wekyb3d8bbwe\LocalState**. The **%localappdata%** variable resolves to your local application data folder. By default, this corresponds to **C:\Users\<UserName>\AppData\Local Replace <UserName>** where **UserName** is the account name of the signed-in user. 
2. Application logs are stored in files following the pattern **Log_<n>.log**. Attach these logs to the support ticket.

## Report problem to Microsoft

Complete the following steps to report a problem directly to Microsoft in the Feedback Hub app. Microsoft doesn't respond to this type of report but uses it to improve upon the products. You can include screenshots and diagnostic details, but the report should remain anonymous, so don't include information like name, email address, or phone number.

1. Open the **Company Portal** app.
1. Go to **Help & support**.
1. Select **Report problem to Microsoft**.
1. Select **Report problem**. Alternatively, you can send a suggestion or leave a review of the app.

## What is a diagnostic log?

Events and errors that occur in the Company Portal app are saved on your device in a special document called a _diagnostic log_. Logs can reveal:
* When the problem happened.
* The steps leading up to the problem.
* The state of the app when the problem appeared.

## Next steps

If your workplace or school needs additional information about app or device activity, you might need to resend [logs from the Settings app](send-logs-to-your-it-admin-settings-windows.md).
