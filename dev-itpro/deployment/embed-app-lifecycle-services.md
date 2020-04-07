---
title: "Lifecycle Services for Embed App"
author: jswymer

ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: jswymer
ms.date: 04/06/2020
---

# Managing an [!INCLUDE [prodshort](../developer/includes/prodshort.md)] [!INCLUDE[embed app](../developer/includes/embedapp.md)] in Microsoft Lifecycle Services

Microsoft provides essential functionality within [Microsoft Lifecycle Services](https://lcs.dynamics.com/v2) collaboration portal (LCS) to support qualified ISVs in managing the [!INCLUDE[embedapp](../developer/includes/embedapp.md)] based on [!INCLUDE [prodshort](../developer/includes/prodshort.md)] online.  

## Creating LCS project

In LCS, you should create a project for each [!INCLUDE[embedapp](../developer/includes/embedapp.md)] and each country you would like to deploy to [!INCLUDE [prodshort](../developer/includes/prodshort.md)] service. You provide the list of countries where you want to run your Embed app during onboarding. You can only deploy your solution to the country that is already supported in the Business Central online service. Find the list of supported countries here: https://aka.ms/bccountries. 

Before you can create a project, you need to unlock a corresponding Private Preview feature. Once you sign in to LCS, click on the **Preview feature management** action. Then on the Preview feature management page, select the "+" action to add a new preview feature using a preview code. In the **Preview code** field, enter the code you received from Microsoft during onboarding. You should now see the "Microsoft Dynamics 365 Business Central (SaaS)" feature on the list of the Private preview features on this page.     

> [!IMPORTANT] Even though the project will be created by one user, every user you are planning to add to your LCS project will have to activate the "Microsoft Dynamics 365 Business Central (SaaS)" feature using the same preview code you received from Microsoft. Without this activation, the users you add to your LCS project will run into permissions issues when trying to open the LCS project that you created. 

Navigate back to the main page and start creating a new project by selecting the "+" action. Choose **Migrate, create solutions, and learn** category as the purpose of the project. On the next page, provide the project name. 

> [!NOTE]
> You will have to create a separate project for each country, even if your Embed app is going to be exactly the same. Therefore we recommend that you use the name of your Embed app appended by the country code as the name of your project, for example "Fabrikam Rentals, DK", "Fabrikam Rentals, US" and so on.

Next, provide a short description for your project (optional), select **Microsoft Dynamics NAV** as the product name and **Microsoft Dynamics 365 Business Central (SaaS)** as the product version. Select the **Create** button to complete creation of the project. 

After you create the project, send its ID to the e-mail alias specified on the main project page for whitelisting purposes. You can find the project ID in the URL displayed in your browser, such as `https://lcs.dynamics.com/V2/NavProjectDashboard/[projectID]`

## Uploading deployment package

Once your LCS project ID has been whitelisted by Microsoft, you can continue to upload the [!INCLUDE[embedapp](../developer/includes/embedapp.md)] deployment package into the Asset library. <!-- COMMENTED OUT UNTIL THE FILE IS FOUND You can read more about the the content and structure of the deployment package [here]: https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/embedapps/embed-app-deployment-package.--> 

In your LCS project, select the **Asset library** action to navigate to the Asset library page. Then, select the **+** action to open the **Upload Software deployable package file** wizard. Provide the **Name** and **Description** (optional) for your package. The asset name you provide here will be displayed on the Application Version list inside your project. Select the Add the file action to select and upload the deployment package. Wait for the package to get uploaded and select the Confirm button to close the upload wizard.  

## Deploying the Embed app

To deploy the package you uploaded in the **Asset library**, do these steps:

1. Go to the **Rings** section of your project.
2. Select **Maintain** menu, then select **Deploy** action to open the **Deploy package** wizard.
3. Select the package you want to deploy in the **Package name** field.
4. Select the **Target platform**, then select **Deploy** button to start the deployment. 

> [!IMPORTANT]
> The [!INCLUDE [prodshort](../developer/includes/prodshort.md)] platform is updated monthly. You are responsible for updating the Embed App to operate with the updated version of Business Central. The Embed App must run on a supported build of Business Central, for example, the current version of Business Central or one of the two immediately preceding versions. The immediately preceding versions can be both minor and major versions of Business Central. The list of supported versions is displayed in the LCS portal on the **Deploy package wizard** in the **Target platform** field. The versions, which aren't displayed on that list are out of support. You customers running on these versions can't be serviced at the service levels set forth in the published [Service Level Agreement](https://www.microsoft.com/licensing/product-licensing/products). 

After the Environment is successfully provisioned, its status on the list of application versions will be set to **Deployed**. To allow sign-ups to be directed to this application version, you select the **Use for new tenants** check box. You can only have one application version marked this way at a time. 

## Onboarding customers and creating environments

It isn't possible to create environments and add customers in LCS. The customers are onboarded the same way as they're onboarded to the [!INCLUDE [prodshort](../developer/includes/prodshort.md)] service - via the Partner Center. Also no special licenses are used for the Embed apps customers. Use the same licenses and subscriptions that are available for [!INCLUDE [prodshort](../developer/includes/prodshort.md)] itself. You can find more details [here](../administration/get-started-online.MD)].  

Once you've established the reseller relationship with the customer and added [!INCLUDE [prodshort](../developer/includes/prodshort.md)] subscriptions with required number of licenses for them, you must use your own branded Embed app URL to sign in their environment and [!INCLUDE [prodshort](../developer/includes/prodshort.md)] Administration center.

To create a new production environment for your customers, go to this URL:

```http
https://[your application family].bc.dynamics.com/[Customer's Azure AD Tenant ID]/Production 
```

To open your customer's [!INCLUDE [prodshort](../developer/includes/prodshort.md)] Administration center, go to this URL:

```http
https://[your application family].bc.dynamics.com/[Customer's Azure AD Tenant ID]/admin
```

Each environment that you signed up for the [!INCLUDE[embedapp](../developer/includes/embedapp.md)] is then displayed on the Tenant list part in your LCS project. On this part, you can find more details about the environment, including the name and the URL to sign in to each one. You can see which environments are running on which application version by selecting application version on the list.  

## Monitoring the Embed app

In the LCS portal, you get access to various logs for the activities that you do in the portal:

- Deployment: logs of deployment of the application versions 
- Tenant provisioning: logs of creation of the new customer environments   
- Tenant upgrades: logs of customer environments upgrades  
- Application errors: errors that are displayed to the customers when they work with the Embed app functionality

To get to these logs, in the Rings section of your project, select **Maintain** menu and then select **Monitor** action.  

On the **Ring monitoring** page, first select the **Category**, depending on the operation for which you want to retrieve the logs. Then set the **Period (min)** field to the number of minutes back in time, for which you want to see the logs. Don't use the **All** category.

> [!NOTE]
> The logs typically appear in LCS with a delay of 15 minutes. 

For easier troubleshooting, we recommend exporting the logs to a CSV file, using **Export to CSV** action, and then analyzing them in Microsoft Excel instead.  

It's important to always review the logs before submitting any issues to Microsoft. When reporting issues, attach the relevant logs in TXT or CSV format, don't use screenshots. 
 

## See Also

[[!INCLUDE[embedapp](../developer/includes/embedapp.md)] Overview](embed-app-overview.md)  
[Licensing in Dynamics 365 Business Central](licensing.md)  
[Components and Capabilities](app-components.md)  
[Microsoft Responsibilities for Apps on Business Central online](microsoft-responsibilities.md)  
[Preparing Demonstration Environments of [!INCLUDE[prodlong](../developer/includes/prodlong.md)]](../administration/demo-environment.md)  
[Preparing Test Environments of [!INCLUDE[prodlong](../developer/includes/prodlong.md)]](../administration/test-environment.md)  
