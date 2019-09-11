---
title: Troubleshooting CMPivot
titleSuffix: Configuration Manager
description: Learn how to troubleshoot CMPivot in Configuration Manager.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart 
manager: dougeby
ms.collection: M365-identity-device-management
---

# Troubleshooting CMPivot

CMPivot is an in-console utility that now provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. Occasionally, you may find yourself needing to troubleshoot CMPivot. For example, you may see that a client sent a state message for CMPivot. However, the site server didn't process the message because it was corrupted. This article helps you understand the flow of information for CMPivot.

## Get information from the site server

By default, the site server log files are located in C:\Program Files\Microsoft Configuration Manager\logs. This location may change depending on what was specified for your installation directory or if you offloaded items like the SMS Provider to another server.

Check the **smsprov.log** for this line:

``` Log
Auditing: User <username> initiated client operation 135 to collection <CollectionId>.
```

Find the ID in the CMPivot window. This ID is the **ClientOperationID**.

![CMPivot window with ClientOperationID highlighted](media/cmpivot-clientoperationid.png)

Find the **TaskID** from the ClientAction table. The **TaskID** corresponds to the **UniqueID** in the ClientAction table. 

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

In the **BgbServer.log**, look for the **TaskID** you gathered from SQL. In the Bgbserver.log, it will be labeled **TaskGUID**. For example: 


- Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: **F8C7C37F-B42B-4C0A-B050-2BB44DF1098A** TaskType: 15 TaskParam:   PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
    g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp
    cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX
    Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP
    SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ
    YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd
    HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH
    JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0
    UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW
    1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX
    JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N
    NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2
    NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW
    1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi
    ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU
    2NyaXB0Q29udGVudD4=-) to 5 clients with throttling (strategy: 1 param: 42)
   Finished sending push task (PushID: 260 TaskID: 258) to 5 clients

## Client logs

Once you have the information from the site server, check the client logs. By default, the client logs are located in C:\Windows\CCM\Logs.

Check the **CcmNotificationAgent.log**. You'll find logs like the following entry:  

- **Error! Bookmark not defined.**+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
    g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp
    cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX
    Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP
    SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ
    YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd
    HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH
    JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0
    UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW
    1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX
    JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N
    NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2
    NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW
    1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi
    ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU
    2NyaXB0Q29udGVudD4=-

Check **Scripts.log** for the **TaskID**. In the following example, we see **Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}**:

``` Log
Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
State message: Task Id {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A} Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

Check the **StateMessage.log**. Our example **TaskID** is near the bottom of the message next to &lt;Param>. You should see lines similar to the one below:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>
StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

> [!NOTE]
> The above log entry in the StateSys.log is only visible when Verbose Logging is enabled for the SMS_STATE_SYSTEM component, which can be done by modifying this registry key:
> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_STATE_SYSTEM\Verbose logging = 1 (Default is 0)

## Review messages on the site server

Open the **statesys.log** to see if the message is received and processed. Our example **TaskID** is near the bottom of the message next to &lt;Param>.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Check the state message inbox if you don't see that the message has been processed. The default location of the inbox is C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\. The files will be in either:
  
- Incoming
- Corrupted
- Process

Check the monitoring view for CMPivot from SQL using the **TaskID**.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

## Next steps

[Using CMPivot](/sccm/core/servers/manage/cmpivot)

[Create and run PowerShell scripts](/sccm/apps/deploy-use/create-deploy-scripts)
