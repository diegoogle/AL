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

### **Instructions**
- **Comment**

    //This is a comment    
    /* This is a comment */

    ///<'summary'>
    /// This property always returns a value &lt; 1.
    /// 
    ///<'/summary'>
    
- **Compoud**

    ```
    begin
        statement 1;
        statement 2;
        statement 3;
        ...
    end;
    ```
- **Conditional**

    ```
    if a > b then
        c := a - b;

    //Or:

    if a > b then begin
        c := a - b;
        Message('%1', c);
    end;
    ```

    - If-Else Sentence:

    ```
    if a > b then
        c := a - b
    else
        c := a + b;
    
    //Or:

    if a > b then begin
        c := a - b;
        Message('%1', c);
    end
    else begin
        c := a + b;
        Message('%1', c);
    end;
    ```
    - Nested If
    ```
    begin
    if Amount <> 0 then
        if Amount > 0 then
            Sales := Sales + Amount
        else
            if Reason = Reason::Return then
                if ReasonForReturn = ReasonForReturn::Defective then
                    Refund := Refund + Amount
                else
                    Credits := Credits + Amount
            else
                Sales := Sales - Amount;
    end;
    ```
    - Case Statement

    The case statement can use an else block that will be run when no other blocks are run. Because you can only run one statement for each block with a case statement, you have to use compound statements to run more statements simultaneously.   
    Depending on the value of Document Type the case statement will run some statements.
    ```
    var
        a: Integer;
    begin
        case "Document Type" of
            "Document Type"::Quote:
                a := 1 + 1;
            "Document Type"::Order:
                a := 2 + 1;
            "Document Type"::Invoice:
                begin
                    // Some statement 1;
                    // Some statement 2;
                    // Some statement 3;
                    a := 3 + 1;
                end;
            "Document Type"::"Return Order":
                if Reason = Reason::Return then begin
                    // Some statement 1;
                    // Some statement 2;
                    // Some statement 3;
                    a := 4 + 1;                
                end;
        else
            a := 5 + 1;//Last option 
        end;
    end;
    ```
    - Preprocessor Directives in AL

        The following conditional preprocessor directives are supported in AL.

        - #if - Specifies the beginning of a conditional clause. The #endif clause ends it. Compiles the code between the directives if the specified symbol being checked is defined.
        - #else - Specifies a compound conditional clause. If none of the preceding clauses evaluates to true, the compiler will evaluate code between #else and #endif.
        - #elif - Combines else and if. If #elif is true the compiler evaluates all code between #elif and the next conditional directive.
        - #endif - Specifies the end of a conditional clause that begins with #if.
        - #define - Defines a symbol that can be used to specify conditions for a compilation. For example, #define DEBUG. The scope of the symbol is the file that it was defined in.
        - #undef - Undefines a symbol.

        Symbols can be defined globally in the app.json file. A symbol can also be defined using the #define directive in code, but if symbols are defined in the **app.json** file, they can be used globally.
        ```
        "preprocessorSymbols": [ "DEBUG" ]
        ```

        al-code using DEBUG symbol
        ```
        #if DEBUG
            trigger OnOpenPage()
            begin
                Message('Only in debug versions');
            end;
        #endif
        ```

        There is a new suppressWarnings property in the app.json manifest so that you can suppress a comma-separated list of warning IDs when you compile the extension:

        ```
        "suppressWarnings": [Warning ID,Warning ID2,...]
        ```

        Local
        Directives is a new construct in the AL language that specifies how the AL compiler treats an enclosed section of code. The same concept is known in other languages. The specific directive instructions must be supported by the compiler. You can't create custom preprocessing instructions.

        One of the new directives is a warning pragma, which you can set around a code section to suppress a comma-separated list of warnings only in that enclosure.
        If no end pragma closure is provided, it will be the rest of the file.

        ```
        #pragma warning disable warning-list
        #pragma warning restore warning-list
        ```

- **Repetitive**

if you want to stop the cycle use the **break** expression
  - For-to-do

        
        var
            intCount: Integer;
            total: Integer;
        begin
            for intCount := 1 to 5 do
                total := total + 3;
        end;

        //Or:

        var
            intCount: Integer;
            numberOfLoops: Integer;
            total: Integer;
        begin
            numberOfLoops := 5;
            for intCount := 1 to numberOfLoops do
                total := total + 3;
        end;
        

- For-downto-do

        
        var
            intCount: Integer;
            totalSales: Integer;
            numberSales: Integer;
            sales: array[5] of Integer;
        begin
        GetSales(sales);

            for intCount := 5 downto 1 do begin
                totalSales := totalSales + sales[intCount];
                numberSales := numberSales + 1;
            end;
        end;
        
        
- Foreach-in-do


        var
            stringList: List of [Text[20]];
            stringItem: Text[20];
        begin
            foreach stringItem in stringList do
                Message(stringItem);
        end;


- While-do
        
        var
            index: Integer;
            totalSales: Integer;
            sales: array[5] of Integer;
        begin
            GetSales(sales);
            while totalSales < 8 do begin
                index := index + 1;
                totalSales := totalSales + sales[index];
            end;
        end;
        ```
    - Repeat-until

    ```
    var
        index: Integer;
        totalSales: Integer;
        sales: array[5] of Integer;
    begin
        GetSales(sales);
        repeat
            index := index + 1;
            totalSales := totalSales + sales[index];
        until totalSales >= 8;
    end;

    //Or:

    var
        myTable: Record MyTable;
    begin
        myTable.FindSet();
        repeat
            myTable.Amount := 100;
        until myTable.Next() = 0;
    end;
    ```    

- With Statement

    This statement reduce the use of your recrod variables:
    ```
    var
        myTable: Record MyTable;
    begin
        myTable."No." := 1;
        myTable.Amount := 100;
        myTable.Credits := 10;
        myTable."Document Type" := myTable."Document Type"::Invoice;
        myTable.Reason := myTable.Reason::Return;
        myTable.Refund := 100;
    end;   

    //Instead you can write this (Not recomended use),
    var
        myTable: Record MyTable;
    begin
        with myTable do begin
            "No." := 1;
            Amount := 100;
            Credits := 10;
            "Document Type" := "Document Type"::Invoice;
            Reason := Reason::Return;
            Refund := 100;
        end;
    end;

    // Safe version
    codeunit 50140 MyCodeunit
    {
        procedure DoStuff()
        var
            Customer: Record Customer;
        begin
            // Do some work on the Customer record.
            Customer.Name := 'Foo';

            if IsDirty() then 
                Customer.Modify();
        end; 

        local procedure IsDirty(): Boolean;
        begin
            exit(false);
        end;
    }
    ``` 

    The procedures with the same name in differents files have priority??

### Pages

    page 50143 ImplicitWith
    {
        SourceTable = Customer;

        layout
        {
            area(Content)
            {
                field("No."; "No.") { }
                field(Name; Name)
                {
                    trigger OnValidate()
                    begin
                        Name := 'test';
                    end;
                }
            }
        }

        trigger OnInit()
        begin
            if IsDirty() then Insert()
        end;

        local procedure IsDirty(): Boolean
        begin
            exit(Name <> '');
        end;
    }

### Interaction functions

- Message
    Is used to comunicate information to users

    ```
    Message(string [,Value1, ...]);
    Message('Hello World');

    //Or:

    var
        MyInt: Integer;
        TheValueOfTxt: Label 'The value of %1 is %2';
    begin
        MyInt := 5;
        Message(TheValueOfTxt, 'MyInt', MyInt);
        // Displays: The value of MyInt is 5
    end;
    ```
- Confirm

    You can use the Confirm function based on a string, which is generated from the question that you ask the user. The message is displayed with a Yes and a No button.
    ```
    Ok := Dialog.Confirm(string [,Default] [,Value1, ...]);

    //If clause:
    
    if Confirm('Are you sure you want to delete?') then
        Message('OK')
    else
        Message('Not OK');

    //No button have the default focus, add false as a parameter:

    if Confirm('Are you sure you want to delete?', false) then
        Message('OK')
    else
        Message('Not Ok');
    ```

- StrMenu

- Error

### Tables
You can handle data with AL, the basic struct for a table is next:

```
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
```


#### Short cuts
* ttable -> basic struct for a table.
* tpage -> basic struct for a page.
    - tpagefield -> basic struct for a field page.
* tpageext -> basic struct for a extension page.
* tcodeunit -> basic struct for a codeunit

#### Links

- Shortcuts VS CODE | https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf |


### Doubts
With Statement Symbols Search |
https://learn.microsoft.com/es-mx/training/modules/al-statements/4-repetitive |