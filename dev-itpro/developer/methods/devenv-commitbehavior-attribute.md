---
title: "CommitBehavior Attribute"
ms.author: solsen
ms.custom: na
ms.date: 07/16/2020
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: SusanneWindfeldPedersen
---

# CommitBehavior Attribute

Specifies the behavior of `commit` calls inside the method scope of the call.

## Syntax  

```  
[CommitBehavior(CommitBehavior::Ignore)]
local procedure ProcedureIgnoreCommit()
begin
    // Do something
end;
```

## Attribute values

`CommitBehavior::Ignore`
This will ignore all `commit` calls until the method scope ends.

`CommitBehavior::Error`
This will throw an exception and stop the execution of further code when a `commit` is called before the end of the scope of the method.


> [!NOTE]  
> It is only possible to assign a more restrictive `commit` behavior. That is, if `CommitBehavior::Ignore` is attempted on a method scope, but the method calling the current method, e.g. the parent method is actually running with `CommitBehavior::Error`, then the current method will continue running with `CommitBehavior::Error`, even though the `Ignore` attribute was specified.


> [!NOTE]   
> The `CommitBehavior` only lasts for the method scope. Regardless of whether the method finishes successfully or if an error causes the method to exit prematurely, the `CommitBehavior` reverts to the standard behavior, where `commit` statements will commit to the database.

## Example

```
codeunit 50100 MyCodeunit
{
    trigger OnRun()
    var
    begin
        FunctionAllowCommit();
    end;

    local procedure FunctionAllowCommit()
    begin
        FunctionIgnoreCommit();
        COMMIT; // This is valid, and Commit call will be executed.
    end;

    [CommitBehavior(CommitBehavior::Ignore)]
    local procedure FunctionIgnoreCommit()
    begin
        TryFunctionErrorCommit();
        COMMIT; // This call will be silently ignored.
    end;

    [CommitBehavior(CommitBehavior::Error)]
    [TryFunction]
    local procedure TryFunctionErrorCommit()
    begin
        COMMIT; // This will throw an error. No further code will be executed and User will see a dialog to contact the System administrator.
    end;

    var
        myInt: Integer;
}
```
  
## See Also  

[AL Method Reference](../methods-auto/library.md)  
