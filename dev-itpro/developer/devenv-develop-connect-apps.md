---
title: "Getting Started Developing Connect Apps for Dynamics 365 Business Central"
author: SusanneWindfeldPedersen
ms.author: solsen
ms.custom: na
ms.date: 05/24/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
---

[!INCLUDE[d365fin_dev_blog](includes/d365fin_dev_blog.md)]

# Getting Started Developing Connect Apps for [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)]
A Connect app establishes a point-to-point connection between [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] and a 3rd party solution or service and is typically created using standard REST API to interchange data. Any coding language capable of calling REST APIs can be used to develop your Connect app. In the following section you can read about how you get started exploring the available APIs for [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)].

To explore and develop against APIs in [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)], you must first sign up for a trial tenant and then you have to connect and authenticate. To do that, follow the steps below.

1. Sign up for [Dynamics 365 Business Central](https://signup.microsoft.com/signup?sku=6a4a1628-9b9a-424d-bed5-4118f0ede3fd&ru=https%3A%2F%2Fbusinesscentral.dynamics.com%2FSandbox%2F%3FredirectedFromSignup%3D1).  
When you have your tenant, you can sign into the UI to play with the product, as well as [explore the APIs](/dynamics-nav/fin-graph/)
2. There are two different ways to connect to and authenticate against the APIs.  
    - Use Azure Active Directory (AAD) based authentication against the common API endpoint: https://api.businesscentral.dynamics.com/v1.0/api/beta
    - Use basic authentication with username and password (a so-called web service access key) against the common API endpoint that includes the user domain, for example https://api.businesscentral.dynamics.com/v1.0/cronus.com/api/beta.  
        > [!IMPORTANT]  
        > When going into production, you must use Azure Active Directory (AAD)/OAuth v2 authentication and the common endpoint https://api.businesscentral.dynamics.com/v1.0/api/beta. For exploring and initial development, you can use basic authentication. In the simple **Hello World** example below, we are going to use basic authentication, as it is a bit faster to get up and running.

In the following sections you can read more about setting up the two types of authentication.

## Setting up Azure Active Directory (AAD) based authentication
Sign in to the [Azure Portal](https://portal.azure.com) to register [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] as an app and thereby provide access to [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] for users in the directory.

1. Follow the instructions in the [Integrating applications with Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications) article. The next steps elaborate on some of the specific settings you must enable.
2. During the registration of the app, make sure to go to **Settings**, and then under **API ACCESS**, choose **Required permissions**.
3. Choose **Add**, and then under **Add API Access**, choose **Select an API** and search for the **Dynamics 365** option.  
    > [!NOTE]  
    > If **Dynamics 365** does not show up in search, it's because the tenant does not have any knowledge of Dynamics 365. To make it visible, an easy way is to register for a [free trial](https://signup.microsoft.com/signup?sku=6a4a1628-9b9a-424d-bed5-4118f0ede3fd&ru=https%3A%2F%2Fbusinesscentral.dynamics.com%2FSandbox%2F%3FredirectedFromSignup%3D1) for [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] with a user from the directory. 
4. Choose **Dynamics 365** and select **Delegated permissions**, and then choose the **Done** button.
5. Again, under **Settings**, now choose **Keys** and enter a **Description** for the new key, and then choose the expiration of the key. 
6. Choose **Save**, and then copy the generated key from the **Value** field.  
    > [!NOTE]  
    > Remember to copy the key, as it will only be visible once.

You have now set up the AAD based authentication. Next, you can go exploring the APIs, see the [Exploring the APIs with Postman](devenv-develop-connect-apps#exploring-the-apis-with-postman) section below.

## Setting up basic authentication
If you prefer to set up an environment with basic authentication just to explore the APIs, you can skip setting up the AAD based authentication for now and proceed with the steps below. If you, however, want to go into production, you must use AAD/Oauth v2 authentication, see the section above **Setting up Azure Active Directory (AAD) based authentication**.

1. To set up basic authentication, log into your tenant, and in the **Search** field, enter **Users** and then select the relevant link.
2. On the **Users** page, in the **Web Service Access Key** field, generate a key.  
3. Copy the generated key and use it as the password for the username. 

Now that we have the username and password, we can connect and authenticate. You can do this from code, or API explorers such as Postman or Fiddler. In the [Exploring the APIs with Postman](devenv-develop-connect-apps#exploring-the-apis-with-postman) section we will use Postman.

## Exploring the APIs with Postman
In this `Hello World` example, we are going over the basic steps required to retrieve the list of customers in our trial tenant. This example is based on running with basic authentication. 

1.	First, in Postman, set up a `GET` call to the base API URL.  
    - When you call the base API URL, you will get a list of all the available APIs. You can append `$metadata` to the URL to also get information about the fields in the APIs. The list of supported APIs and fields information can also be found in the API documentation.

    - Since we are using basic authentication, we need to include the users domain in the URL, for example, call `GET https://api.businesscentral.dynamics.com/v1.0/myusersdomain.com/api/beta`
    
2. On the **Authorization** tab in Postman select **Basic Auth** in the **Type** and provide the Username and **Web Service Access Key** from above as password. 

3. Choose **Send** in Postman to execute the call, and inspect the returned body, which should include a list of the APIs.
    
Each resource is uniquely identified through an ID, see the following example of calling `GET <endpoint>/companies`:  

    ``` 
    {
        "@odata.context": "<endpoint>/$metadata#companies",
        "value": [
            {
                "id": "bb6d48b6-c7b2-4a38-9a93-ad5506407f12",
                "systemVersion": "18453",
                "name": "CRONUS USA, Inc.",
                "displayName": "CRONUS USA, Inc.",
                "businessProfileId": ""
            }
        ]
    }
    ```


The resource ID must be provided in the URL when trying to read or modify a resource or any of its children. The ID is provided in parenthesis () after the API endpoint. For example, to GET the “CRONUS USA, Inc.” company details, you must call `<endpoint>/companies(bb6d48b6-c7b2-4a38-9a93-ad5506407f12)/`.

All resources, such as customers, invoices etc., live in the context of a parent company, of which there can be more than one in the [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] tenant. Therefore, it is a requirement to provide the company ID in the URL for all resource API calls. To GET all customers in the “CRONUS USA, Inc.” company, we must call a GET on the URL `<endpoint>/companies(bb6d48b6-c7b2-4a38-9a93-ad5506407f12)/customers`.

## See Also
[Using Deltas With APIs](devenv-connect-apps-delta.md)  
[Using Filtering With APIs](devenv-connect-apps-filtering.md)  
[Tips for Working with APIs](devenv-connect-apps-tips.md)