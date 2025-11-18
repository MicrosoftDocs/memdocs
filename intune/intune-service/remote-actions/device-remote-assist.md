---
title: "Remote Device Action: New Remote Assistance Session"
description: Learn how to use the the new remote assistance session action in Intune to offer support to your users.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action:  new Remote Assistance session

Microsoft Intune provides remote assistance capabilities to help IT support teams troubleshoot and resolve issues on user devices. This functionality is available through two integration paths: **Remote Help** (part of the Intune Suite) and **TeamViewer**. Each option offers different features, licensing requirements, and setup steps.

## How It Works

When selecting the **New remote assistance session** action in Intune:

- If your tenant is configured for **Remote Help**, the session will launch using Microsoft's Remote Help app.
- If your tenant is configured for **TeamViewer**, the session will launch using TeamViewer's remote support interface.

## Learn More

Every solution has its own requirements and options. For more information, see:

- [Use Remote Help with Microsoft Intune][RA-HELP]
- [Use TeamViewer to remotely administer Intune devices][RA-TVIEW]

[RA-HELP]: ../fundamentals/remote-help.md
[RA-TVIEW]: ../fundamentals/teamviewer-support.md
