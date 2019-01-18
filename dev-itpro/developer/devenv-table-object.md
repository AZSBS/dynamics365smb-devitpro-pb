---
title: "Table Object"
description: "Description of the table object."
author: SusanneWindfeldPedersen
ms.custom: na
ms.date: 01/18/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: solsen
---

[!INCLUDE[d365fin_dev_blog](includes/d365fin_dev_blog.md)]

# Table Object
Tables are the core objects used to store data in [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)]. Regardless of how data is registered in the product - from a web service to a finger swipe on the phone app, the results of that transaction will be recorded in a table. 

The structure of a table has four sections. The first block contains metadata for the overall table; the table type. The fields section describes the data elements that make up the table; their name and the type of data they can store. The keys section contains the definitions of the keys that the table needs to support. The final section details the triggers and code that can run on the table.

> [!NOTE]  
> Extension objects can have a name with a maximum length of 30 characters.

> [IMPORTANT]  
> System and virtual tables cannot be extended. System tables are created in the ID range of 2.000.000.000. For more information about object ranges, see [Object Ranges](devenv-object-ranges.md).

## Snippet support
Typing the shortcut `ttable` will create the basic layout for a table object when using the [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] in Visual Studio Code.

## Table syntax
```
table id MyTable
{
    DataClassification = ToBeClassified;
    
    fields
    {
        field(1;MyField; Integer)
        {
            DataClassification = ToBeClassified;
            
        }
    }
    
    keys
    {
        key(PK; MyField)
        {
            Clustered = true;
        }
    }
    
    var
        myInt: Integer;
    
    trigger OnInsert()
    begin
        
    end;
    
    trigger OnModify()
    begin
        
    end;
    
    trigger OnDelete()
    begin
        
    end;
    
    trigger OnRename()
    begin
        
    end;
    
} 
```

## Table example
This table stores address information and has four fields; Address, Locality, Town/City, and County.

```
table 50104 Address
{
    caption = 'Sample table';
    DataPerCompany = true;

    fields
    {
        field(1; Address; Text[50])
        {
            Description = 'Address retrieved by Service';
        }
        field(2; Locality; Text[30])
        {
            Description = 'Locality retrieved by Service';
        }
        field(3; "Town/City"; Text[30])
        {
            Description = 'Town/City retrieved by Service';
        }
        field(4; County; Text[30])
        {
            Description = 'County retrieved by Service';

            trigger OnValidate();
            begin
                ValidateCounty(County);
            end;

        }
    }
    keys
    {
        key(PrimaryKey; Address)
        {
            Clustered = TRUE;
        }
    }

    var
        Msg: TextConst = 'Hello from my method';

    trigger OnInsert();
    begin

    end;

    procedure MyMethod();
    begin
        Message(Msg);
    end;
}
```

## See Also
[AL Development Environment](devenv-reference-overview.md)  
[Table Overview](devenv-tables-overview.md)  
[Table Extension Object](devenv-table-ext-object.md)  
[Table Keys](devenv-table-keys.md)  
[Table Properties](properties/devenv-table-properties.md)  
