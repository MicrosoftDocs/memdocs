---
title: "Introduction to WBEMTEST"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1a627513-494d-4e82-92e4-b3689c9ecf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Introduction to WBEMTEST
If you spend much time around Configuration Manager you become aware that much of it runs through WMI.  WMI is "Windows Management Instrumentation" and is Microsoft’s implementation of an Internet standard called Web Based Enterprise Management (WBEM).  

 As you dig further into Configuration Manager - perhaps doing task sequences and wanting to provide intelligent branching, digging into hardware inventory to possibly extend it, or working with the Configuration Manger SDK – you will need to dig deeper in to WMI/WBEM.  One useful tool for working with WMI/WBEM is WBEMTEST. There are many WMI tools out there.  However, WBEMTEST is immediately available on most systems, rather than having to be downloaded first. You might think of it like Notepad.exe – there are text editors with richer capabilities available, but Notepad.exe is always there when you need to view or create a text file.  

## Opening WBEMTEST  
 WBEMTEST is available on any Windows system. Go to Start and type "WBEMTEST" into the search or run box.  

 When you launch WBEMTEST, different operating system will work slightly differently.  Some will automatically connect to a WMI namespace, others (like Windows 7) will not.  If you aren’t connected automatically to a WMI namespace, you can hit the connect button, make sure that "root\cimv2" is selected, then hit connect again.  Now you are back in the main user interface with everything available (when not connected, most buttons are grayed out).  You can think of a WMI namespace as similar to a directory within WMI.  You can navigate to other WMI namespaces, just like you might change directories on the file system. ROOT\CIMV2 is a WMI namespace where a lot of hardware information is kept – a good starting point.  

> [!IMPORTANT]
>  One limitation of WBEMTEST, is that it doesn’t browse the WMI namespaces – you need to know where you’re going to connect. ROOT\CIMV2 (all Windows systems), ROOT\CCM (Configuration Manager clients) and ROOT\SMS\site_\<site code> (Configuration Manager site server) are some useful starting points.  

 ROOT\CIMV2 Namespace  

 ![WBEMTEST CIMV2](../../../develop/core/understand/media/wbemtestcimv2.jpg "WBEMTESTCIMV2")  

 Configuration Manager Primary Client Namespace  

 ![WBEMTEST CCM](../../../develop/core/understand/media/wbemtest_ccm.jpg "WBEMTEST_CCM")  

 Configuration Manager Primary Site Server Namespace (Site Code: ABC)  

 ![WBEMTEST Site](../../../develop/core/understand/media/wbemtest_site.jpg "WBEMTEST_SITE")  

 Once you are connected to a WMI namespace, there are many options. If you are already a WMI expert and know what you are after, you could hit the query button and type in a WMI query to look for something specific.  

 When just starting out, one approach is to explore WMI a bit by browsing the classes in the **ROOT\CIMV2** namespace.  

1.  Open WBEMTEST.  

2.  Connect to the **ROOT\CIMV2** namespace.  

3.  Click the **Enum Classes** button.  

4.  Select **Recursive** and click **OK**.  

 You have just done the equivalent of a `DIR` to list all the contents of the namespace.  Everything with underscores (\__) in the front of the name is WMI overhead - this is what helps WMI be WMI.  In most cases you will skip over everything starting with underscores (\_\_) and look at classes that are specific interest to you.  

 A more specific example using `Win32_Service`:  

1.  Open WBEMTEST.  

2.  Connect to the **ROOT\CIMV2** namespace.  

3.  Click the **Enum Classes** button.  

4.  Select **Recursive** and click **OK**.  

5.  Browse to **Win32_Service** and select it by double-clicking.  

     You have now opened up the Win32_Service class in WMI  - all of the services on your computer are related to this class. (It gets a little complicated here and the directory analogy breaks down at this point – we’ll skip the details and move on to some useful next steps).  

6.  Click the **Instances** button to see a list of the services available on your computer.  

7.  Pick a service, such as `RemoteRegistry` and select it by double-clicking.  

8.  Click the **Show MOF** button.  

 Looking at the MOF is a convenient way to look at the information about the RemoteRegistry service- here you can see the service state, description, start mode, etc.  

 This was just a starting point to introduce WBEMTEST. Once you are familiar with WBEMTEST, it will become an invaluable tool as you dig into WMI.  

### More Resources  
 **Books:** There are numerous books available for WMI. A few example books are listed below.  

-   [Developing WMI Solutions: A Guide to Windows Management Instrumentation](http://www.amazon.com/gp/product/0201616130/ref=pd_lpo_k2_dp_sr_1?pf_rd_p=1535523722&pf_rd_s=lpo-top-stripe-1&pf_rd_t=201&pf_rd_i=1578702607&pf_rd_m=ATVPDKIKX0DER&pf_rd_r=05X3A23E6YKTXGZ0P9NZ)  

-   [Windows Management Instrumentation](http://www.amazon.com/Windows-Management-Instrumentation-Matthew-Lavy/dp/1578702607)  

-   [Microsoft® Windows® Scripting with WMI: Self-Paced Learning Guide](http://www.amazon.com/Microsoft-Windows-Scripting-WMI-Self-Paced/dp/0735622310/ref=sr_1_5?ie=UTF8&qid=1383150816&sr=8-5&keywords=wmi+books)  

 **Videos:** There are numerous videos available for WMI. A few example videos are listed below.  

-   [YouTube: WMI Powershell Introduction](http://www.youtube.com/watch?v=5qZfs4j73IQ)  

-   [YouTube: What is WMI and how to enable remote WMI ?](http://www.youtube.com/watch?v=Nlf3IuTY9wA)  

 **Other:** Other resources for WMI are listed below.  

-   [Windows Management Instrumentation (SDK)](http://msdn.microsoft.com/library/aa394582.aspx)  

-   [WMI Scripting Primer: Part 1](http://msdn.microsoft.com/library/ms974579.aspx)  

-   [WMI Scripting Primer: Part 2](http://msdn.microsoft.com/library/ms974592.aspx)  

-   [WMI Scripting Primer: Part 3](http://msdn.microsoft.com/library/ms974547.aspx)  

## See Also  
 [Getting Started with Configuraiton Manager Programming](../../../develop/core/understand/getting-started-with-configuration-manager-programming.md)
