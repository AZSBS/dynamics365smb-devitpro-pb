---
title: "Testing the Application Overview"
ms.custom: na
ms.date: 08/26/2019
ms.reviewer: solsen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: "dynamics365-business-central"
author: jswymer
---

# Testing the Application Overview

Before you release your [!INCLUDE[prodshort](includes/prodshort.md)] application, you should test its functionality to ensure it works as expected. Testing is an iterative process. It's important to create repeatable tests, and helpful to create tests that can be automated. This article describes the features in [!INCLUDE[prodshort](includes/prodshort.md)] that help you test the business logic in your application, and it provides some best practices for testing. 

For a walkthrough concerning advanced extension testing, see [Testing the Advanced Extension Sample](devenv-extension-advanced-example-test.md).

[!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] includes the below features to help you test your application.

> [!IMPORTANT]
> Running automated tests is only possible with a Partner or Application Builder license.

With a customer license, you can't run Business Central test toolkit objects. These objects have IDs the range 130000-139999. If you only have a customer license, talk to your partner about the Application Builder and Solution Developer modules. As a partner, you should write your tests to use codeunit **132217 Library - Lower Permissions** to simulate licenses.

## Test Codeunits and Test Methods 

You write tests as AL code in methods of codeunits that are configured to be test codeunits. Test condunits hae the [SubType Property](properties/devenv-subtype-codeunit-property.md) set to **Test**. There are three types of methods that you can add in a test codeunit: test, handler, and normal. Each method type is used for a specific  purpose and behaves differently. When a test codeunit runs, it executes the **OnRun** trigger, and then executes each test method in the codeunit. The outcome of a test method is either SUCCESS or FAILURE.

For more information about test codeunits and test methods, see [Test Codeunits and Test Methods](devenv-test-codeunits-and-test-methods.md).

## Test Runner Codeunits
  
You use test runner codeunits to manage the execution of test codeunits and to integrate with other test management, execution, and reporting frameworks. By integrating with a test management framework, you can automate your tests and enable them to run unattended.  

Test runner codeunits are codeunits that have the [SubType Property](properties/devenv-subtype-codeunit-property.md) set to **TestRunner**.

Test runner codeunits include the following triggers:  

-   [OnRun Trigger](triggers/devenv-onrun-trigger.md) 

-   [OnBeforeTestRun Trigger](triggers/devenv-OnBeforeTestRun-Trigger.md)  

-   [OnAfterTestRun Trigger](triggers/devenv-OnAfterTestRun-Trigger.md)  

 In the **OnRun** trigger you enter the code to run the codeunits. It runs when you execute the codeunit and before the test methods run. You can use the **OnBeforeTestRun** and the **OnAfterTestRun** triggers to perform preprocessing and postprocessing, such as initialization or logging test results.  

For more information about test runner codeunits, see [Test Runner Codeunits](devenv-testrunner-codeunits.md).

## Test Pages  
Test pages mimic actual pages but do not present any UI on a client computer. Test pages let you test the code on a page by using AL to simulate user interaction with the page.  

There are two types of test pages:  

- TestPage, which is a regular page and can be any kind of page. This includes page parts or subpages.  

- TestRequestPage, which represents the request page on a report.  

You can access the fields on a page and the properties of a page or a field by using the dot notation. You can open and close test pages, perform actions on the test page, and navigate around the test page by using AL methods. For more information, see [Testing Pages](devenv-testing-pages.md).

## UI Handlers
To create tests that can be automated, you must handle cases when user interaction is requested by code that is being tested. UI handlers run instead of the requested UI. UI handlers provide the same exit state as the UI. For example, a method that has the [ConfirmHandler Attribute](methods/devenv-confirmhandler-attribute.md) set handles [CONFIRM Method](methods-auto/dialog/dialog-confirm-method.md) calls. If code that is being tested calls the [CONFIRM Method](methods-auto/dialog/dialog-confirm-method.md), then the **ConfirmHandler** method is called instead of the [CONFIRM Method](methods-auto/dialog/dialog-confirm-method.md). You write code in the **ConfirmHandler** method to verify that the expected question is displayed by the [CONFIRM Method](methods-auto/dialog/dialog-confirm-method.md) and you write AL code to return the relevant reply. 

You create a specific handler for each page that you want to handle and a specific report handler for each report that you want to handle.  

If you run a test codeunit from a test runner codeunit, then any unhandled UI in the test methods of the test codeunit causes a failure of the test. If you do not run the test codeunit from a test runner codeunit, then any unhandled UI is displayed as it typically would. 

For more information, see [Creating Handler Methods](devenv-creating-handler-methods.md). 

## ASSERTERROR Keyword
You use `AssertError` statements in test methods to test how your application behaves under failing conditions. These are called positive and negative tests. The `AssertError` keyword specifies that an error is expected at run time in the statement that follows the `AssertError` keyword.

If a simple or compound statement that follows the `AssertError` keyword causes an error, then execution successfully continues to the next statement in the test method. You can get the error text of the statement by using the [GETLASTERRORTEXT Method](methods-auto/system/system-getlasterrortext-method.md).

If a statement that follows the `AssertError` keyword does not cause an error, then the `AssertError` statement causes the following error and the test method that is running produces a FAILURE result.

### Example  
To create a test method to test the result of a failure of a CheckDate method that you have defined, you can use the following code. This example requires that you create a method called CheckDate to check whether the date is valid for the customized application and that you create the following text constant and the *Date* variable InvalidDate and the *Text* variable InvalidDateErrorMessage.  

```  
InvalidDate := 010184D;  
InvalidDateErrorMessage := 'The date is outside the valid date range.';  
ASSERTERROR CheckDate(InvalidDate);  
if GETLASTERRORTEXT <> InvalidDateErrorMessage then  
  ERROR('Unexpected error: %1', GETLASTERRORTEXT);  
```

## Test with Permission Sets
In most cases, users will be running with a permission set that limits their access to the functionality they need to do their work. To ensure that it works as intended, you can write application tests in AL that use specific permission sets when the test is run. For more information, see [Testing with Permission Sets](devenv-testing-with-permission-sets.md).

## Testing Best Practices
We recommend the following best practices for designing your application tests:  

- Test code should be kept separate from the code that is being tested. That way, you can release the tested code to a production environment without releasing the test code.  

- Test code should test that the code being tested works as intended both under successful and failing conditions. These are called positive and negative tests. The positive tests validate that the code being tested works as intended under successful conditions. The negative tests validate that the code being tested work as intended under failing conditions.  

  1. In positive tests, the test method should validate the results of application calls, such as return values, state changes, or database transactions.

  2. In negative tests, the test method should validate that the intended errors occur, error messages are presented, and the data has the expected values.  

- Automated tests should not require user intervention.  

- Tests should leave the system in the same well-known state as when the test started so that you can re-run the test or run other tests in any order and always start from the same state.  

- Test execution and reporting should be fast and able to integrate with the test management system so that the tests can be used as check-in tests or other build verification tests, which typically run on unattended servers.  

- Create test methods that follow the same pattern:  

  1. Initialize and set up the conditions for the test.  

  2. Invoke the business logic that you want to test.  

  3. Validate that the business logic performed as expected.  

<!-- TO DO: Check this-->
- Only use hardcoded values in tests when you really need it. For all other data, consider using random data. For example, you want to test the `Ext. Doc. No. Mandatory` field in the `Purchases & Payables Setup` table. To do this you need to create and post typical purchase invoice. The typical purchase invoice line specifies an amount. For most tests, it does not matter exactly what amount. For inspiration, see the use of the **GenerateRandomCode** method in the tests that are included in the **TestToolkit** folder on the [!INCLUDE[prodshort](includes/prodshort.md)] product media. For more information, see [Random Test Data](devenv-random-test-data.md).  

<!--- Monitor code coverage. For more information, see [Code Coverage](uiref/-$-N_9990-Code-Coverage-$-.md). -->


<!-- TO DO: Add articles for the links below-->
## See Also
 <!--[Application Test Automation](Application-Test-Automation.md)   -->
[Testing Pages](devenv-Testing-Pages.md)   
[Testing with Permission Sets](devenv-testing-with-permission-sets.md)     
[Creating Handler Methods](devenv-creating-handler-methods.md)      
[Test Codeunits and Test Methods](devenv-test-codeunits-and-test-methods.md)   
[Application Testing Example: Testing Purchase Invoice Discounts](devenv-test-application-example-purchase-invoice-discounts.md)     
[Random Test Data](devenv-Random-Test-Data.md)    
[Testing the Advanced Extension Sample](devenv-extension-advanced-example-test.md)
<!--[How to: Run Automated ApplicationTests](How-to--Run-Automated-ApplicationTests.md)   -->
<!--[Walkthrough: Create a Test with Confirmation Dialog](Walkthrough--Create-a-Test-with-Confirmation-Dialog.md)  -->

