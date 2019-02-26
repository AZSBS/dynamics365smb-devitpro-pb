---
title: "Debugging"
description: "Overview of debugging in AL"
author: SusanneWindfeldPedersen
ms.custom: na
ms.date: 01/17/2019
ms.reviewer: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: solsen
---

[!INCLUDE[d365fin_dev_blog](includes/d365fin_dev_blog.md)]

# Debugging

The process of finding and correcting errors is called *debugging*. With Visual Studio Code and the [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] you get an integrated debugger to help you inspect your code to verify that your application can run as expected. You start a debugging session by pressing F5.


> [!TIP]  
> For more information about Debugging in Visual Studio Code, see [Debugging](https://code.visualstudio.com/docs/editor/debugging).

> [!IMPORTANT]  
> To enable debugging the `NetFx40_LegacySecurityPolicy` setting in the Microsoft.Dynamics.Nav.Server.exe.config file must be set to **false**. This requires a server restart.

There are a number of limitations to be aware of:

- "External code" can only be debugged if the code has the `showMyCode` flag set. For more information, see [Security Setting and IP Protection](devenv-security-settings-and-ip-protection.md). 
- Not all AL types yet show helpful debugging.
- The debugger launches a new client instance each time you press F5. If you close the debugging session, and then start a new session, this new session will rely on a new client instance. We recommend that you close the Web client instances when you close a debugging session.

> [!TIP]  
> To control table data synchronization between each debugging session, see [Retaining table data after publishing](devenv-retaining-data-after-publishing.md).  

## Breakpoints
  
The basic concept in debugging is the *breakpoint*, which is a mark that you set on a statement. When the program flow reaches the breakpoint, the debugger stops execution until you instruct it to continue. Without any breakpoints, the code runs without interruption when the debugger is active. You can set a breakpoint by using the **Debug Menu** in Visual Studio Code. For more information, see [Debugging Shortcuts](#debugging-shortcuts). 
 
Set breakpoints on the external code that is not part of your original project. You can step into the base application code by using the **Go To Definition** feature, and set breakpoints on the referenced code which is generally a `.dal` file. To set a breakpoint on the external code or base application code, you do the following: 

- Use **Go To Definition** which opens the “external file” and then a breakpoint can be set.  
- Using the debugger, step into the code, and then set a breakpoint.

> [!NOTE]  
> "External code" can only be debugged if the code has the `showMyCode` flag set. For more information, see [Security Setting and IP Protection](devenv-security-settings-and-ip-protection.md).

In the following video illustration, the `Customer.dal` is an external file. A breakpoint is set in the `Customer.dal` file which is referenced from your AL project to stop execution at the marked point. 

![Debugger](media/DebuggingAL.gif)

For more information about **Go To Definition**, see [AL Code Navigation](devenv-al-code-navigation.md). 

## Break on Errors

Specify if the debugger breaks on the next error by using the `breakOnError` property. If the debugger is set to `breakOnError`, then it stops execution both on errors that are handled in code and on unhandled errors. 

The default value of the `breakOnError` property is **true**, which means the debugger stops execution that throws an error by default. To skip the error handling process, set the `breakOnError` property to **false** in the `launch.json` file. 

> [!TIP]  
> If the debugging session takes longer, you can refresh the session by pressing the Ctrl+Shift+P keys, and select the Reload Window.

## Break on Record changes

Specify if the debugger breaks on record changes by using the `breakOnRecordWrite` property. If the debugger is set to break on record changes, then it breaks before creating, modifying, or deleting a record. The following table shows each record change and the AL methods that cause each change.  

|Record change|AL Methods|  
|-------------------|---------------------|  
|Create a new record|[INSERT Method (Record)](methods/devenv-insert-method-record.md)|  
|Update an existing record|[MODIFY Method (Record)](methods/devenv-modify-method-record.md), [MODIFYALL Method (Record)](methods/devenv-modifyall-method-record.md), [RENAME Method (Record)](methods/devenv-rename-method-record.md)|  
|Delete an existing record|[DELETE Method (Record)](methods/devenv-delete-method-record.md), [DELETEALL Method (Record)](methods/devenv-deleteall-method-record.md)|  


The default value of the `breakOnRecordWrite` property is **false**, which means the debugger is not set to break on record changes by default. To break on record changes, you can set the `breakOnRecordWrite` property to **true** in the `launch.json` file. For more information, see [JSON Files](devenv-json-files.md).

## Debugging shortcuts

|Keystroke    |Action         |
|-------------|---------------|
|F5           |Start debugging|
|Ctrl+F5      |Start without debugging|
|Shift+F5     |Stop debugging|
|Ctrl+Shift+F5|Restart debugging|
|F10          |Step over|
|F11          |Step into|
|Shift+F11    |Step out|
|F12          |Go To Definition| 

For more shortcuts, see [Debugging](https://code.visualstudio.com/docs/editor/debugging). 

<!-- 
To use the Go To Definition on local server, it requires that the AL symbols are rebuilt and downloaded from C/SIDE. The application symbols that were built with the previous version of C/SIDE would not make it possible to have Go To Definition work on base application methods. -->

## Debugging SQL behavior

Traditionally, debugging AL has been about examining behavior of the language runtime, for example, looking into the content of local variables at a breakpoint.  As of [!INCLUDE[prodshort](includes/prodshort.md)] April 2019, the AL debugger also offers the capability to examine the impact that your AL code has on the [!INCLUDE[prodshort](includes/prodshort.md)] database.

In the variables box of the debugger, expand the <Database statistics> node to get insights, 
such as the current network latency between the [!INCLUDE[server](includes/server.md)] and the [!INCLUDE[prodshort](includes/prodshort.md)] database, the total number of SQL statements executed, and the total number of rows read, as well as insights into the most recent SQL statements executed by the server. The following insights are part of the database statistics:

|       |       |
|-------|-------|
|Current SQL latency (ms) | When the debugger hits a breakpoint, the server will send a short SQL statement to the database and measure how long time it takes. The value is shown is in milliseconds.| 
|Number of SQL Executes | This number shows the total number of SQL statements executed in the debugging session since the debugger was started.|
|Number of SQL Rows Reads | This number shows the total number of rows read from the [!INCLUDE[prodshort](includes/prodshort.md)] database in the debugging session since the debugger was started.|

Database insights also give you the possibility to peek into the most recent and the latest long running SQL statements executed by the server. Expand either the <Last Executed SQL Statements> or the <Last Long Running SQL Statements> node to get a list of these. The following insights are part of the SQL statement statistics:

|       |       |
|-------|-------|
|Statement | The SQL statement that the AL server sent to the [!INCLUDE[prodshort](includes/prodshort.md)] database. You can copy this into other database tools such as SQL Server Management Studio for further analysis.| 
|Execution time (UTC) | The timestamp in UTC of when the SQL statement was executed. You can use this to infer if the SQL statement was part of the AL code between current and last breakpoint (if set).
|Duration (ms) | The duration in milliseconds of the total execution time of the SQL statement measured inside the [!INCLUDE[server](includes/server.md)]. You can use this to analyze if you are missing indexes ([!INCLUDE[prodshort](includes/prodshort.md)] keys), or to experiment with performance of database partitioning and/or compression.|
|Approx. Rows Read | This number shows the approximate number of rows read from the [!INCLUDE[prodshort](includes/prodshort.md)] database by the SQL statement. You can use this to analyze if you are missing filters.|

The number of SQL statements tracked by the debugger can be configured in the [!INCLUDE[server](includes/server.md)]. The default value is 10.

## Configuring Debugger in [!INCLUDE[prodshort](../includes/prodshort.md)] on-premises

The [!INCLUDE[server](includes/server.md)] instance has several configuration settings that control whether the debugger is enabled and the issights it provides. For more information about these settings, see [Configuring Business Central Server](../administration/configure-server-instance.md#Developer).

## See Also
  
[Developing Extensions](devenv-dev-overview.md)  
[JSON Files](devenv-json-files.md)  
[AL Code Navigation](devenv-al-code-navigation.md)  