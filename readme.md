# Readme

## Microsoft AL Comments

### Tables
You can handle data with AL, the basic struct for a table is next:

table id MyTable {
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
        key(Key1; MyField)
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



#### Short cuts
* ttable -> basic struct for a table.
* tpage -> basic struct for a page.
* tpageext -> basic struct for a extension page.
* tcodeunit -> basic struct for a codeunit