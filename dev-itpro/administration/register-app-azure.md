---
title: "Register on-premises as an app in the Azure Management Portal"
author: jswymer
ms.author: jswymer
ms.custom: na
ms.date: 08/10/2020
ms.reviewer: na
ms.service: "dynamics365-business-central"
ms.topic: article
---

# Registering Business Central On-Premises in Azure AD for Integrating with Other Services

> **APPLIES TO** [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises. [!INCLUDE [prodshort](../developer/includes/prodshort.md)] online is automatically configured for integration with other online services.

This article describes how to set up [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises to use services that are based on Microsoft Azure. There are several services that you can integrate with [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises, like Cortana Intelligence and Power BI. Before using the services, you have to register Business Central on-premises in Azure Active directory and give it access to the services. For example, the [Sales and Inventory Forecast](https://docs.microsoft.com/dynamics365/business-central/ui-extensions-sales-forecast) extension requires that you specify an API key and API URI. Other services require similar information.

> [!NOTE]
> In [!INCLUDE [prodshort](../developer/includes/prodshort.md)] version earlier than 16.4, the **Set up Azure Active Directory** wizard has an **Auto register** action. Previously, you could use this action to automatically register [!INCLUDE [prodshort](../developer/includes/prodshort.md)] in Azure AD. The auto-register functionality has since been removed. Now, you must register the application manually, regardless of your version. The wizard in earlier versions still includes the **Auto register** link. But the link now opens this article, which guides you through the manual registration.

## Prerequisites

- [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises is configured to use Azure Active Directory (AD) authentication.

    For more information, see [Authenticating [!INCLUDE[prodshort](../developer/includes/prodshort.md)] Users with Azure Active Directory](authenticating-users-with-azure-active-directory.md)
- An Azure AD account

    In most cases, this account is the same as your Business Central account. You'll use this account to access Azure Active AD tenant via the Azure portal.

## Register an application in Azure Active Directory

The first task is to use Azure portal to register an application for Business Central on your Azure AD tenant. As part of the registration, you'll also give the relevant services access to the application. The purpose of registration is to ensure [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises and the services to know each other's Azure Active Directory (Azure AD) details.

> [!TIP]
> The following steps describe how to register a new application. However, because you're using Azure AD authentication, you already have a registered application for [!INCLUDE [prodshort](../developer/includes/prodshort.md)]. So instead of registering a new application, you can use the existing application. But if you do, make sure you modify it based on the information in the steps that follow. 

1. Sign in to the [Azure portal](https://portal.azure.com) and register an application for [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises in Azure Active Directory tenant.

    1. Follow the general guidelines at [Register your application with your Azure Active Directory tenant](/azure/active-directory/active-directory-app-registration).

        When you add an application to an Azure AD tenant, you must specify the following information:
    
        |Setting|Description|
        |-------|-----------|
        |Name|Specify a name for your Business Central on-premises solution, such as *Business Central on-premises* or *Azure Services for Business Central on-premises*. |
        |Supported account types| Select <strong>Accounts in any organizational directory (Any Azure AD directory - Multitenant)</strong> |
        |Redirect URI|Set the first box to **Web** to specify a web application. Enter the URL for your Business Central on-premises browser client, followed by *OAuthLanding.htm*. For example, *https://MyServer:8080/BC160/OAuthLanding.htm*. This file is used to manage the exchange of data between Business Central on-premises and other services through Azure AD.|
    
        When completed, an **Overview** displays in the portal for the new application.

    2. Copy the **Application (Client) ID** that was assigned the application and also redirect URL that you specified. You'll use this information later.
2. Create a client secret for the registered application.

    1. Follow the general guidelines at [Add credentials to your web application](https://docs.microsoft.com/azure/active-directory/develop/quickstart-configure-app-access-web-apis#add-credentials-to-your-web-application).

    2. Before you leave the **Certificates & secrets** page, copy the secret's value to a temporary location. The value isn't accessible once you leave the page. You'll use this key later in your client application code.

3. Grant the registered application delegated permission to access the required service APIs, like Power BI.

    Follow the general guidelines at [Add permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/quickstart-configure-app-access-web-apis#add-permissions-to-access-web-apis) for each service.

    Use the following table to help you set the minimum permissions:

    |API / Permission name|Type|Description|
    |---------------------|----|-----------|
    |Microsoft Graph / User.Read|Delegated|Sign in and read user profile|
    |Power BI Service / Report.Read.All|Delegated|View all reports|

## Set up the registered application in Business Central

After you register the application, the next task is to configure the Business Central tenant to use the application. You'll need the information about the application that you created in the previous task: redirect URL, application (client) ID, and client secret.

1. In the top-right corner, choose the ![Tell me](../developer/media/search-icon.png "Tell me what you want to do") icon, enter **Assisted Setup**, and then choose the related link.
2. Select **Set up Azure Active Directory**, then **Next**.

    The **Connect With Azure** page opens.

    ![Setting the Azure Active Directory](../developer/media/set-up-azure-ad.png)
3. In the **Redirect URL** field, make sure the URL matches the redirect URL that's assigned the registered Business Central application in Azure AD.
4. In the **Application ID** field, specify the application (client) ID of the Business Central application in Azure AD that you copied in the previous task.
5. In the **Key** field, specify the value of the client secret used by the Business Central application in Azure AD.
6. Choose **Next**. Unless you see an error message, you're now done.

The [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises solution is registered and ready to connect to services such as Cortana Intelligence, or embedding Power BI in [!INCLUDE [prodshort](../developer/includes/prodshort.md)].  

## Fixing problems

This section provides solutions to problems that might occur.

### Sorry, but we're having trouble signing you in

When you try to connect, you get a message similar to the following:  

**AADSTS50011: The reply URL specified in the request does not match the reply URLs configured for the application: '1111111-aaaa-2222-bbbb-333333333333'**

To fix this issue, verify that the **Reply URL** in the Setup Azure AD page is correct. It must match the Reply URL set on the registered app in Azure AD.

## See Also
[Enabling Your Business Data for Power BI](https://docs.microsoft.com/dynamics365/business-central/admin-powerbi)  
[FAQ about Connecting to the Intelligent Cloud from On-Premises Solutions](FAQ-Intelligent-Cloud.md)  
[Deployment of [!INCLUDE[prodlong](../developer/includes/prodlong.md)]](../deployment/Deployment.md)  
[Migrating On-Premises Data to Business Central Online](migrate-data.md)  
