---
title: Configure the Help experience
description: Learn how to give your customers access to the right Help content.
author: edupont04
ms.custom: na
ms.reviewer: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.date: 03/08/2019
ms.author: edupont
---

# Configuring the Help Experience for [!INCLUDE[prodlong](../developer/includes/prodlong.md)]

The default version of [!INCLUDE[prodshort](../developer/includes/prodshort.md)] comes with conceptual overviews and other articles that publish to the [https://docs.microsoft.com/dynamics365/business-central/](https://docs.microsoft.com/en-us/dynamics365/business-central/) site. This location is then accessible from the Help menu and through the Learn More links in all tooltips. Each extension that you add will include its own tooltips and links to Help. But what if you want to deploy [!INCLUDE[prodshort](../developer/includes/prodshort.md)] locally? Or if you have a vertical solution so that you want to refer your customers to your own website for Help? Or if you have a legacy Help collection based on the Dynamics NAV Help Server?  

These and other scenarios are also supported in [!INCLUDE[prodshort](../developer/includes/prodshort.md)]. But the options and possibilities are different, depending on your deployment scenario.  

## Apps for online tenants

When you build an app for in[!INCLUDE [prodshort](../developer/includes/prodshort.md)] using the AL developer experience, you are expected to comply with the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] user assistance model. This includes tooltips and context-sensitive links to Help.  

For more information, see [User Assistance Model](../user-assistance.md) and [Configure Context-Sensitive Help](../help/context-sensitive-help.md).  

## On-premises deployments

For deploying [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on-premises, you must choose between using the legacy Dynamics NAV Help Server or an online website. Help Server is a simple website that requires your Help to be in a specific format (HTML files), and the online website can host any content that you want to make available. Your choice depends on the concrete needs of your solution and your users.  

> [!IMPORTANT]
> You can configure each client to use either an online library or Help Server. If you add configuration for an online library, you must remove the settings for Help Server.  

### Online library

If you want to use a website that is not based on Help Server, then you must specify the URL in the settings for the Web client and the Windows client, if your company uses this legacy client. The website does not have to be publicly accessible, but it must be accessible to all users of the solution that it support.  

For the Web client, which is accessed by users from a browser or from the mobile apps, the navsettings.json file must contain the following settings:

```json
    "//BaseHelpUrl":  "The location of Help for this application.",
    "BaseHelpUrl": "https://mysite.com/{0}/documentation/",
    "//BaseHelpSearchUrl":  "The URL to use if Help is included in the Search functionality in Business Central.",
    "BaseHelpSearchUrl": "https://docs.microsoft.com/{0}/search/index?search={1}&scope=BusinessCentral",
    "//DefaultRelativeHelpPath":  "The Help article to look up if no other article can be found.",
    "DefaultRelativeHelpPath": "index",
```

For users who use the legacy Windows client connected to [!INCLUDE[prodshort](../developer/includes/prodshort.md)], the ClientUserSettings.config file must contain the following settings:

```
    <add key="BaseHelpUrl" value="https://mysite.com/{0}/documentation/" />
    <add key="DefaultRelativeHelpPath" value="index" />
```

> [!NOTE]
> Replace the value of the BaseHelpUrl key with the URL for your own website, such as `https://mysite.com/{0}/documentation/`. The parameter, {0}, represents the locale of the browser that the user is using, such as en-us or da-dk, and is set automatically at runtime.

### Help Server

If you want to use Help Server, then you must specify the server and port in the installation options. The Help Server website can also serve as a starting point for adding a library to your existing website, for example.  

For the Web client, which is accessed by users from a browser or from the mobile apps, the navsettings.json file must contain the following settings:

```json
    "//HelpServer": [
        "Name of the Dynamics NAV Help Server to connect to."
        ],
    "HelpServer": "https://myserver.com",
    "//HelpServerPort":  "The listening TCP port for the Dynamics NAV Help Server. Valid range: 1-65535",
    "HelpServerPort": "49000",
```

For users who use the legacy Windows client connected to [!INCLUDE[prodshort](../developer/includes/prodshort.md)], the ClientUserSettings.config file must contain the following settings:

```
    <add key="HelpServer" value="https://myserver.com" />
    <add key="HelpServerPort" value="49000" />
```

In both examples, *https://myserver.com* represents the URL to the Help Server instance. For more information, see [Configuring Microsoft Dynamics NAV Help Server](/dynamics-nav/configuring-microsoft-dynamics-nav-help-server) in the developer and ITpro content for [!INCLUDE[navnow_md](../developer/includes/navnow_md.md)].  

> [!IMPORTANT]
> If you use Help Server, the UI-to-Help mapping functionality that is described in [Configure Context-Sensitive Help](../help/context-sensitive-help.md) does not work. Instead, you must rely on the legacy Help lookup mechanism that hinges on .HTM files with filenames that reflect the object IDs, such as N_123.htm for the page object with the ID 123. For more information, see [Working with Dynamics NAV Help Server](/dynamics-nav/microsoft-dynamics-nav-help-server?target=_blank).  

For guidance about how to generate HTML files, see the [Readme.md in the public source repo for the business functionality content](https://github.com/MicrosoftDocs/dynamics365smb-docs?target=_blank#building-html-files). Optionally, you can choose to reuse the HTML and .HTM files that you used for Dynamics NAV in your online library or Help Server deployment.  

## Fork the Microsoft repos

If you want to customize or extend the Microsoft Help, you can fork our public repo for either the source repo in English (US) at [https://github.com/MicrosoftDocs/dynamics365smb-docs](https://github.com/MicrosoftDocs/dynamics365smb-docs), or one of the related repos with translations into the supported languages. For more information, see [Extend, Customize, and Collaborate on the Help](../help/contributor-guide.md).  

## See Also

[User Assistance Model](../user-assistance.md)  
[Adding Help Links from Pages, Reports, and XMLports](../developer/devenv-adding-help-links-from-pages-tables-xmlports.md)  
[Working with Dynamics NAV Help Server](/dynamics-nav/microsoft-dynamics-nav-help-server)  
[Configuring Microsoft Dynamics NAV Help Server](/dynamics-nav/configuring-microsoft-dynamics-nav-help-server)  
[Migrate Legacy Help to the Business Central Format](../upgrade/migrate-help.md)  
[Development of a Localization Solution](../developer/readiness/readiness-develop-localization.md)  
[System Requirements](system-requirement-business-central.md)  
[Resources for Help and Support](../help-and-support.md)  
[Blog post: Extending and customizing the Help](https://community.dynamics.com/business/b/businesscentraldevitpro/archive/2018/12/11/extending-and-customizing-help)  
[Blog post: Collaborate on content for Business Central](https://community.dynamics.com/business/b/businesscentraldevitpro/archive/2018/12/15/collaborate-on-content-for-business-central)  
[Docs Contributor Guide](/contribute/)  
[Docs Authoring Pack for Visual Studio Code](/contribute/how-to-write-docs-auth-pack)  
