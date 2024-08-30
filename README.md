# M Language for Power Query: A Comprehensive Guide

## 1. **Basic Understanding of M Language**
M language, also known as Power Query Formula Language, is a functional, case-sensitive language used in Power Query. It's designed to transform and manipulate data within Power BI, Excel, and other Microsoft tools. M language is a powerful tool for data preparation and offers various functions for data transformation.

## 2. **Variables**
In M language, variables are used to store values or expressions that can be referenced later in the query.

### **Declaring Variables**
Variables are declared using the `let` keyword. The general syntax is:

```m
let
    variableName = expression
in
    variableName
```
### Example
```m
let
    SalesAmount = 1000,
    Tax = SalesAmount * 0.16,
    TotalAmount = SalesAmount + Tax
in
    TotalAmount
```
## 3. Comments
Comments in M language are essential for documenting your code and making it more understandable. There are two types of comments:

### Single-Line Comments
Use // to create a single-line comment.

```m
// This is a single-line comment
let
    SalesAmount = 1000
in
    SalesAmount
```
### Multi-Line Comments
Use /* ... */ for multi-line comments.

```m
/*
This is a multi-line comment
explaining the code below.
*/
let
    SalesAmount = 1000
in
    SalesAmount
```
## 4. Operators
M language provides several operators to perform calculations, comparisons, and logical operations.

### Arithmetic Operators
+ : Addition
- : Subtraction
* : Multiplication
/ : Division
### Comparison Operators
= : Equal to
<> : Not equal to
< : Less than
<= : Less than or equal to
> : Greater than
>= : Greater than or equal to
### Logical Operators
and : Logical AND
or : Logical OR
not : Logical NOT
#### Example
```m
let
    a = 10,
    b = 5,
    isGreater = a > b, // Comparison operator
    isEqual = a = b,   // Comparison operator
    Sum = a + b        // Arithmetic operator
in
    Sum
```
## 5. Power Query Functions
M language offers a wide range of built-in functions for data transformation. These functions can be categorized as follows:

### Text Functions
- Text.Upper: Converts text to uppercase.
- Text.Lower: Converts text to lowercase.
- Text.Trim: Removes leading and trailing spaces from text.
- Date & Time Functions
- DateTime.LocalNow: Returns the current date and time.
- Date.AddDays: Adds a specified number of days to a date.
### List Functions
- List.Sum: Sums all elements in a list.
- List.Max: Returns the maximum value in a list.
- List.Min: Returns the minimum value in a list.
### Table Functions
- Table.SelectRows: Filters rows based on a condition.
- Table.AddColumn: Adds a new column to a table.
- Table.RemoveColumns: Removes specified columns from a table.
### Example
```m
let
    Source = Table.FromRecords({
        [Name = "John", Age = 25],
        [Name = "Jane", Age = 30],
        [Name = "Smith", Age = 28]
    }),
    FilteredTable = Table.SelectRows(Source, each [Age] > 25),
    UpperNames = Table.TransformColumns(FilteredTable, {"Name", Text.Upper})
in
    UpperNames
```
## 6. Error Handling
M language provides ways to handle errors using functions like try ... otherwise and if ... then ... else.

### Example
```m
let
    SalesAmount = "invalid number",
    Result = try Number.FromText(SalesAmount) otherwise 0
in
    Result
```
### 7. Conditional Statements
Conditional logic can be implemented using if ... then ... else.

Example
```m
let
    Age = 18,
    Category = if Age >= 18 then "Adult" else "Minor"
in
    Category
```
### 8. Loops and Iterations
M language does not have traditional loops like for or while. However, recursion and list functions can achieve similar results.

### Example
```m
let
    List = {1, 2, 3, 4, 5},
    Sum = List.Sum(List)
in
    Sum
```
## 9. Advanced Functions
M language allows creating custom functions using the => operator.

### Example
```m
let
    Add = (x, y) => x + y,
    Result = Add(5, 10)
in
    Result
```
## 10. Conclusion
Understanding M language is crucial for efficiently using Power Query to prepare and transform data. With knowledge of variables, operators, functions, and error handling, you can unlock the full potential of data manipulation in Power Query.

# Creating Columns and Adding Data Using M Language in Power Query

## 1. **Creating a New Column**

In Power Query, you can create a new column using the `Table.AddColumn` function. This function takes three parameters:
- The table you want to add the column to.
- The name of the new column.
- The function that defines the values for the new column.

### **Syntax**
```m
Table.AddColumn(table as table, columnName as text, columnGenerator as function) as table
Example 1: Adding a Calculated Column
Suppose you have a table with columns Price and Quantity, and you want to add a new column Total that calculates the total price.

m
Copy code
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100, Quantity = 2],
        [Product = "B", Price = 150, Quantity = 3]
    }),
    AddTotalColumn = Table.AddColumn(Source, "Total", each [Price] * [Quantity])
in
    AddTotalColumn
```
In this example, the Table.AddColumn function creates a new column Total by multiplying the values of Price and Quantity.

### Example 2: Adding a Conditional Column
You can also add a column based on a condition. For instance, let's add a column Category based on the Price:

```m
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100],
        [Product = "B", Price = 150],
        [Product = "C", Price = 50]
    }),
    AddCategoryColumn = Table.AddColumn(Source, "Category", each if [Price] > 100 then "Premium" else "Standard")
in
    AddCategoryColumn
```
In this example, the Category column will have "Premium" for products with a price greater than 100 and "Standard" otherwise.

### 2. Adding Multiple Columns
You can add multiple columns by chaining Table.AddColumn functions together.

### Example: Adding Multiple Columns
Let's add two new columns: DiscountedPrice (10% discount) and FinalPrice (total price after discount).

```m
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100, Quantity = 2],
        [Product = "B", Price = 150, Quantity = 3]
    }),
    AddDiscountColumn = Table.AddColumn(Source, "DiscountedPrice", each [Price] * 0.9),
    AddFinalPriceColumn = Table.AddColumn(AddDiscountColumn, "FinalPrice", each [DiscountedPrice] * [Quantity])
in
    AddFinalPriceColumn
```
Here, we first add the DiscountedPrice column and then the FinalPrice column, which depends on the value of DiscountedPrice.

### 3. Adding Static Data to a New Column
If you want to add a column with the same value for every row, you can simply use a constant expression.

### Example: Adding a Static Column
Let's add a column Country with a static value "Kenya".

```m
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100],
        [Product = "B", Price = 150]
    }),
    AddCountryColumn = Table.AddColumn(Source, "Country", each "Kenya")
in
    AddCountryColumn
```
In this example, the Country column will have "Kenya" as its value for all rows.

### 4. Renaming Columns
After adding columns, you might want to rename them using the Table.RenameColumns function.

## Syntax
```m
Table.RenameColumns(table as table, renames as list) as table
```
### Example: Renaming a Column
Let's rename the Price column to UnitPrice.

```m
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100],
        [Product = "B", Price = 150]
    }),
    RenamePriceColumn = Table.RenameColumns(Source, {{"Price", "UnitPrice"}})
in
    RenamePriceColumn
```
### 5. Removing Columns
You can remove unwanted columns using the Table.RemoveColumns function.

### Syntax
```m
Table.RemoveColumns(table as table, columns as list) as table
```
### Example: Removing a Column
Let's remove the Quantity column from a table.

```m
let
    Source = Table.FromRecords({
        [Product = "A", Price = 100, Quantity = 2],
        [Product = "B", Price = 150, Quantity = 3]
    }),
    RemoveQuantityColumn = Table.RemoveColumns(Source, {"Quantity"})
in
    RemoveQuantityColumn
```
### 6. Conclusion
Creating and manipulating columns in Power Query using M Language provides a flexible way to transform your data. By understanding the functions for adding, renaming, and removing columns, you can tailor your data model to meet specific requirements.
