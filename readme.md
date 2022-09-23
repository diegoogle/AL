# Readme

# Microsoft AL Sintaxis

## Variables:

- All identifiers must be unique.
- When set the name to a variable is recomended start with '_' or a letter. 
- The language is not sensitive to lower and upper in identifiers names (Recomend use PascalCase).
- The variables need a identify, type, propuse and must be initialized.
- Varaible can be local or global, local: inside a procedure or trigger, global: out of that.
- **'Rec' and 'xRec' is used by the system language, Rec -> access to current record, xRec -> access to last record (before update).**
- Default numeric variable type is 0.
- Default text variable is empty.
- Default boolean variable is false.

**Variable Declaration:**

```
  - var
  - myInt, nextInt, thirdInt : Integer; //this 3 var's as integer
  - isValid, doCheck : Boolean; // this 2 var's as boolean
```

**Protected Variable:**
  - protected var
  - myInt: Integer

### **Fundamentals Data Types**
- **Numeric**
  - Action (no available to tables)
    - Ok
    - Cancel
    - LookupOk
    - lookupCancel
    - Yes
    - No
    - RunObject
    - RunSystem
  - Integer
  - BigInteger
  - Decimal
  - Option 
  - Char (ASCII from 0 to 255)
  - Byte
  - Duration
- **String**
  - Text
  - Code
- **Boolean**
- **Date**
- **Time**
- **DateTime**
### **Complex Data Types**
This data types can be store multiple values
- BigText
- BLOB
- CodeUnit
- DateFormula
- Dialog
- File
- Fieldref
- GUID
- InStream y OutSream
- KeyRef
- Page
- Query
- Record
- RecordID
- RecordRef
- Report
- System
- TableFilter
- Variant
- List y Dictionary

### **Operations and numerations**

- **Option**
Is a enumerator so, the options will save as integer inside the option variable like:
```
var Color: **Option** Green,Red,Yellow;  
then
Color := Color::Red;
```
The options fields in a table can´t be extended with a table extension.

- **Enum** 

The Enum is also to enumerate options and can be extended like:

```
enum 50100 Color
{
    Extensible = true;

    value(0; Green)
    {
        Caption = 'Green';
    }
    value(1; Red)
    {
        Caption = 'Red'
    }
    value(1; Yellow)
    {
        Caption = 'Yellow'
    }
}

var MyFavoriteColor: **Enum** Color; //This set MyFavoriteColor variable as type Enum Color
begin
    MyFavoriteColor := Color:Red;
    Message('Selected Color is: %1', MyFavoriteColor);
end;
```

-   **Collections**

AL have 3 collection types
- Array ->  
  - Identifier
  - Data type
  - One or more elements
  - One index
  - A dimension
    ```
    SalesAmount: array[10] of Integer;
    ```
    To enter to element:
    ```
    SalesAmount[5] := 0;
    ```
    #### **In AL starts counting at 1 for any array**
    For multidimensional array 
    ```
    SalesAmount: array[6,9] of Integer;
    SalesAmount[5,3] := 0;
    ```

- List

    Just can be use with fundamental type, this type 
    use System.Collections.Generic.List<T> Class form .NET Framework, so you can use some their methods.
    ```
    procedure AddCustomerNames()
    var
        CustomerNames: List of [Text];
    begin
        CustomerNames.Add('Paul');
        CustomerNames.Add('Linda');
        Message(CustomerNames.Get(1));//Result 'Paul'
    end;
    ```

- Dictionary

    This type use System.Collections.Generic.Dictionary<TKey, TValue> of .Net Framework, this type represent a collection of keys and values
    procedure AddCustomerNames()
    ```
    var    
        CustomerNames2: List of [Text];
        CountriesDictionary: Dictionary of [Code[20], List of [Text]];//Code is a string type

        CustomerNames2.Add('Eddy');
        CustomerNames2.Add('Mark');
        CountriesDictionary.Add('US', CustomerNames);
        CountriesDictionary.Add('CA', CustomerNames2);

        Message(CountriesDictionary.Get('US').Get(2));
        //Result in 'Linda'
    begin       
    ```
### **Use assignments and type conversions**

You can set a value to a variable or the statement will asign a value to a variable.
You can asign with ':='

```
var 
    MyInt: Integer;
    A: Integer;
    B: Integer;
begin    
    A := 2;
    B := 3;
    MyInt := A + B;
end;
```
Description was assigned to the variable Code. Because the variable Code is of data type Code, it will automatically convert all lowercase letters to uppercase, and it will remove all leading and trailing spaces

Just string and numeric types allow automatic type **conversion**
```
var
    Description: Text[20];
    Code: Code[20];
begin
    Description = ' Hello World ';
    Code := Description;
    //Return 'HELLO WORLD'
    //Code delete start and finish blank spaces and convert to upper.
```
The value needs to be within the range of the variable. You can't assign a BigInteger value to an Integer data type if it exceeds the range of the integer.

### **Different expression types**

With a unary operator, the operator impacts the term that directly follows it. A binary operator impacts on either side of the operator.
Can be categorized by:
- Unary
  - (+)
  - (-)
  - NOT
   ```
   var
    CustomerExists: Boolean;
    MyBoolean: Boolean;
   begin
    CustomerExists := true;
    MyBoolean =: NOT CustomerExists;
    // Will result in MyBoolean: false 
    end; 
    ```

- String 
    
    Only (+) because concatenate two string in one
    ```
    Var
        MyText: Text[50];
    begin
        MyText := 'Wo' + 'rd'//Result is 'Word'
    end;
    ```
- Arithmetic

    Arithmetic operators are used in numeric expressions. A numeric expression is a formula that results in a numeric value.
    The following arithmetic operators are available:

    - Plus (+)
    - Minus (-)
    - Times (*)
    - Divide (/)

    If you divide two integer values, you'll always end with a Decimal value.

    Integer divide (DIV)

    The integer divide (DIV) operator is returning the integer quotient of the integer division. It's a binary operator that results in an integer value. You can calculate the result of an integer divide by dropping all the decimals of the result.

    ```
    17 DIV 8 = 2  // The decimal portion .125 is dropped
    17 DIV 9 = 1  // The decimal portion .88 is dropped
    ```

    Modulus (MOD)
    The modulus finds the remainder of the division of one number by another number.
    ```
    5 MOD 2 = 1   5 = (2x2) + 1
    17 MOD 9 = 8   17 = (9x1) + 8
    ```
- Relational

    The following Relational expressions are available:
    - = (equal to)
    - < (less than)
    - > (greater than)
    - <= (less than or equal to)
    - >= (greater than or equal to)
    - <> (not equal to)
    - IN (include in set)

    - Numeric comparisons - Numeric comparisons are clear; they compare on the numeric value.
    - String comparisons - Strings are compared with the Unicode date to determine which value comes first.
    - Date and time comparisons - The calendar is used to determine which value comes first.
    - Boolean comparisons - The false value will come before the true value.

    The Set Inclusion (with the IN operator) is a list of values:
    ```    
    5 IN [2,4,6,8,10] is FALSE
    5 IN [1..9,11..19] is TRUE
    5 IN [2,4..6,8,10] is TRUE
    10 IN [1..9,11..19] is FALSE
    'M' IN ['A'..'Z'] is TRUE
    ```

- Logical expresions
    
    The following logical expressions are available:
    - AND
    - OR
    - XOR 
    - NOT


### Tables
You can handle data with AL, the basic struct for a table is next:

```
table iod MyTable {
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
```


#### Short cuts
* ttable -> basic struct for a table.
* tpage -> basic struct for a page.
* tpageext -> basic struct for a extension page.
* tcodeunit -> basic struct for a codeunit
