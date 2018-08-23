---
title: System Requirements for Business Central 2018
description: This article provides the specifications of minimum hardware and software requirements to install and run Business Central on-premises.
author: jswymer
ms.custom: na
ms.reviewer: edupont
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
manager: edupont
ms.date: 08/23/2018
---
# System Requirements for [!INCLUDE[prodlong](../developer/includes/prodlong.md)] On-premises

The following sections list the minimum hardware and software requirements to install and run [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on-premises. **Minimum** means that later versions \(such as SP1, SP2, or R2 versions\) of a required software product are also supported.  

> [!NOTE]  
>  [!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs some software if it is not already present in the target computer. For more information, see the "Additional Information" section for each component.  

## Client Components

###  <a name="WebClient"></a> Web Client Requirements  
 The following table shows the minimum system requirements for the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Web client on-premises.  

|||  
|-|-|  
|Supported browsers|<ul><li>Microsoft Edge.</li><li>Internet Explorer 11.</li><li>Google Chrome 61.0 for Windows.</li><li>Mozilla Firefox 55.0 for Windows.</li><li>Safari 10.0 for macOS.</li></ul><br><br>Cookies and JavaScript must be enabled in the browser.|  
|Business inbox in Outlook|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|  
|Sending data to Excel|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|  
|Editing in Excel using the Excel Add-in |<ul><li>Excel 2016 or Excel Online.<br /><br />For more information, see [Exporting Your Business Data to Excel](/dynamics365/business-central/about-export-data).</li></ul>|  
|SharePoint Online links|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|  
|Printing reports to Excel or Word|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|  
|Additional information|If you experience problems using the [!INCLUDE[nav_web](../developer/includes/nav_web_md.md)], you can try to turn off browser tools, such as translator tools that may run in the background.|  

###  <a name="NavApps"></a> [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Tablet Client and Phone Client \(in a Browser\) Requirements  
 The following table shows the minimum system requirements for the [!INCLUDE[nav_tablet](../developer/includes/nav_tablet_md.md)] and [!INCLUDE[nav_phone](../developer/includes/nav_phone_md.md)] running in a browser when used for development and testing purposes.  

|||  
|-|-|  
|Server component|Identical to the [!INCLUDE[prodshort](../developer/includes/prodshort.md)]Web client.|  
|Supported browsers|The following desktop browsers are supported:<ul><li> Microsoft Edge</li><li>Internet Explorer 11 \(build 11.0.9600.17239\) for Windows 10.</li><li>Google Chrome 61.0 for Windows.</li><li>Mozilla Firefox 55.0 for Windows.</li><li>Safari 10.0 for macOS.</li></ul><br><br>Cookies and JavaScript must be enabled in the browser. |  

###  <a name="DynNAVApp"></a> [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Universal App Requirements  
 The following table shows the minimum system requirements for the [!INCLUDE[nav_uni_app](../developer/includes/nav_uni_app_md.md)]. For the latest information, see [Business Central for Windows](http://go.microsoft.com/fwlink/?LinkId=509974), [Business Central for iPad and iPhone](http://go.microsoft.com/fwlink/?LinkId=509975), and [Business Central for Android tablet and Android phone](http://go.microsoft.com/fwlink/?LinkId=509976).  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 S, Home, Pro, Enterprise, or Education \(32-bit and 64-bit editions\).</li><li>Android 5.0 or higher (tablet and phone).</li><li> iOS 10.0 or higher (iPad and iPhone).</li></ul>|  
|Additional hardware|<ul><li>1 GB RAM for Android and Windows.</li></ul>|  
|Additional software|<ul><li>A third-party telephony or VoIP app such as Skype is required for placing calls from [!INCLUDE[prodshort](../developer/includes/prodshort.md)].</li><li>A third-party email program such as Outlook is required for sending emails from [!INCLUDE[prodshort](../developer/includes/prodshort.md)].</li><li>Microsoft Office 2016 or Microsoft Office 365 is required for sending data to Microsoft Excel or to Microsoft Word.</li></ul>|  
|Additional information|<ul><li>Device diagonal screen size 7” for tablets.</li><li>Screen resolution 960 × 510 for tablets.</li><li>Device diagonal screen size 4” for phones.</li><li>Screen resolution 854 x 480 for phones.</li></ul>|  

###  <a name="WinClient"></a> Dynamics NAV Client Requirements  
 The following table shows the minimum system requirements for using the Dynamics NAV Client to connect to [!INCLUDE[prodshort](../developer/includes/prodshort.md)].  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 Pro, Enterprise, or Education \(32-bit and 64-bit editions\).<br />**Important:** Windows 10 S is not supported.</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul>|  
|Hardware resources|<ul><li>Hard disk space: 200 MB.</li><li>Memory: 1 GB.</li></ul>|  
|Reports|<ul><li>For editing RDLC report layouts:<ul><li>Report Builder for SQL Server 2016 or Visual Studio 2017 with [Microsoft Rdlc Report Designer for Visual Studio](https://go.microsoft.com/fwlink/?linkid=857038) installed.</li></ul><li>For editing Word layouts:<ul><li>Microsoft Word 2016 or later</li></ul></ul>|  
|Outlook client integration and mail merge|<ul><li>Microsoft Office 365, Microsoft Office 2016.</li></ul>|  
|Import and export with Microsoft Excel and Office XML, and SharePoint links|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|  
|Editing in Excel using the Excel Add-in |<ul><li>Excel 2016.<br />For more information, see [Exporting Your Business Data to Excel](/dynamics365/business-central/about-export-data). For [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on-premises, see [Setting up the Excel Add-In for Editing Dynamics NAV Data](/dynamics-nav/configuring-dynamics-nav-excel-addin) since the same steps apply to [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on-premises.</li></ul>|  
|OneNote integration|<ul><li>Microsoft Office 2016 or Microsoft Office 365.</li></ul>|
|Email logging|<ul><li>Active Directory and Microsoft Exchange Server 2013.</li><li>Microsoft Exchange Online, or Exchange Online as part of an Office 365 subscription.</li></ul>|  
|Additional software|<ul><li>Microsoft .NET Framework 4.7.</li></ul>|  
|Additional information|<ul><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present in the target computer:<ul><li>Microsoft .NET Framework 4.7.</li></ul></li><li>The [!INCLUDE[prodshort](../developer/includes/prodshort.md)] is available in a 32-bit version and 64-bit version. On a 32-bit Windows operating system, the 32-bit version is run. On a 64-bit Windows operating system, the 64-bit version is run by default; however, you can also run the 32-bit version if it is required.</li><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] can only install the Excel Add-in if Excel is present on the target computer.</li><li>Outlook synchronization is not supported on 64-bit versions of Office.</li></ul>|  

###  <a name="DevEnv"></a> Dynamics NAV Development Environment Requirements  
 The following table shows the minimum system requirements for the [!INCLUDE[nav_dev_long](../developer/includes/nav_dev_long_md.md)].  

|||  
|-|-|  
|Supported operating systems|<ul><li> Windows 10 Pro, Enterprise, or Education \(32-bit and 64-bit editions\).</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul>|  
|Hardware resources|<ul><li>Hard disk space: 200 MB.</li><li> Memory: 1 GB.</li></ul>|  
|Reports|<ul><li>For creating and editing RDLC report layouts:<ul><li>Report Builder for SQL Server 2016, or</li><li>One of the following versions of Visual Studio:<ul><li>Visual Studio 2017 with [Microsoft Rdlc Report Designer for Visual Studio](https://go.microsoft.com/fwlink/?linkid=857038) installed.</li><li>Visual Studio 2015 Professional or Enterprise edition with SQL Server Data Tools installed.<br />**Important:**  Before you install Visual Studio 2015, install Microsoft .NET Framework 4.7; otherwise, an error will occur when you compile or run RDLC reports. For more information, see [Report error "Visual Basic Command Line Compiler has stopped working"](http://go.microsoft.com/fwlink/?LinkID=722862).</li></ul></li></ul></ul><ul><li>For upgrading reports:<ul><li>Report Builder for SQL Server 2016</li></ul><li>For creating Word report layouts:<ul><li>Word 2016 or later</li></ul></li></ul>|  
|Additional software|<ul><li>Microsoft .NET Framework 4.7.</li></ul>|  
|Additional information|<ul><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present in the target computer:<ul><li>Microsoft .NET Framework 4.7.</li><li>SQL Server Native Client 11.0.</li><li>Report Builder for SQL Server 2016. This is not installed if a version of SQL Server Report Builder or Microsoft Visual Studio is already present on the target computer</li></ul></li><li>If the [!INCLUDE[nav_dev_short](../developer/includes/nav_dev_short_md.md)] and [!INCLUDE[server](../developer/includes/server.md)] are on the same computer, then only a 64-bit operating system is supported.</li></ul>|  


## Server Components
###  <a name="NavServerReqs"></a> [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Server Requirements  
 The following table shows the minimum system requirements for [!INCLUDE[server](../developer/includes/server.md)].  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 Pro, Enterprise, or Education \(64-bit edition\).</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul>.|  
|Hardware resources|<ul><li>Hard disk space: 500 MB.</li><li>Memory: 2 GB.|  
|[!INCLUDE[crm](../developer/includes/crm_md.md)] integration|<ul><li>Windows Identity Framework.<br />     For a list of supported [!INCLUDE[crm](../developer/includes/crm_md.md)] versions, see [Microsoft Dynamics 365 for Sales Integration Requirements](system-requirements-for-business-central.md#CRM).|  
|Additional software|<ul><li>Microsoft .NET Framework 4.7.</li><li>Windows PowerShell 3.0.|  
|Additional information|<ul><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present on the target computer:<ul><li>Microsoft .NET Framework 4.7.</li><li>Windows Identity Framework.</li></ul></li></ul>|  

###  <a name="WebServer"></a> [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Web Server Components Requirements  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 Pro, Enterprise, or Education \(64-bit edition\).</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul>.|  
|Web server|<ul><li>Internet Information Server 10, Internet Information Server 8.5, or Internet Information Server 8.0.|   
|Additional software|<ul><li>Microsoft .NET Framework 4.7.</li><li>Windows PowerShell 3.0.|  
|Additional information|<ul><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present on the target computer.<ul><li>Microsoft .NET Core 1.0 Windows Server Hosting. This is installed by [!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] if not already present.</li><li>Microsoft .NET Framework 4.7.</li><li>Internet Information Server 10, Internet Information Server 8.5, or Internet Information Server 8.0, depending in the operating system, with the required features enabled.</li></ul></li><li>For more information about configuring IIS, see Configuring IIS](configure-iis.md)</li></ul>|  

###  <a name="SQLReq"></a>[!INCLUDE[prodshort](../developer/includes/prodshort.md)] Database Components for SQL Server Requirements  
 The following table shows the minimum system requirements for [!INCLUDE[prodshort](../developer/includes/prodshort.md)] database components for SQL Server.  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 Pro, Enterprise, or Education \(64-bit edition\).</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul> |  
|Hardware resources|For more information, see [Hardware and Software Requirements for Installing SQL Server 2016](http://go.microsoft.com/fwlink/?LinkId=622999). From this page, you can also access requirements for other versions of SQL Server.|  
|SQL Server|<ul><li>Microsoft SQL Server 2017 Express, Standard or Enterprise.</li> <li>Microsoft SQL Server 2016 Express, Standard or Enterprise.</li><li>Microsoft SQL Server 2014 Express, Standard or Enterprise.</li><li>Azure SQL Database V12 Standard and Premium service tiers.<br /><br />|  
|Service Packs and Cumulative Updates| Unless explicitly stated, all released Service Packs and Cumulative Updates of the above Microsoft SQL Server versions are supported. It is recommended to always be on the latest released Service Pack and Cumulative Update.|
|Additional information|[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present on the target computer:<ul><li>SQL Server 2016 Express \(64-bit edition\).<br>If the operating system on the target computer does not support SQL Server 2016 Express, Setup displays a pre-requisite warning. In this case you should exit Setup and then update the operating system on the computer to one that does support SQL Server 2016 Express. Then run Setup again.</li></ul>|  

###  <a name="HelpServer"></a> [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Help Server Requirements  
 The following table shows the minimum system requirements for the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Help Server.  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows 10 Pro, Enterprise, or Education \(64-bit editions\).</li><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Essentials \(64-bit edition\).</li></ul>|  
|Hardware resource|<ul><li>Hard disk space: 500 MB.</li><li>Memory: 2 GB.</li></ul>|  
|Web server|<ul><li>Internet Information Server 10, Internet Information Server 8.5, or Internet Information Server 8.0.</li></ul>|  
|Additional software|<ul><li>Microsoft .NET Framework 4.7.</li></ul>|  
|Additional information|<ul><li>[!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] installs the following software if it is not already present on the target computer.<ul><li>Microsoft .NET Framework 4.7.</li><li>Internet Information Server 10, Internet Information Server 8.5, or Internet Information Server 8.0. depending on the operating system, with the required features enabled.</li></ul></li><li>Windows Search must be enabled on the computer that you install the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Help Server on. If you install on Windows Server 2012 R2, and Windows Search is not enabled as a file service, [!INCLUDE[prodsetup](../developer/includes/prodsetup.md)] adds the service. However, the changes do not take effect until the computer has restarted.</li></ul>|  

## Additional Components and Features
###  <a name="ADCS"></a> Automated Data Capture System Requirements  
 The following table shows the minimum system requirements for Automated Data Capture System \(ADCS\) for [!INCLUDE[prodshort](../developer/includes/prodshort.md)].  

|||  
|-|-|  
|Additional software|<ul><li>MSXML version 6.0.</li><li>Telnet or Microsoft Windows HyperTerminal.</li><li>VT100 Plug-in for each computer on which you install ADCS.</li><li>Microsoft Loopback Adapter.</li></ul>|  
|Additional information|<ul><li>HyperTerminal is no longer included with Windows. For more information, see [What happened to HyperTerminal?](http://go.microsoft.com/fwlink/?LinkId=222571) in the Windows Help.</li><li>VT100 Plug-in acts as a virtual Telnet server.</li></ul>|  

###  <a name="BusInboxOutlook"></a> Business Inbox in Microsoft Outlook Requirements  
The following table shows the minimum system requirements for using [!INCLUDE[prodshort](../developer/includes/prodshort.md)] as your business inbox in Outlook.

|||  
|-|-|  
|Supported Outlook Applications |<ul><li>Outlook 2016 or later</li><li>Outlook Web App</li><li>OWA for iPad</li><li>OWA for iPhone</li><li> OWA for Android.</li></ul>|
|Supported Exchange Servers|<ul><li>Exchange Online</li><li>Exchange Server 2016</li><li>Exchange Server 2013.<br />In deployments that use Exchange Server, the Exchange PowerShell endpoint must be accessible by [!INCLUDE[server](../developer/includes/server.md)].</li></ul>|
|Supported Authentication|<ul><li>The [!INCLUDE[server](../developer/includes/server.md)] must be configured to run with NavUserPassword, ACS, or AAD Credentials Type.<br /> Also, the [!INCLUDE[nav_web_md](../developer/includes/nav_web_md.md)] must be configured for Secure Sockets Layer (SSL).</li></ul>|
|Supported Browsers|<ul><li>When using the Outlook Web App (OWA), your computer must be running a supported browser listed in the [!INCLUDE[nav_web_md](../developer/includes/nav_web_md.md)] Requirements.</li></ul>|
|Supported Operating Systems|<ul><li>When using OWA for iPad, OWA for iPad, or OWA for Android, your mobile device must use a supported Operating System listed in [!INCLUDE[nav_uni_app_md](../developer/includes/nav_uni_app_md.md)] Requirements.</li></ul>|  

###  <a name="Outlook"></a> Microsoft Outlook Add-In Requirements  
The following table shows the minimum system requirements for the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Add-In for Outlook for synchronization with Outlook.

|||  
|-|-|  
|Supported Outlook Applications |<ul><li>Outlook 2016</li></ul>|
|Supported Exchange Servers|<ul><li>Exchange Server 2016</li><li>Exchange Server 2013</li><li>Exchange Online.</li></ul>|  


##  <a name="CRM"></a> Microsoft Dynamics 365 for Sales Integration Requirements  
 The following table shows the system requirements for integrating [!INCLUDE[prodshort](../developer/includes/prodshort.md)] with [!INCLUDE[crm](../developer/includes/crm_md.md)].  

|||  
|-|-|  
|Microsoft Dynamics CRM versions|<ul><li>Microsoft Dynamics CRM 2015 or Microsoft Dynamics CRM 2016<BR />Note: AD, IFD and Claims authentication types are supported for above editions.</li><li>Microsoft Dynamics CRM Online 2015, Microsoft Dynamics CRM Online 2015 Update 1, or Microsoft Dynamics CRM Online 2016 Update 1 or Microsoft Dynamics 365<BR />Note: Oauth and Office365 authentication types are supported for these editions.</li></ul>For more details on authentication types, see [Connection strings in XRM tooling to connect to Dynamics 365](https://msdn.microsoft.com/en-us/library/mt608573.aspx).|
|[!INCLUDE[prodshort](../developer/includes/prodshort.md)] Integration Solution (.zip)|For Dynamics CRM 2015, Dynamics CRM Online 2015, and Dynamics CRM Online 2015 Update 1:<ul><li>Use the DynamicsNAVIntegrationSolution.zip file that is found on the Dynamics NAV 2016 installation media (DVD) to install the solution.</li><li>Item Availability is not supported on Dynamics CRM 2015, versions Update 1 and Online.</li></ul>For more information, see [How to: Prepare Dynamics 365 for Sales for Integration](How-to-prepare-Dynamics-CRM-for-Integration.md).      |  

###  <a name="SharePointApp"></a>[!INCLUDE[prodshort](../developer/includes/prodshort.md)]as an App for SharePoint Requirements  
 The following table shows the minimum system requirements for [!INCLUDE[prodshort](../developer/includes/prodshort.md)] as an App for SharePoint.  

|||  
|-|-|  
|Supported operating systems|<ul><li>Windows Server 2016 Standard, Essentials, or Datacenter.</li><li>Windows Server 2012 R2 Standard or Datacenter \(64-bit edition\).</li></ul>|  
|Additional software|<ul><li>SharePoint 2013 Service Pack 1.</li><li>SharePoint Online.</li></ul>|  

<!--
###  <a name="Azure"></a> Automated Deployment on Microsoft Azure Requirements  
 Automated deployment of [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on Microsoft Azure by using the [!INCLUDE[nav_prov_short](../developer/includes/nav_prov_short_md.md)] is only supported on Azure virtual machines that are running Windows Server 2012. For additional requirements for specific [!INCLUDE[prodshort](../developer/includes/prodshort.md)] components, refer to the other sections in this topic. 

--> 

## See Also
[Welcome to the Developer and IT-Pro Help for Business Central](./index.md)  
[Product and Architecture Overview](product-and-architecture-overview.md)  
[Deployment](Deployment.md)  
