---
title: "SelectToken Method"
ms.author: solsen
ms.custom: na
ms.date: 09/27/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .resx files in the ModernDev repo.)
# SelectToken Method
Selects a JsonToken using a JPath expression.

## Syntax
```
[Ok := ]  JsonObject.SelectToken(Path: String, var Result: JsonToken)
```
## Parameters
*JsonObject*  
&emsp;Type: [JsonObject](jsonobject-data-type.md)  
An instance of the [JsonObject](jsonobject-data-type.md) data type.  

*Path*  
&emsp;Type: [String](string-data-type.md)  
A valid JPath expression.  
*Result*  
&emsp;Type: [JsonToken](jsontoken-data-type.md)  
A JsonToken variable that will contain the result if the operation is successful.  


## Return Value
*Ok*  
&emsp;Type: [Boolean](boolean-data-type.md)  
**True** if the operation was successful; otherwise, **false**.  
**true** if the read was successful; otherwise, **false**.  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks
The operation will fail if more or less than 1 tokens are the result of evaluating the JPath.

## Example
The following example shows how to select a value from a complex JSON Object. We build up a select expression in the query variable, we select the token corresponding to the salary of the employee with the given employeeId, and finally, we convert the token to a Decimal value.

We assume that the company token contains JSON data similar to the one below.

```
{ "company": {
    "employees": [
      { "id": "Marcy",
        "salary": 8.95
      },
      { "id": "John",
        "salary": 7
      },
      { "id": "Diana",
        "salary": 10.95
      }
    ]
  }
}
```

```
local procedure SelectEmployeeSalary(companyData : JsonToken; employeeId : Text) salary : Decimal;
var
    query : Text;
    salaryToken : JsonToken;
begin
    query := '$.company.employees[?(@.id=="'+employeeId+'")].salary';
    companyData.SelectToken(query, salaryToken);

    salary := salaryToken.AsValue().AsDecimal();    
end;
```

## See Also
[JsonObject Data Type](jsonobject-data-type.md)  
[Getting Started with AL](../devenv-get-started.md)  
[Developing Extensions](../devenv-dev-overview.md)