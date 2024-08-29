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
Example
m
Copy code
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
Example
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
