# Power Query / M Query Cheatsheet

Author : [Naveen Jujaray](https://www.linkedin.com/in/naveenjujaray/) <br>
Created On : 20-Aug-2025 <br>
Last Updated : 20-Aug-2025 <br>
References : [PDF](https://github.com/naveenjujaray/M-Query-Cheat-Sheet/blob/a70efcef6fe0fbc46e270f254d9104301f33cd7f/powerquery-m.pdf) | [Web](https://learn.microsoft.com/pdf?url=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fpowerquery-m%2Ftoc.json) <br>

## **Disclaimer** <br>
>This cheatsheet is a community-compiled reference intended for quick lookup and learning. Power Query M evolves over time and :
>
>- Some functions, connectors, options, or examples here may be deprecated, renamed, or behavior-changed across product versions (Power BI Desktop/Service, Excel, Dataflows, Fabric, Gateway).
>
>- Certain features may be preview-only, region-limited, or require specific privacy, authentication, or tenant settings.
>
>- Syntax, parameter shapes, return types, folding behavior, and culture/locale handling can differ between engines and releases.
>
>Before using any item in production :
>
>- Verify the current function signature, availability, and supported options in the latest official documentation.
>
>- Test in a clean query with your target engine and data source.
>
>- Prefer explicit types and culture parameters where applicable.
>
>- Watch for deprecation notices, connector version notes, and breaking-change announcements.
>
>Use at your own risk. No warranty of completeness, correctness, or fitness for a particular purpose is provided. Always follow the latest syntax and guidance from Microsoft Learn and your organization’s governance policies.

## Tables of Content
<nav aria-label="Table of Contents">
  <ul>
    <li><a href="#-table-functions">📂 Table Functions</a></li>
    <li><a href="#-text-functions">📂 Text Functions</a></li>
    <li><a href="#-number-functions">📂 Number Functions</a></li>
    <li><a href="#-date-functions">📂 Date Functions</a></li>
    <li><a href="#-time-functions">📂 Time Functions</a></li>
    <li><a href="#-datetime-functions">📂 DateTime Functions</a></li>
    <li><a href="#-duration-functions">📂 Duration Functions</a></li>
    <li><a href="#-logical--conditional-functions">📂 Logical &amp; Conditional Functions</a></li>
    <li><a href="#-data-type--type-system-functions">📂 Data Type &amp; Type System Functions</a></li>
    <li><a href="#-list-functions">📂 List Functions</a></li>
    <li><a href="#-record-functions">📂 Record Functions</a></li>
    <li><a href="#-function--parameter-handling">📂 Function &amp; Parameter Handling</a></li>
    <li><a href="#-expression-advanced--metadata-functions">📂 Expression, Advanced &amp; Metadata Functions</a></li>
    <li><a href="#-accessing-data-functions">📂 Accessing Data Functions</a></li>
    <li><a href="#-binary-functions">📂 Binary Functions</a></li>
    <li><a href="#-binaryformat-functions">📂 BinaryFormat Functions</a></li>
    <li><a href="#-combiner-functions">📂 Combiner Functions</a></li>
    <li><a href="#-comparer-functions">📂 Comparer Functions</a></li>
    <li><a href="#-lines-functions">📂 Lines Functions</a></li>
    <li><a href="#-replacer-functions">📂 Replacer Functions</a></li>
    <li><a href="#-splitter-functions">📂 Splitter Functions</a></li>
    <li><a href="#-uri-functions">📂 Uri Functions</a></li>
    <li><a href="#-value-functions">📂 Value Functions</a></li>
    <li><a href="#-expression--error--diagnostics">📂 Expression &amp; Error &amp; Diagnostics</a></li>
    <li><a href="#-table-helper-functions">📂 Table Helper Functions</a></li>
    <li><a href="#-text-helper-functions">📂 Text Helper Functions</a></li>
    <li><a href="#-number-helper-functions">📂 Number Helper Functions</a></li>
    <li><a href="#-datetime-overloads">📂 Date/Time Overloads</a></li>
  </ul>
</nav>
<br>


***
<section id="-table-functions"><h2>📂 Table Functions</h2></section>

***
### **Table.AddColumn**

**Syntax**

```m
Table.AddColumn(table as table, newColumnName as text, columnGenerator as function, optional columnType as nullable type) as table
```

**Syntax + Placeholder**

```m
Table.AddColumn(SourceTable, "NewColumn", each [ColumnA] + [ColumnB], type number)
```

**Example**

```m
Table.AddColumn(Sales, "Total", each [Qty] * [Price], type number)
// Adds a new column "Total" to Sales table.
```


***

### **Table.AddConditionalColumn**

**Syntax**

```m
Table.AddConditionalColumn(table as table, newColumnName as text, columnGenerator as function, optional columnType as nullable type) as table
```

**Syntax + Placeholder**

```m
Table.AddConditionalColumn(Source, "Status", each if [Score] >= 50 then "Pass" else "Fail", type text)
```

**Example**

```m
Table.AddConditionalColumn(Students, "Result", each if [Marks] >= 40 then "Pass" else "Fail", type text)
// Adds a new column "Result" with condition.
```


***

### **Table.AddIndexColumn**

**Syntax**

```m
Table.AddIndexColumn(table as table, newColumnName as text, optional initialValue as number, optional increment as number, optional columnType as nullable type) as table
```

**Syntax + Placeholder**

```m
Table.AddIndexColumn(Source, "Index", 1, 1, Int64.Type)
```

**Example**

```m
Table.AddIndexColumn(Sales, "RowNumber", 1, 1, Int64.Type)
// Adds sequential row numbers starting at 1.
```


***

### **Table.AddKey**

**Syntax**

```m
Table.AddKey(table as table, keyColumns as list, isPrimary as logical) as table
```

**Syntax + Placeholder**

```m
Table.AddKey(Source, {"CustomerID"}, true)
```

**Example**

```m
Table.AddKey(Customers, {"CustomerID"}, true)
// Sets CustomerID as Primary Key.
```


***

### **Table.AddPrimaryKey**

**Syntax**

```m
Table.AddPrimaryKey(table as table, keyColumns as list, isPrimary as logical) as table
```

**Syntax + Placeholder**

```m
Table.AddPrimaryKey(Source, {"OrderID"}, true)
```

**Example**

```m
Table.AddPrimaryKey(Orders, {"OrderID"}, true)
// Marks OrderID as the Primary Key.
```


***

### **Table.AddRankColumn**

**Syntax**

```m
Table.AddRankColumn(table as table, rankKind as number, optional comparisonColumns as any, optional tiesMethod as number) as table
```

**Syntax + Placeholder**

```m
Table.AddRankColumn(Source, RankKind.Ascending, {"Score"}, Ties.Mean)
```

**Example**

```m
Table.AddRankColumn(Students, RankKind.Descending, {"Marks"}, Ties.Dense)
// Adds a ranking column based on Marks.
```


***

### **Table.AlternateRows**

**Syntax**

```m
Table.AlternateRows(table as table, offset as number, skip as number, take as number) as table
```

**Syntax + Placeholder**

```m
Table.AlternateRows(Source, 0, 1, 2)
```

**Example**

```m
Table.AlternateRows(Sales, 0, 1, 2)
// Skips 1 row, takes 2 rows, alternates the pattern.
```


***

### **Table.Buffer**

**Syntax**

```m
Table.Buffer(table as table) as table
```

**Syntax + Placeholder**

```m
Table.Buffer(Source)
```

**Example**

```m
Table.Buffer(Sales)
// Buffers the Sales table in memory for performance.
```


***

### **Table.Column**

**Syntax**

```m
Table.Column(table as table, column as text) as list
```

**Syntax + Placeholder**

```m
Table.Column(Source, "ColumnA")
```

**Example**

```m
Table.Column(Sales, "Price")
// Returns a list of values from the "Price" column.
```


***

### **Table.ColumnCount**

**Syntax**

```m
Table.ColumnCount(table as table) as number
```

**Syntax + Placeholder**

```m
Table.ColumnCount(Source)
```

**Example**

```m
Table.ColumnCount(Sales)
// Returns the number of columns in Sales table.
```


***

### **Table.ColumnNames**

**Syntax**

```m
Table.ColumnNames(table as table) as list
```

**Syntax + Placeholder**

```m
Table.ColumnNames(Source)
```

**Example**

```m
Table.ColumnNames(Sales)
// Returns: {"Product", "Qty", "Price"}
```


***

### **Table.ColumnsOfType**

**Syntax**

```m
Table.ColumnsOfType(table as table, types as list) as list
```

**Syntax + Placeholder**

```m
Table.ColumnsOfType(Source, {type number})
```

**Example**

```m
Table.ColumnsOfType(Sales, {type number})
// Returns list of numeric columns.
```


***

### **Table.Combine**

**Syntax**

```m
Table.Combine(tables as list) as table
```

**Syntax + Placeholder**

```m
Table.Combine({Table1, Table2})
```

**Example**

```m
Table.Combine({Sales2023, Sales2024})
// Combines two tables into one.
```


***

### **Table.CombineColumns**

**Syntax**

```m
Table.CombineColumns(table as table, columns as list, combiner as function, newColumn as text) as table
```

**Syntax + Placeholder**

```m
Table.CombineColumns(Source, {"FirstName","LastName"}, Combiner.CombineTextByDelimiter(" "), "FullName")
```

**Example**

```m
Table.CombineColumns(Employees, {"FirstName","LastName"}, Combiner.CombineTextByDelimiter(" "), "FullName")
// Combines FirstName and LastName into FullName column.
```


***

### **Table.DemoteHeaders**

**Syntax**

```m
Table.DemoteHeaders(table as table) as table
```

**Syntax + Placeholder**

```m
Table.DemoteHeaders(Source)
```

**Example**

```m
Table.DemoteHeaders(MyTable)
// Demotes headers to first row.
```


***

### **Table.Distinct**

**Syntax**

```m
Table.Distinct(table as table, optional columnsOrKey as any) as table
```

**Syntax + Placeholder**

```m
Table.Distinct(Source, {"CustomerID"})
```

**Example**

```m
Table.Distinct(Sales)
// Removes duplicate rows from Sales.
```


***

### **Table.ExpandListColumn**

**Syntax**

```m
Table.ExpandListColumn(table as table, column as text) as table
```

**Syntax + Placeholder**

```m
Table.ExpandListColumn(Source, "Tags")
```

**Example**

```m
Table.ExpandListColumn(Products, "Categories")
// Expands lists into multiple rows.
```


***

### **Table.ExpandRecordColumn**

**Syntax**

```m
Table.ExpandRecordColumn(table as table, column as text, fields as list, optional newNames as list) as table
```

**Syntax + Placeholder**

```m
Table.ExpandRecordColumn(Source, "Details", {"Address","Phone"}, {"CustomerAddress","CustomerPhone"})
```

**Example**

```m
Table.ExpandRecordColumn(Customers, "Contact", {"Email","Phone"})
// Expands nested records.
```


***

### **Table.ExpandTableColumn**

**Syntax**

```m
Table.ExpandTableColumn(table as table, column as text, fields as list, optional newNames as list) as table
```

**Syntax + Placeholder**

```m
Table.ExpandTableColumn(Source, "Orders", {"OrderID","Amount"}, {"CustomerOrderID","OrderAmount"})
```

**Example**

```m
Table.ExpandTableColumn(Customers, "Orders", {"OrderID","Amount"})
// Expands nested table.
```


***

### **Table.FillDown**

**Syntax**

```m
Table.FillDown(table as table, columns as list) as table
```

**Syntax + Placeholder**

```m
Table.FillDown(Source, {"Region"})
```

**Example**

```m
Table.FillDown(Sales, {"Region"})
// Fills nulls with values from above row.
```


***

### **Table.FillUp**

**Syntax**

```m
Table.FillUp(table as table, columns as list) as table
```

**Syntax + Placeholder**

```m
Table.FillUp(Source, {"Region"})
```

**Example**

```m
Table.FillUp(Sales, {"Region"})
// Fills nulls with values from below row.
```


***

### **Table.FirstN**

**Syntax**

```m
Table.FirstN(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.FirstN(Source, 5)
```

**Example**

```m
Table.FirstN(Sales, 5)
// Returns first 5 rows.
```


***

### **Table.FromColumns**

**Syntax**

```m
Table.FromColumns(columns as list, optional columnNames as any) as table
```

**Syntax + Placeholder**

```m
Table.FromColumns({{1,2,3}, {"A","B","C"}}, {"Numbers","Letters"})
```

**Example**

```m
Table.FromColumns({{1,2,3},{10,20,30}}, {"Col1","Col2"})
// Creates table from two lists.
```


***
### **Table.FromList**

**Syntax**

```m
Table.FromList(list as list, splitter as function, optional columns as any, optional default as any, optional extraValues as any) as table
```

**Syntax + Placeholder**

```m
Table.FromList({"A","B","C"}, Splitter.SplitByNothing(), {"Letters"})
```

**Example**

```m
Table.FromList({1,2,3}, Splitter.SplitByNothing(), {"Numbers"})
// Creates a single-column table with values 1,2,3.
```


***

### **Table.FromRecords**

**Syntax**

```m
Table.FromRecords(records as list) as table
```

**Syntax + Placeholder**

```m
Table.FromRecords({[ID=1, Name="John"], [ID=2, Name="Jane"]})
```

**Example**

```m
Table.FromRecords({[Product="A", Price=10], [Product="B", Price=20]})
// Creates a table from record values.
```


***

### **Table.FromRows**

**Syntax**

```m
Table.FromRows(rows as list, optional columns as any) as table
```

**Syntax + Placeholder**

```m
Table.FromRows({{1,"John"},{2,"Jane"}}, {"ID","Name"})
```

**Example**

```m
Table.FromRows({{101,"TV"},{102,"Laptop"}}, {"ProductID","Name"})
// Creates a table from lists of rows.
```


***

### **Table.FromValue**

**Syntax**

```m
Table.FromValue(value as any) as table
```

**Syntax + Placeholder**

```m
Table.FromValue("Hello")
```

**Example**

```m
Table.FromValue([Name="John", Age=30])
// Converts a record into a one-row table.
```


***

### **Table.Group**

**Syntax**

```m
Table.Group(table as table, keys as any, aggregates as list, optional groupKind as any, optional comparer as any) as table
```

**Syntax + Placeholder**

```m
Table.Group(Source, {"Region"}, {{"TotalSales", each List.Sum([Sales]), type number}})
```

**Example**

```m
Table.Group(Sales, {"Region"}, {{"Total", each List.Sum([Sales]), type number}})
// Groups Sales table by Region and sums Sales.
```


***

### **Table.HasColumns**

**Syntax**

```m
Table.HasColumns(table as table, columns as list) as logical
```

**Syntax + Placeholder**

```m
Table.HasColumns(Source, {"CustomerID"})
```

**Example**

```m
Table.HasColumns(Sales, {"Qty","Price"})
// Returns true if Sales contains both columns.
```


***

### **Table.Intersect**

**Syntax**

```m
Table.Intersect(tables as list, optional equationCriteria as any) as table
```

**Syntax + Placeholder**

```m
Table.Intersect({Table1, Table2})
```

**Example**

```m
Table.Intersect({Sales2023, Sales2024})
// Returns rows appearing in both tables.
```


***

### **Table.Join**

**Syntax**

```m
Table.Join(table1 as table, key1 as any, table2 as table, key2 as any, optional joinKind as number) as table
```

**Syntax + Placeholder**

```m
Table.Join(Orders, "CustomerID", Customers, "CustomerID", JoinKind.Inner)
```

**Example**

```m
Table.Join(Orders, "CustomerID", Customers, "CustomerID", JoinKind.LeftOuter)
// Joins Customers to Orders on CustomerID.
```


***

### **Table.LastN**

**Syntax**

```m
Table.LastN(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.LastN(Source, 5)
```

**Example**

```m
Table.LastN(Sales, 10)
// Returns last 10 rows.
```


***

### **Table.MatchesAllRows**

**Syntax**

```m
Table.MatchesAllRows(table as table, predicate as function) as logical
```

**Syntax + Placeholder**

```m
Table.MatchesAllRows(Source, each [Score] > 50)
```

**Example**

```m
Table.MatchesAllRows(Students, each [Marks] >= 40)
// Returns true if every row passes condition.
```


***

### **Table.MatchesAnyRows**

**Syntax**

```m
Table.MatchesAnyRows(table as table, predicate as function) as logical
```

**Syntax + Placeholder**

```m
Table.MatchesAnyRows(Source, each [Score] > 90)
```

**Example**

```m
Table.MatchesAnyRows(Students, each [Marks] >= 90)
// Returns true if at least one row matches condition.
```


***

### **Table.NestedJoin**

**Syntax**

```m
Table.NestedJoin(table1 as table, key1 as any, table2 as table, key2 as any, newColumn as text, optional joinKind as number) as table
```

**Syntax + Placeholder**

```m
Table.NestedJoin(Orders, "CustomerID", Customers, "CustomerID", "Customer")
```

**Example**

```m
Table.NestedJoin(Orders, "CustomerID", Customers, "CustomerID", "Customer")
// Expands Customers inside Orders as nested table column.
```


***

### **Table.Partition**

**Syntax**

```m
Table.Partition(table as table, column as text, partitions as number, selector as function) as list
```

**Syntax + Placeholder**

```m
Table.Partition(Source, "Region", 3, each _ mod 3)
```

**Example**

```m
Table.Partition(Sales, "Region", 2, each if _ = "North" then 0 else 1)
// Divides table rows into partitions by Region.
```


***

### **Table.Pivot**

**Syntax**

```m
Table.Pivot(table as table, pivotValues as list, attributeColumn as text, valueColumn as text, optional aggregationFunction as function) as table
```

**Syntax + Placeholder**

```m
Table.Pivot(Source, {"Q1","Q2"}, "Quarter", "Sales", List.Sum)
```

**Example**

```m
Table.Pivot(Sales, {"North","South"}, "Region", "Amount", List.Sum)
// Pivots Region into new columns summing Amount.
```


***

### **Table.PositionOf**

**Syntax**

```m
Table.PositionOf(table as table, row as record, optional equationCriteria as any) as number
```

**Syntax + Placeholder**

```m
Table.PositionOf(Source, [ID=5])
```

**Example**

```m
Table.PositionOf(Orders, [OrderID=1001])
// Returns index of matching row.
```


***

### **Table.PositionOfAny**

**Syntax**

```m
Table.PositionOfAny(table as table, rows as list, optional equationCriteria as any) as number
```

**Syntax + Placeholder**

```m
Table.PositionOfAny(Source, {[ID=1],[ID=2]})
```

**Example**

```m
Table.PositionOfAny(Orders, {[OrderID=1001],[OrderID=1002]})
// Returns index of first match among specified rows.
```


***

### **Table.PrefixColumns**

**Syntax**

```m
Table.PrefixColumns(table as table, prefix as text) as table
```

**Syntax + Placeholder**

```m
Table.PrefixColumns(Source, "Sales_")
```

**Example**

```m
Table.PrefixColumns(Sales, "Region_")
// Renames columns by adding prefix.
```


***

### **Table.Profile**

**Syntax**

```m
Table.Profile(table as table, optional options as record) as table
```

**Syntax + Placeholder**

```m
Table.Profile(Source)
```

**Example**

```m
Table.Profile(Sales)
// Returns profiling metrics like count, min, max for each column.
```


***

### **Table.PromoteHeaders**

**Syntax**

```m
Table.PromoteHeaders(table as table, optional options as record) as table
```

**Syntax + Placeholder**

```m
Table.PromoteHeaders(Source)
```

**Example**

```m
Table.PromoteHeaders(MyTable)
// Promotes first row to headers.
```


***

### **Table.Range**

**Syntax**

```m
Table.Range(table as table, offset as number, optional count as number) as table
```

**Syntax + Placeholder**

```m
Table.Range(Source, 2, 5)
```

**Example**

```m
Table.Range(Sales, 3, 10)
// Skips 3 rows then takes 10 rows.
```


***

### **Table.RandomSample**

**Syntax**

```m
Table.RandomSample(table as table, percentage as number) as table
```

**Syntax + Placeholder**

```m
Table.RandomSample(Source, 0.1)
```

**Example**

```m
Table.RandomSample(Sales, 0.2)
// Returns random 20% sample.
```


***

### **Table.ReorderColumns**

**Syntax**

```m
Table.ReorderColumns(table as table, columns as list, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.ReorderColumns(Source, {"Name","Age","ID"})
```

**Example**

```m
Table.ReorderColumns(Employees, {"EmployeeID","Name","Department"})
// Rearranges column order.
```


***

### **Table.RemoveColumns**

**Syntax**

```m
Table.RemoveColumns(table as table, columns as list, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.RemoveColumns(Source, {"TempColumn"})
```

**Example**

```m
Table.RemoveColumns(Sales, {"Notes"})
// Removes Notes column.
```


***

### **Table.RemoveFirstN**

**Syntax**

```m
Table.RemoveFirstN(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.RemoveFirstN(Source, 5)
```

**Example**

```m
Table.RemoveFirstN(Sales, 10)
// Removes first 10 rows.
```


***

### **Table.RemoveLastN**

**Syntax**

```m
Table.RemoveLastN(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.RemoveLastN(Source, 3)
```

**Example**

```m
Table.RemoveLastN(Sales, 5)
// Removes last 5 rows.
```


***

### **Table.RemoveMatchingRows**

**Syntax**

```m
Table.RemoveMatchingRows(table as table, rows as table, optional equationCriteria as any) as table
```

**Syntax + Placeholder**

```m
Table.RemoveMatchingRows(Source, TableToRemove)
```

**Example**

```m
Table.RemoveMatchingRows(Sales, Returns)
// Removes rows in Returns from Sales.
```


***

### **Table.RemoveRows**

**Syntax**

```m
Table.RemoveRows(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.RemoveRows(Source, 4)
```

**Example**

```m
Table.RemoveRows(Sales, 2)
// Removes first 2 rows.
```


***

### **Table.RemoveRowsWithErrors**

**Syntax**

```m
Table.RemoveRowsWithErrors(table as table, optional columns as any) as table
```

**Syntax + Placeholder**

```m
Table.RemoveRowsWithErrors(Source, {"ColumnA"})
```

**Example**

```m
Table.RemoveRowsWithErrors(Sales)
// Removes rows containing any errors.
```


***

### **Table.RenameColumns**

**Syntax**

```m
Table.RenameColumns(table as table, renames as list, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.RenameColumns(Source, {{"OldName","NewName"}})
```

**Example**

```m
Table.RenameColumns(Employees, {{"FName","FirstName"},{"LName","LastName"}})
// Renames columns.
```


***

### **Table.ReplaceErrorValues**

**Syntax**

```m
Table.ReplaceErrorValues(table as table, replacements as list) as table
```

**Syntax + Placeholder**

```m
Table.ReplaceErrorValues(Source, {{"ColumnA",0}})
```

**Example**

```m
Table.ReplaceErrorValues(Sales, {{"Amount",0}})
// Replaces errors with default 0.
```


***

### **Table.ReplaceKeys**

**Syntax**

```m
Table.ReplaceKeys(table as table, keys as list) as table
```

**Syntax + Placeholder**

```m
Table.ReplaceKeys(Source, {{"CustomerID", true}})
```

**Example**

```m
Table.ReplaceKeys(Customers, {{"CustomerID", true}})
// Replaces the table keys with new key definition.
```


***

### **Table.ReplaceMatchingRows**

**Syntax**

```m
Table.ReplaceMatchingRows(table as table, replacements as table, optional equationCriteria as any) as table
```

**Syntax + Placeholder**

```m
Table.ReplaceMatchingRows(Source, ReplacementTable)
```

**Example**

```m
Table.ReplaceMatchingRows(Sales, CorrectionData)
// Replaces rows in Sales with matching rows from CorrectionData.
```


***

### **Table.ReplaceValue**

**Syntax**

```m
Table.ReplaceValue(table as table, oldValue as any, newValue as any, replacer as function, columns as list) as table
```

**Syntax + Placeholder**

```m
Table.ReplaceValue(Source, "Unknown", "N/A", Replacer.ReplaceText, {"Region"})
```

**Example**

```m
Table.ReplaceValue(Employees, null, "NA", Replacer.ReplaceValue, {"Department"})
// Replaces null in Department with "NA".
```


***
### **Table.RowCount**

**Syntax**

```m
Table.RowCount(table as table) as number
```

**Syntax + Placeholder**

```m
Table.RowCount(Source)
```

**Example**

```m
Table.RowCount(Sales)
// Returns the number of rows in Sales.
```


***

### **Table.Schema**

**Syntax**

```m
Table.Schema(table as table) as table
```

**Syntax + Placeholder**

```m
Table.Schema(Source)
```

**Example**

```m
Table.Schema(Sales)
// Returns schema including Name, Type, etc.
```


***

### **Table.SelectColumns**

**Syntax**

```m
Table.SelectColumns(table as table, columns as any, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.SelectColumns(Source, {"Name","Age"})
```

**Example**

```m
Table.SelectColumns(Employees, {"EmployeeID","Name"})
// Selects only ID and Name columns.
```


***

### **Table.SelectRows**

**Syntax**

```m
Table.SelectRows(table as table, selector as function) as table
```

**Syntax + Placeholder**

```m
Table.SelectRows(Source, each [Age] > 30)
```

**Example**

```m
Table.SelectRows(Employees, each [Department] = "HR")
// Filters rows based on condition.
```


***

### **Table.SelectRowsWithErrors**

**Syntax**

```m
Table.SelectRowsWithErrors(table as table, optional columns as any) as table
```

**Syntax + Placeholder**

```m
Table.SelectRowsWithErrors(Source, {"ColumnA"})
```

**Example**

```m
Table.SelectRowsWithErrors(Sales)
// Returns only rows containing errors.
```


***

### **Table.Skip**

**Syntax**

```m
Table.Skip(table as table, count as number) as table
```

**Syntax + Placeholder**

```m
Table.Skip(Source, 5)
```

**Example**

```m
Table.Skip(Sales, 10)
// Skips first 10 rows.
```


***

### **Table.Sort**

**Syntax**

```m
Table.Sort(table as table, order as list, optional comparer as any) as table
```

**Syntax + Placeholder**

```m
Table.Sort(Source, {{"Sales", Order.Ascending}})
```

**Example**

```m
Table.Sort(Sales, {{"Amount", Order.Descending}})
// Sorts Sales in descending order by Amount.
```


***

### **Table.SplitColumn**

**Syntax**

```m
Table.SplitColumn(table as table, column as text, splitter as function, optional newColumnNames as list, optional default as any, optional extraValues as any) as table
```

**Syntax + Placeholder**

```m
Table.SplitColumn(Source, "FullName", Splitter.SplitTextByDelimiter(" "), {"FirstName","LastName"})
```

**Example**

```m
Table.SplitColumn(Employees, "FullName", Splitter.SplitTextByEachDelimiter({" "}), {"FirstName","LastName"})
// Splits FullName into two columns.
```


***

### **Table.ToColumns**

**Syntax**

```m
Table.ToColumns(table as table) as list
```

**Syntax + Placeholder**

```m
Table.ToColumns(Source)
```

**Example**

```m
Table.ToColumns(Sales)
// Converts columns into a list of lists.
```


***

### **Table.ToRecords**

**Syntax**

```m
Table.ToRecords(table as table) as list
```

**Syntax + Placeholder**

```m
Table.ToRecords(Source)
```

**Example**

```m
Table.ToRecords(Sales)
// Converts table rows into records.
```


***

### **Table.ToRows**

**Syntax**

```m
Table.ToRows(table as table) as list
```

**Syntax + Placeholder**

```m
Table.ToRows(Source)
```

**Example**

```m
Table.ToRows(Sales)
// Converts table into list of row-lists.
```


***

### **Table.TransformColumnNames**

**Syntax**

```m
Table.TransformColumnNames(table as table, nameGenerator as function, optional comparer as any) as table
```

**Syntax + Placeholder**

```m
Table.TransformColumnNames(Source, Text.Upper)
```

**Example**

```m
Table.TransformColumnNames(Sales, each "Col_" & _)
// Renames each column with prefix "Col_".
```


***

### **Table.TransformColumns**

**Syntax**

```m
Table.TransformColumns(table as table, transformations as list, optional defaultTransformation as any, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.TransformColumns(Source, {{"Price", each _ * 1.1, type number}})
```

**Example**

```m
Table.TransformColumns(Sales, {{"Amount", each _ * 1.05, type number}})
// Increases Amount by 5%.
```


***

### **Table.TransformColumnTypes**

**Syntax**

```m
Table.TransformColumnTypes(table as table, typeTransformations as list, optional culture as text, optional missingField as any) as table
```

**Syntax + Placeholder**

```m
Table.TransformColumnTypes(Source, {{"Date", type date}})
```

**Example**

```m
Table.TransformColumnTypes(Sales, {{"OrderDate", type date}, {"Amount", type number}})
// Converts data types of columns.
```


***

### **Table.Transpose**

**Syntax**

```m
Table.Transpose(table as table) as table
```

**Syntax + Placeholder**

```m
Table.Transpose(Source)
```

**Example**

```m
Table.Transpose(Sales)
// Converts rows to columns and vice versa.
```


***

### **Table.Union**

**Syntax**

```m
Table.Union(tables as list) as table
```

**Syntax + Placeholder**

```m
Table.Union({Table1, Table2})
```

**Example**

```m
Table.Union({Sales2023, Sales2024})
// Combines all rows, retaining duplicates.
```


***

### **Table.Unpivot**

**Syntax**

```m
Table.Unpivot(table as table, pivotColumns as list, attributeColumn as text, valueColumn as text) as table
```

**Syntax + Placeholder**

```m
Table.Unpivot(Source, {"Q1","Q2","Q3","Q4"}, "Quarter", "Sales")
```

**Example**

```m
Table.Unpivot(Sales, {"Jan","Feb","Mar"}, "Month", "Value")
// Converts wide columns into long format.
```


***

### **Table.UnpivotColumns**

**Syntax**

```m
Table.UnpivotColumns(table as table, pivotColumns as list, attributeColumn as text, valueColumn as text) as table
```

**Syntax + Placeholder**

```m
Table.UnpivotColumns(Source, {"Column1","Column2"}, "Attribute", "Value")
```

**Example**

```m
Table.UnpivotColumns(Sales, {"Q1","Q2"}, "Quarter","Revenue")
// Makes selected columns unpivoted.
```


***

### **Table.UnpivotOtherColumns**

**Syntax**

```m
Table.UnpivotOtherColumns(table as table, keyColumns as list, attributeColumn as text, valueColumn as text) as table
```

**Syntax + Placeholder**

```m
Table.UnpivotOtherColumns(Source, {"ID"}, "Quarter", "Sales")
```

**Example**

```m
Table.UnpivotOtherColumns(Sales, {"Product"}, "Month","Value")
// Keeps Product column and unpivots others.
```


***

### **Table.View**

**Syntax**

```m
Table.View(name as text, handlers as record) as table
```

**Syntax + Placeholder**

```m
Table.View("MyView", [GetType = ()=> Table.Type, GetRows = ()=> {}])
```

**Example**

```m
Table.View("CustomView", [GetType = ()=> Table.Type, GetRows = ()=> {{1,"A"},{2,"B"}}])
// Defines a custom query table view.
```


***
<section id="-text-functions"><h2>📂 Text Functions</h2></section>


***

### **Text.Upper**

**Syntax**

```m
Text.Upper(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Upper("hello world")
```

**Example**

```m
Text.Upper("power query")
// Output: "POWER QUERY"
```


***

### **Text.Lower**

**Syntax**

```m
Text.Lower(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Lower("HELLO")
```

**Example**

```m
Text.Lower("WORLD")
// Output: "world"
```


***

### **Text.Proper**

**Syntax**

```m
Text.Proper(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Proper("hello world")
```

**Example**

```m
Text.Proper("power query m language")
// Output: "Power Query M Language"
```


***

### **Text.Trim**

**Syntax**

```m
Text.Trim(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Trim("  hello  ")
```

**Example**

```m
Text.Trim("  World  ")
// Output: "World"
```


***

### **Text.TrimStart**

**Syntax**

```m
Text.TrimStart(text as text, optional trimChars as any) as text
```

**Syntax + Placeholder**

```m
Text.TrimStart("  hello  ")
```

**Example**

```m
Text.TrimStart("  Power Query")
// Output: "Power Query"
```


***

### **Text.TrimEnd**

**Syntax**

```m
Text.TrimEnd(text as text, optional trimChars as any) as text
```

**Syntax + Placeholder**

```m
Text.TrimEnd("test   ")
```

**Example**

```m
Text.TrimEnd("World   ")
// Output: "World"
```


***

### **Text.Clean**

**Syntax**

```m
Text.Clean(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Clean("hello" & Character.FromNumber(10))
```

**Example**

```m
Text.Clean("Power" & Character.FromNumber(10) & "Query")
// Removes non-printable characters.
```


***

### **Text.Length**

**Syntax**

```m
Text.Length(text as text) as number
```

**Syntax + Placeholder**

```m
Text.Length("hello world")
```

**Example**

```m
Text.Length("Power")
// Output: 5
```


***

### **Text.Start**

**Syntax**

```m
Text.Start(text as text, count as number) as text
```

**Syntax + Placeholder**

```m
Text.Start("HelloWorld", 5)
```

**Example**

```m
Text.Start("PowerQuery", 5)
// Output: "Power"
```


***

### **Text.End**

**Syntax**

```m
Text.End(text as text, count as number) as text
```

**Syntax + Placeholder**

```m
Text.End("HelloWorld", 5)
```

**Example**

```m
Text.End("PowerQuery", 5)
// Output: "Query"
```


***

### **Text.Middle**

**Syntax**

```m
Text.Middle(text as text, start as number, count as number) as text
```

**Syntax + Placeholder**

```m
Text.Middle("HelloWorld", 1, 4)
```

**Example**

```m
Text.Middle("PowerQuery", 5, 5)
// Output: "Query"
```


***

### **Text.Range**

**Syntax**

```m
Text.Range(text as text, start as number, optional count as number) as text
```

**Syntax + Placeholder**

```m
Text.Range("Hello", 1, 3)
```

**Example**

```m
Text.Range("PowerQuery", 0, 5)
// Output: "Power"
```


***

### **Text.PositionOf**

**Syntax**

```m
Text.PositionOf(text as text, substring as text, optional comparer as any) as number
```

**Syntax + Placeholder**

```m
Text.PositionOf("HelloWorld", "World")
```

**Example**

```m
Text.PositionOf("Power Query", "Query")
// Output: 6
```


***

### **Text.PositionOfAny**

**Syntax**

```m
Text.PositionOfAny(text as text, characters as list, optional comparer as any) as number
```

**Syntax + Placeholder**

```m
Text.PositionOfAny("HelloWorld", {"o","W"})
```

**Example**

```m
Text.PositionOfAny("PowerQuery", {"Q","z"})
// Output: 5 (position of Q)
```


***
### **Text.BeforeDelimiter**

**Syntax**

```m
Text.BeforeDelimiter(text as text, delimiter as text, optional occurrence as any) as text
```

**Syntax + Placeholder**

```m
Text.BeforeDelimiter("John,Doe", ",")
```

**Example**

```m
Text.BeforeDelimiter("Power-Query-M", "-")
// Output: "Power"
```


***

### **Text.AfterDelimiter**

**Syntax**

```m
Text.AfterDelimiter(text as text, delimiter as text, optional occurrence as any) as text
```

**Syntax + Placeholder**

```m
Text.AfterDelimiter("John,Doe", ",")
```

**Example**

```m
Text.AfterDelimiter("Power-Query-M", "-")
// Output: "Query-M"
```


***

### **Text.BetweenDelimiters**

**Syntax**

```m
Text.BetweenDelimiters(text as text, start as text, end as text, optional startIndex as any, optional endIndex as any) as text
```

**Syntax + Placeholder**

```m
Text.BetweenDelimiters("(Hello)", "(", ")")
```

**Example**

```m
Text.BetweenDelimiters("Product[123]Data", "[", "]")
// Output: "123"
```


***

### **Text.Replace**

**Syntax**

```m
Text.Replace(text as text, old as text, new as text) as text
```

**Syntax + Placeholder**

```m
Text.Replace("Hello World", "World", "Power Query")
```

**Example**

```m
Text.Replace("Power BI", "BI", "Query")
// Output: "Power Query"
```


***

### **Text.ReplaceRange**

**Syntax**

```m
Text.ReplaceRange(text as text, offset as number, length as number, newText as text) as text
```

**Syntax + Placeholder**

```m
Text.ReplaceRange("Hello World", 6, 5, "Query")
```

**Example**

```m
Text.ReplaceRange("PowerBI", 5, 2, "Query")
// Output: "PowerQuery"
```


***

### **Text.ReplaceEach**

**Syntax**

```m
Text.ReplaceEach(text as text, replacements as list) as text
```

**Syntax + Placeholder**

```m
Text.ReplaceEach("Hello", {{"H","J"},{"e","a"}})
```

**Example**

```m
Text.ReplaceEach("Power BI", {{"Power","Query"},{"BI","M"}})
// Output: "Query M"
```


***

### **Text.Remove**

**Syntax**

```m
Text.Remove(text as text, removeChars as any) as text
```

**Syntax + Placeholder**

```m
Text.Remove("Hello World", {"o","l"})
```

**Example**

```m
Text.Remove("PowerQuery", {"e","u"})
// Output: "PwrQry"
```


***

### **Text.RemoveRange**

**Syntax**

```m
Text.RemoveRange(text as text, offset as number, count as number) as text
```

**Syntax + Placeholder**

```m
Text.RemoveRange("HelloWorld", 5, 5)
```

**Example**

```m
Text.RemoveRange("PowerQuery", 5, 5)
// Output: "Power"
```


***

### **Text.Split**

**Syntax**

```m
Text.Split(text as text, delimiter as text, optional quoteStyle as any) as list
```

**Syntax + Placeholder**

```m
Text.Split("A,B,C", ",")
```

**Example**

```m
Text.Split("Power Query M", " ")
// Output: {"Power","Query","M"}
```


***

### **Text.SplitAny**

**Syntax**

```m
Text.SplitAny(text as text, separators as any) as list
```

**Syntax + Placeholder**

```m
Text.SplitAny("One;Two,Three", {";",","})
```

**Example**

```m
Text.SplitAny("123-456/789", {"-","/"})
// Output: {"123","456","789"}
```


***

### **Text.SplitByLengths**

**Syntax**

```m
Text.SplitByLengths(text as text, lengths as list) as list
```

**Syntax + Placeholder**

```m
Text.SplitByLengths("123456", {2,2,2})
```

**Example**

```m
Text.SplitByLengths("PowerQuery", {5,5})
// Output: {"Power","Query"}
```


***

### **Text.SplitByPositions**

**Syntax**

```m
Text.SplitByPositions(text as text, positions as list) as list
```

**Syntax + Placeholder**

```m
Text.SplitByPositions("abcdef", {2,4})
```

**Example**

```m
Text.SplitByPositions("PowerQuery",{5})
// Output: {"Power","Query"}
```


***

### **Text.Combine**

**Syntax**

```m
Text.Combine(texts as list, optional delimiter as text) as text
```

**Syntax + Placeholder**

```m
Text.Combine({"A","B","C"}, ", ")
```

**Example**

```m
Text.Combine({"Power","Query","M"}, " ")
// Output: "Power Query M"
```


***

### **Text.Contains**

**Syntax**

```m
Text.Contains(text as text, substring as text, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
Text.Contains("Hello World", "World")
```

**Example**

```m
Text.Contains("Power Query","Query")
// Output: true
```


***

### **Text.StartsWith**

**Syntax**

```m
Text.StartsWith(text as text, substring as text, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
Text.StartsWith("HelloWorld", "Hello")
```

**Example**

```m
Text.StartsWith("PowerQuery","Power")
// Output: true
```


***

### **Text.EndsWith**

**Syntax**

```m
Text.EndsWith(text as text, substring as text, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
Text.EndsWith("HelloWorld", "World")
```

**Example**

```m
Text.EndsWith("PowerQuery","Query")
// Output: true
```


***

### **Text.Insert**

**Syntax**

```m
Text.Insert(text as text, position as number, newText as text) as text
```

**Syntax + Placeholder**

```m
Text.Insert("HelloWorld", 5, " ")
```

**Example**

```m
Text.Insert("PowerQuery", 5, " BI")
// Output: "Power BIQuery"
```


***

### **Text.PadStart**

**Syntax**

```m
Text.PadStart(text as text, length as number, optional pad as text) as text
```

**Syntax + Placeholder**

```m
Text.PadStart("123", 5, "0")
```

**Example**

```m
Text.PadStart("45", 4, "0")
// Output: "0045"
```


***

### **Text.PadEnd**

**Syntax**

```m
Text.PadEnd(text as text, length as number, optional pad as text) as text
```

**Syntax + Placeholder**

```m
Text.PadEnd("123", 5, "0")
```

**Example**

```m
Text.PadEnd("45", 4, "0")
// Output: "4500"
```


***

### **Text.ToList**

**Syntax**

```m
Text.ToList(text as text) as list
```

**Syntax + Placeholder**

```m
Text.ToList("ABC")
```

**Example**

```m
Text.ToList("Power")
// Output: {"P","o","w","e","r"}
```


***

### **Text.ToBinary**

**Syntax**

```m
Text.ToBinary(text as text, optional encoding as number) as binary
```

**Syntax + Placeholder**

```m
Text.ToBinary("Hello")
```

**Example**

```m
Text.ToBinary("Data")
// Converts text to binary.
```


***

### **Text.FromBinary**

**Syntax**

```m
Text.FromBinary(binary as binary, optional encoding as number) as text
```

**Syntax + Placeholder**

```m
Text.FromBinary(Text.ToBinary("Hello"))
```

**Example**

```m
Text.FromBinary(Text.ToBinary("Power"))
// Output: "Power"
```


***

### **Text.From**

**Syntax**

```m
Text.From(value as any, optional culture as text) as text
```

**Syntax + Placeholder**

```m
Text.From(1234)
```

**Example**

```m
Text.From(#date(2025,8,20))
// Output: "8/20/2025" (depending on culture)
```


***

### **Text.NewGuid**

**Syntax**

```m
Text.NewGuid() as text
```

**Syntax + Placeholder**

```m
Text.NewGuid()
```

**Example**

```m
Text.NewGuid()
// Output: "550e8400-e29b-41d4-a716-446655440000" (random GUID)
```


***

### **Text.Format**

**Syntax**

```m
Text.Format(formatString as text, arguments as any) as text
```

**Syntax + Placeholder**

```m
Text.Format("Hello {0}", {"World"})
```

**Example**

```m
Text.Format("{0} scored {1}", {"John", 95})
// Output: "John scored 95"
```


***

### **Text.Repeat**

**Syntax**

```m
Text.Repeat(text as text, count as number) as text
```

**Syntax + Placeholder**

```m
Text.Repeat("Hi", 3)
```

**Example**

```m
Text.Repeat("PQ", 4)
// Output: "PQPQPQPQ"
```


***

### **Text.Select**

**Syntax**

```m
Text.Select(text as text, selectChars as any) as text
```

**Syntax + Placeholder**

```m
Text.Select("Hello World", {"H","e","l"})
```

**Example**

```m
Text.Select("PowerQuery", {"o","e","r"})
// Output: "oer"
```


***

### **Text.Normalize**

**Syntax**

```m
Text.Normalize(text as text) as text
```

**Syntax + Placeholder**

```m
Text.Normalize("café")
```

**Example**

```m
Text.Normalize("café")
// Normalizes accented characters for comparison.
```


***

### **Text.AccentInsensitiveCompare**

**Syntax**

```m
Text.AccentInsensitiveCompare(a as text, b as text) as number
```

**Syntax + Placeholder**

```m
Text.AccentInsensitiveCompare("café","cafe")
```

**Example**

```m
Text.AccentInsensitiveCompare("résumé","resume")
// Output: 0 (equal ignoring accents)
```


***

### **Text.CollatorFromCulture**

**Syntax**

```m
Text.CollatorFromCulture(culture as text, optional options as record) as any
```

**Syntax + Placeholder**

```m
Text.CollatorFromCulture("en-US")
```

**Example**

```m
Text.CollatorFromCulture("fr-FR")
// Returns a text comparer for given culture.
```
***
<section id="-number-functions"><h2>📂 Number Functions</h2></section>


***

### **Number.Abs**

**Syntax**

```m
Number.Abs(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Abs(-10)
```

**Example**

```m
Number.Abs(-25)
// Output: 25
```


***

### **Number.Power**

**Syntax**

```m
Number.Power(number as nullable number, exponent as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Power(2, 3)
```

**Example**

```m
Number.Power(5, 2)
// Output: 25
```


***

### **Number.Sqrt**

**Syntax**

```m
Number.Sqrt(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Sqrt(16)
```

**Example**

```m
Number.Sqrt(25)
// Output: 5
```


***

### **Number.Mod**

**Syntax**

```m
Number.Mod(number as nullable number, divisor as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Mod(10, 3)
```

**Example**

```m
Number.Mod(20, 6)
// Output: 2
```


***

### **Number.Sign**

**Syntax**

```m
Number.Sign(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Sign(-5)
```

**Example**

```m
Number.Sign(10)
// Output: 1
```


***

### **Number.Log**

**Syntax**

```m
Number.Log(number as nullable number, optional base as any) as nullable number
```

**Syntax + Placeholder**

```m
Number.Log(100, 10)
```

**Example**

```m
Number.Log(16, 2)
// Output: 4
```


***

### **Number.Ln**

**Syntax**

```m
Number.Ln(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Ln(5)
```

**Example**

```m
Number.Ln(1)
// Output: 0
```


***

### **Number.Log10**

**Syntax**

```m
Number.Log10(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Log10(1000)
```

**Example**

```m
Number.Log10(100)
// Output: 2
```


***

### **Number.Exp**

**Syntax**

```m
Number.Exp(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Exp(1)
```

**Example**

```m
Number.Exp(2)
// Output: 7.389056...
```


***

### **Number.Round**

**Syntax**

```m
Number.Round(number as nullable number, optional digits as nullable number, optional roundingMode as any) as nullable number
```

**Syntax + Placeholder**

```m
Number.Round(3.14159, 2)
```

**Example**

```m
Number.Round(2.71828, 3)
// Output: 2.718
```


***

### **Number.RoundUp**

**Syntax**

```m
Number.RoundUp(number as nullable number, optional digits as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.RoundUp(3.14159, 2)
```

**Example**

```m
Number.RoundUp(2.11, 1)
// Output: 2.2
```


***

### **Number.RoundDown**

**Syntax**

```m
Number.RoundDown(number as nullable number, optional digits as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.RoundDown(3.14159, 2)
```

**Example**

```m
Number.RoundDown(2.99, 0)
// Output: 2
```


***

### **Number.RoundTowardZero**

**Syntax**

```m
Number.RoundTowardZero(number as nullable number, optional digits as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.RoundTowardZero(-3.75, 0)
```

**Example**

```m
Number.RoundTowardZero(-2.9, 0)
// Output: -2
```


***

### **Number.RoundAwayFromZero**

**Syntax**

```m
Number.RoundAwayFromZero(number as nullable number, optional digits as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.RoundAwayFromZero(-3.75, 0)
```

**Example**

```m
Number.RoundAwayFromZero(2.5, 0)
// Output: 3
```


***

### **Number.From**

**Syntax**

```m
Number.From(value as any, optional culture as text) as nullable number
```

**Syntax + Placeholder**

```m
Number.From("123")
```

**Example**

```m
Number.From("3.14")
// Output: 3.14
```


***

### **Number.FromText**

**Syntax**

```m
Number.FromText(text as text, optional culture as text) as nullable number
```

**Syntax + Placeholder**

```m
Number.FromText("123.45")
```

**Example**

```m
Number.FromText("99")
// Output: 99
```


***

### **Number.ToText**

**Syntax**

```m
Number.ToText(number as nullable number, optional format as any, optional culture as text) as nullable text
```

**Syntax + Placeholder**

```m
Number.ToText(1234.56, "N2")
```

**Example**

```m
Number.ToText(1000, "D")
// Output: "1000"
```


***

### **Number.IntegerDivide**

**Syntax**

```m
Number.IntegerDivide(number as nullable number, divisor as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.IntegerDivide(10, 3)
```

**Example**

```m
Number.IntegerDivide(20, 6)
// Output: 3
```


***

### **Number.Divide**

**Syntax**

```m
Number.Divide(number as nullable number, divisor as nullable number, optional precision as any) as nullable number
```

**Syntax + Placeholder**

```m
Number.Divide(22, 7)
```

**Example**

```m
Number.Divide(10, 2)
// Output: 5
```


***

### **Number.IsNaN**

**Syntax**

```m
Number.IsNaN(number as any) as logical
```

**Syntax + Placeholder**

```m
Number.IsNaN(0/0)
```

**Example**

```m
Number.IsNaN(Number.FromText("abc"))
// Output: true
```


***

### **Number.IsEven**

**Syntax**

```m
Number.IsEven(number as nullable number) as logical
```

**Syntax + Placeholder**

```m
Number.IsEven(10)
```

**Example**

```m
Number.IsEven(7)
// Output: false
```


***

### **Number.IsOdd**

**Syntax**

```m
Number.IsOdd(number as nullable number) as logical
```

**Syntax + Placeholder**

```m
Number.IsOdd(5)
```

**Example**

```m
Number.IsOdd(10)
// Output: false
```


***

### **Number.IsNull**

**Syntax**

```m
Number.IsNull(value as any) as logical
```

**Syntax + Placeholder**

```m
Number.IsNull(null)
```

**Example**

```m
Number.IsNull(5)
// Output: false
```


***

### **Number.IsFinite**

**Syntax**

```m
Number.IsFinite(number as any) as logical
```

**Syntax + Placeholder**

```m
Number.IsFinite(1/0)
```

**Example**

```m
Number.IsFinite(10)
// Output: true
```


***

### **Number.IsInfinity**

**Syntax**

```m
Number.IsInfinity(number as any) as logical
```

**Syntax + Placeholder**

```m
Number.IsInfinity(1/0)
```

**Example**

```m
Number.IsInfinity(0/0)
// Output: false
```


***

### **Number.Random**

**Syntax**

```m
Number.Random() as number
```

**Syntax + Placeholder**

```m
Number.Random()
```

**Example**

```m
Number.Random()
// Output: e.g. 0.4567 (random between 0 and 1)
```


***

### **Number.RandomBetween**

**Syntax**

```m
Number.RandomBetween(min as number, max as number) as number
```

**Syntax + Placeholder**

```m
Number.RandomBetween(1, 10)
```

**Example**

```m
Number.RandomBetween(100, 200)
// Output: e.g. 157
```


***

### **Number.Acos**

**Syntax**

```m
Number.Acos(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Acos(1)
```

**Example**

```m
Number.Acos(0)
// Output: 1.5708 (π/2)
```


***

### **Number.Asin**

**Syntax**

```m
Number.Asin(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Asin(0.5)
```

**Example**

```m
Number.Asin(1)
// Output: 1.5708 (π/2)
```


***

### **Number.Atan**

**Syntax**

```m
Number.Atan(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Atan(1)
```

**Example**

```m
Number.Atan(0)
// Output: 0
```


***

### **Number.Cos**

**Syntax**

```m
Number.Cos(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Cos(0)
```

**Example**

```m
Number.Cos(3.14159)
// Output: -1
```


***

### **Number.Sin**

**Syntax**

```m
Number.Sin(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Sin(1)
```

**Example**

```m
Number.Sin(0)
// Output: 0
```


***

### **Number.Tan**

**Syntax**

```m
Number.Tan(number as nullable number) as nullable number
```

**Syntax + Placeholder**

```m
Number.Tan(1)
```

**Example**

```m
Number.Tan(0)
// Output: 0
```


***

### **Number.BitwiseAnd**

**Syntax**

```m
Number.BitwiseAnd(a as number, b as number) as number
```

**Syntax + Placeholder**

```m
Number.BitwiseAnd(6, 3)
```

**Example**

```m
Number.BitwiseAnd(5, 1)
// Output: 1
```


***

### **Number.BitwiseOr**

**Syntax**

```m
Number.BitwiseOr(a as number, b as number) as number
```

**Syntax + Placeholder**

```m
Number.BitwiseOr(6, 3)
```

**Example**

```m
Number.BitwiseOr(4, 1)
// Output: 5
```


***

### **Number.BitwiseXor**

**Syntax**

```m
Number.BitwiseXor(a as number, b as number) as number
```

**Syntax + Placeholder**

```m
Number.BitwiseXor(6, 3)
```

**Example**

```m
Number.BitwiseXor(4, 5)
// Output: 1
```


***
<section id="-date-functions"><h2>📂 Date Functions</h2></section>


***

### **Date.Year**

**Syntax**

```m
Date.Year(date as date) as number
```

**Syntax + Placeholder**

```m
Date.Year(#date(2025, 8, 20))
```

**Example**

```m
Date.Year(#date(2023, 5, 10))
// Output: 2023
```


***

### **Date.Month**

**Syntax**

```m
Date.Month(date as date) as number
```

**Syntax + Placeholder**

```m
Date.Month(#date(2025, 8, 20))
```

**Example**

```m
Date.Month(#date(2023, 5, 10))
// Output: 5
```


***

### **Date.Day**

**Syntax**

```m
Date.Day(date as date) as number
```

**Syntax + Placeholder**

```m
Date.Day(#date(2025, 8, 20))
```

**Example**

```m
Date.Day(#date(2023, 5, 10))
// Output: 10
```


***

### **Date.DayOfWeek**

**Syntax**

```m
Date.DayOfWeek(date as date, optional firstDayOfWeek as any) as number
```

**Syntax + Placeholder**

```m
Date.DayOfWeek(#date(2025, 8, 20), Day.Sunday)
```

**Example**

```m
Date.DayOfWeek(#date(2023, 5, 15))
// Output: 1 (Monday if Sunday is first day)
```


***

### **Date.DayOfYear**

**Syntax**

```m
Date.DayOfYear(date as date) as number
```

**Syntax + Placeholder**

```m
Date.DayOfYear(#date(2025, 8, 20))
```

**Example**

```m
Date.DayOfYear(#date(2023, 5, 10))
// Output: 130 (depending on year)
```


***

### **Date.WeekOfYear**

**Syntax**

```m
Date.WeekOfYear(date as date, optional firstDayOfWeek as any) as number
```

**Syntax + Placeholder**

```m
Date.WeekOfYear(#date(2025, 8, 20), Day.Sunday)
```

**Example**

```m
Date.WeekOfYear(#date(2023, 5, 10))
// Output: 19 (19th week of the year)
```


***

### **Date.WeekOfMonth**

**Syntax**

```m
Date.WeekOfMonth(date as date, optional firstDayOfWeek as any) as number
```

**Syntax + Placeholder**

```m
Date.WeekOfMonth(#date(2025, 8, 20))
```

**Example**

```m
Date.WeekOfMonth(#date(2023, 5, 15))
// Output: 3 (third week of May)
```


***

### **Date.QuarterOfYear**

**Syntax**

```m
Date.QuarterOfYear(date as date) as number
```

**Syntax + Placeholder**

```m
Date.QuarterOfYear(#date(2025, 8, 20))
```

**Example**

```m
Date.QuarterOfYear(#date(2023, 5, 10))
// Output: 2
```


***

### **Date.StartOfDay**

**Syntax**

```m
Date.StartOfDay(date as date) as datetime
```

**Syntax + Placeholder**

```m
Date.StartOfDay(#date(2025, 8, 20))
```

**Example**

```m
Date.StartOfDay(#date(2023, 5, 10))
// Output: 2023-05-10 00:00:00
```


***

### **Date.EndOfDay**

**Syntax**

```m
Date.EndOfDay(date as date) as datetime
```

**Syntax + Placeholder**

```m
Date.EndOfDay(#date(2025, 8, 20))
```

**Example**

```m
Date.EndOfDay(#date(2023, 5, 10))
// Output: 2023-05-10 23:59:59
```


***

### **Date.StartOfWeek**

**Syntax**

```m
Date.StartOfWeek(date as date, optional firstDayOfWeek as any) as date
```

**Syntax + Placeholder**

```m
Date.StartOfWeek(#date(2025, 8, 20), Day.Monday)
```

**Example**

```m
Date.StartOfWeek(#date(2023, 5, 10))
// Output: 2023-05-08
```


***

### **Date.EndOfWeek**

**Syntax**

```m
Date.EndOfWeek(date as date, optional firstDayOfWeek as any) as date
```

**Syntax + Placeholder**

```m
Date.EndOfWeek(#date(2025, 8, 20), Day.Sunday)
```

**Example**

```m
Date.EndOfWeek(#date(2023, 5, 10))
// Output: 2023-05-14
```


***

### **Date.StartOfMonth**

**Syntax**

```m
Date.StartOfMonth(date as date) as date
```

**Syntax + Placeholder**

```m
Date.StartOfMonth(#date(2025, 8, 20))
```

**Example**

```m
Date.StartOfMonth(#date(2023, 5, 10))
// Output: 2023-05-01
```


***

### **Date.EndOfMonth**

**Syntax**

```m
Date.EndOfMonth(date as date) as date
```

**Syntax + Placeholder**

```m
Date.EndOfMonth(#date(2025, 8, 20))
```

**Example**

```m
Date.EndOfMonth(#date(2023, 2, 15))
// Output: 2023-02-28
```


***

### **Date.StartOfQuarter**

**Syntax**

```m
Date.StartOfQuarter(date as date) as date
```

**Syntax + Placeholder**

```m
Date.StartOfQuarter(#date(2025, 8, 20))
```

**Example**

```m
Date.StartOfQuarter(#date(2023, 5, 10))
// Output: 2023-04-01
```


***

### **Date.EndOfQuarter**

**Syntax**

```m
Date.EndOfQuarter(date as date) as date
```

**Syntax + Placeholder**

```m
Date.EndOfQuarter(#date(2025, 8, 20))
```

**Example**

```m
Date.EndOfQuarter(#date(2023, 5, 10))
// Output: 2023-06-30
```


***

### **Date.StartOfYear**

**Syntax**

```m
Date.StartOfYear(date as date) as date
```

**Syntax + Placeholder**

```m
Date.StartOfYear(#date(2025, 8, 20))
```

**Example**

```m
Date.StartOfYear(#date(2023, 5, 10))
// Output: 2023-01-01
```


***

### **Date.EndOfYear**

**Syntax**

```m
Date.EndOfYear(date as date) as date
```

**Syntax + Placeholder**

```m
Date.EndOfYear(#date(2025, 8, 20))
```

**Example**

```m
Date.EndOfYear(#date(2023, 5, 10))
// Output: 2023-12-31
```


***
### **Date.AddDays**

**Syntax**

```m
Date.AddDays(date as date, number as number) as date
```

**Syntax + Placeholder**

```m
Date.AddDays(#date(2025, 8, 20), 5)
```

**Example**

```m
Date.AddDays(#date(2023, 5, 10), 10)
// Output: 2023-05-20
```


***

### **Date.AddWeeks**

**Syntax**

```m
Date.AddWeeks(date as date, number as number) as date
```

**Syntax + Placeholder**

```m
Date.AddWeeks(#date(2025, 8, 20), 2)
```

**Example**

```m
Date.AddWeeks(#date(2023, 5, 10), 4)
// Output: 2023-06-07
```


***

### **Date.AddMonths**

**Syntax**

```m
Date.AddMonths(date as date, number as number) as date
```

**Syntax + Placeholder**

```m
Date.AddMonths(#date(2025, 8, 20), 3)
```

**Example**

```m
Date.AddMonths(#date(2023, 5, 10), 6)
// Output: 2023-11-10
```


***

### **Date.AddQuarters**

**Syntax**

```m
Date.AddQuarters(date as date, number as number) as date
```

**Syntax + Placeholder**

```m
Date.AddQuarters(#date(2025, 8, 20), 1)
```

**Example**

```m
Date.AddQuarters(#date(2023, 5, 10), 2)
// Output: 2023-11-10
```


***

### **Date.AddYears**

**Syntax**

```m
Date.AddYears(date as date, number as number) as date
```

**Syntax + Placeholder**

```m
Date.AddYears(#date(2025, 8, 20), 1)
```

**Example**

```m
Date.AddYears(#date(2023, 5, 10), 5)
// Output: 2028-05-10
```


***

### **Date.From**

**Syntax**

```m
Date.From(value as any) as date
```

**Syntax + Placeholder**

```m
Date.From("2025-08-20")
```

**Example**

```m
Date.From(#datetime(2023,5,10,12,30,00))
// Output: 2023-05-10
```


***

### **Date.FromText**

**Syntax**

```m
Date.FromText(text as text, optional culture as text) as date
```

**Syntax + Placeholder**

```m
Date.FromText("08/20/2025", "en-US")
```

**Example**

```m
Date.FromText("10-05-2023", "en-GB")
// Output: 2023-05-10
```


***

### **Date.FromParts**

**Syntax**

```m
Date.FromParts(year as number, month as number, day as number) as date
```

**Syntax + Placeholder**

```m
Date.FromParts(2025, 8, 20)
```

**Example**

```m
Date.FromParts(2023, 5, 10)
// Output: 2023-05-10
```


***

### **Date.ToText**

**Syntax**

```m
Date.ToText(date as date, optional format as any, optional culture as text) as text
```

**Syntax + Placeholder**

```m
Date.ToText(#date(2025, 8, 20), "MM/dd/yyyy")
```

**Example**

```m
Date.ToText(#date(2023, 5, 10), "yyyy-MM-dd")
// Output: "2023-05-10"
```


***

### **Date.IsInCurrentDay**

**Syntax**

```m
Date.IsInCurrentDay(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInCurrentDay(DateTime.Date(DateTime.LocalNow()))
```

**Example**

```m
Date.IsInCurrentDay(DateTime.Date(DateTime.LocalNow()))
// Output: true (if date = today)
```


***

### **Date.IsInCurrentWeek**

**Syntax**

```m
Date.IsInCurrentWeek(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInCurrentWeek(#date(2025, 8, 20))
```

**Example**

```m
Date.IsInCurrentWeek(DateTime.Date(DateTime.LocalNow()))
// Output: true (if within current week)
```


***

### **Date.IsInCurrentMonth**

**Syntax**

```m
Date.IsInCurrentMonth(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInCurrentMonth(#date(2025, 8, 20))
```

**Example**

```m
Date.IsInCurrentMonth(DateTime.Date(DateTime.LocalNow()))
// Output: true (if within current month)
```


***

### **Date.IsInCurrentQuarter**

**Syntax**

```m
Date.IsInCurrentQuarter(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInCurrentQuarter(#date(2025, 8, 20))
```

**Example**

```m
Date.IsInCurrentQuarter(DateTime.Date(DateTime.LocalNow()))
// Output: true (if within current quarter)
```


***

### **Date.IsInCurrentYear**

**Syntax**

```m
Date.IsInCurrentYear(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInCurrentYear(#date(2025, 8, 20))
```

**Example**

```m
Date.IsInCurrentYear(DateTime.Date(DateTime.LocalNow()))
// Output: true (if within same year)
```


***

### **Date.IsInNextDay**

**Syntax**

```m
Date.IsInNextDay(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextDay(Date.AddDays(DateTime.Date(DateTime.LocalNow()), 1))
```

**Example**

```m
Date.IsInNextDay(#date(2023,5,11))
// Output: true if tomorrow
```


***

### **Date.IsInNextWeek**

**Syntax**

```m
Date.IsInNextWeek(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextWeek(#date(2025, 8, 27))
```

**Example**

```m
Date.IsInNextWeek(Date.AddDays(DateTime.Date(DateTime.LocalNow()), 7))
// Output: true if next calendar week
```


***

### **Date.IsInNextMonth**

**Syntax**

```m
Date.IsInNextMonth(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextMonth(#date(2025, 9, 1))
```

**Example**

```m
Date.IsInNextMonth(Date.AddMonths(DateTime.Date(DateTime.LocalNow()), 1))
// Output: true if in next month
```


***

### **Date.IsInNextQuarter**

**Syntax**

```m
Date.IsInNextQuarter(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextQuarter(#date(2025, 10, 1))
```

**Example**

```m
Date.IsInNextQuarter(Date.AddQuarters(DateTime.Date(DateTime.LocalNow()), 1))
// Output: true if in next quarter
```


***

### **Date.IsInNextYear**

**Syntax**

```m
Date.IsInNextYear(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextYear(#date(2026, 1, 1))
```

**Example**

```m
Date.IsInNextYear(Date.AddYears(DateTime.Date(DateTime.LocalNow()), 1))
// Output: true if in next year
```


***

### **Date.IsInPreviousDay**

**Syntax**

```m
Date.IsInPreviousDay(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousDay(#date(2025, 8, 19))
```

**Example**

```m
Date.IsInPreviousDay(Date.AddDays(DateTime.Date(DateTime.LocalNow()), -1))
// Output: true if yesterday
```


***

### **Date.IsInPreviousWeek**

**Syntax**

```m
Date.IsInPreviousWeek(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousWeek(#date(2025, 8, 13))
```

**Example**

```m
Date.IsInPreviousWeek(Date.AddDays(DateTime.Date(DateTime.LocalNow()), -7))
// Output: true if in last week
```


***

### **Date.IsInPreviousMonth**

**Syntax**

```m
Date.IsInPreviousMonth(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousMonth(#date(2025, 7, 15))
```

**Example**

```m
Date.IsInPreviousMonth(Date.AddMonths(DateTime.Date(DateTime.LocalNow()), -1))
// Output: true if previous month
```


***

### **Date.IsInPreviousQuarter**

**Syntax**

```m
Date.IsInPreviousQuarter(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousQuarter(#date(2025, 4, 1))
```

**Example**

```m
Date.IsInPreviousQuarter(Date.AddQuarters(DateTime.Date(DateTime.LocalNow()), -1))
// Output: true if last quarter
```


***

### **Date.IsInPreviousYear**

**Syntax**

```m
Date.IsInPreviousYear(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousYear(#date(2024, 12, 31))
```

**Example**

```m
Date.IsInPreviousYear(Date.AddYears(DateTime.Date(DateTime.LocalNow()), -1))
// Output: true if last year
```


***

### **Date.IsInYearToDate**

**Syntax**

```m
Date.IsInYearToDate(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsInYearToDate(#date(2025, 8, 20))
```

**Example**

```m
Date.IsInYearToDate(#date(2023,4,1))
// Output: true if inside YTD
```


***

### **Date.IsLeapYear**

**Syntax**

```m
Date.IsLeapYear(date as date) as logical
```

**Syntax + Placeholder**

```m
Date.IsLeapYear(#date(2024, 1, 1))
```

**Example**

```m
Date.IsLeapYear(#date(2023, 1, 1))
// Output: false
```


***

### **Date.IsInPreviousNMonths**

**Syntax**

```m
Date.IsInPreviousNMonths(date as date, n as number) as logical
```

**Syntax + Placeholder**

```m
Date.IsInPreviousNMonths(#date(2025, 6, 1), 2)
```

**Example**

```m
Date.IsInPreviousNMonths(DateTime.Date(DateTime.LocalNow()), 3)
// Returns true if within last 3 months
```


***

### **Date.IsInNextNMonths**

**Syntax**

```m
Date.IsInNextNMonths(date as date, n as number) as logical
```

**Syntax + Placeholder**

```m
Date.IsInNextNMonths(#date(2025, 11, 1), 3)
```

**Example**

```m
Date.IsInNextNMonths(#date(2023,7,10), 2)
// Returns true if within next 2 months
```


***

### **Date.IsInMonth**

**Syntax**

```m
Date.IsInMonth(date as date, month as number) as logical
```

**Syntax + Placeholder**

```m
Date.IsInMonth(#date(2025, 8, 20), 8)
```

**Example**

```m
Date.IsInMonth(#date(2023,8,15), 8)
// Output: true
```


***
<section id="-time-functions"><h2>📂 Time Functions</h2></section>


***

### **Time.Hour**

**Syntax**

```m
Time.Hour(time as time) as number
```

**Syntax + Placeholder**

```m
Time.Hour(#time(14, 30, 45))
```

**Example**

```m
Time.Hour(#time(18, 45, 00))
// Output: 18
```


***

### **Time.Minute**

**Syntax**

```m
Time.Minute(time as time) as number
```

**Syntax + Placeholder**

```m
Time.Minute(#time(14, 30, 45))
```

**Example**

```m
Time.Minute(#time(18, 45, 00))
// Output: 45
```


***

### **Time.Second**

**Syntax**

```m
Time.Second(time as time) as number
```

**Syntax + Placeholder**

```m
Time.Second(#time(14, 30, 45))
```

**Example**

```m
Time.Second(#time(18, 45, 59))
// Output: 59
```


***

### **Time.From**

**Syntax**

```m
Time.From(value as any) as time
```

**Syntax + Placeholder**

```m
Time.From("14:30:00")
```

**Example**

```m
Time.From(#datetime(2023, 5, 10, 18, 30, 00))
// Output: 18:30:00
```


***

### **Time.FromText**

**Syntax**

```m
Time.FromText(text as text, optional culture as text) as time
```

**Syntax + Placeholder**

```m
Time.FromText("14:30:00", "en-US")
```

**Example**

```m
Time.FromText("18:45:30")
// Output: 18:45:30
```


***

### **Time.FromParts**

**Syntax**

```m
Time.FromParts(hour as number, minute as number, second as number, optional fraction as number) as time
```

**Syntax + Placeholder**

```m
Time.FromParts(14, 30, 45, 0)
```

**Example**

```m
Time.FromParts(18, 45, 59, 0)
// Output: 18:45:59
```


***

### **Time.ToText**

**Syntax**

```m
Time.ToText(time as time, optional format as any, optional culture as text) as text
```

**Syntax + Placeholder**

```m
Time.ToText(#time(14, 30, 00), "HH:mm")
```

**Example**

```m
Time.ToText(#time(18, 45, 59), "hh:mm tt")
// Output: "06:45 PM"
```


***
<section id="-datetime-functions"><h2>📂 DateTime Functions</h2></section>


***

### **DateTime.From**

**Syntax**

```m
DateTime.From(value as any) as datetime
```

**Syntax + Placeholder**

```m
DateTime.From("2025-08-20T14:30:00")
```

**Example**

```m
DateTime.From(#date(2025, 8, 20))
// Output: 2025-08-20 00:00:00
```


***

### **DateTime.FromText**

**Syntax**

```m
DateTime.FromText(text as text, optional culture as text) as datetime
```

**Syntax + Placeholder**

```m
DateTime.FromText("08/20/2025 14:30:00", "en-US")
```

**Example**

```m
DateTime.FromText("2023-05-10T18:45:00")
// Output: 2023-05-10 18:45:00
```


***

### **DateTime.ToText**

**Syntax**

```m
DateTime.ToText(datetime as datetime, optional format as any, optional culture as text) as text
```

**Syntax + Placeholder**

```m
DateTime.ToText(#datetime(2025, 8, 20, 14, 30, 0), "yyyy-MM-dd hh:mm tt")
```

**Example**

```m
DateTime.ToText(#datetime(2023, 5, 10, 18, 45, 0), "MM/dd/yyyy HH:mm")
// Output: "05/10/2023 18:45"
```


***

### **DateTime.LocalNow**

**Syntax**

```m
DateTime.LocalNow() as datetime
```

**Syntax + Placeholder**

```m
DateTime.LocalNow()
```

**Example**

```m
DateTime.LocalNow()
// Output: Current local datetime, e.g. 2025-08-20 02:07:00
```


***

### **DateTime.FixedLocalNow**

**Syntax**

```m
DateTime.FixedLocalNow() as datetime
```

**Syntax + Placeholder**

```m
DateTime.FixedLocalNow()
```

**Example**

```m
DateTime.FixedLocalNow()
// Output: Fixed local datetime value (does not change during evaluation)
```


***

### **DateTime.FromFileTimeUtc**

**Syntax**

```m
DateTime.FromFileTimeUtc(filetime as number) as datetime
```

**Syntax + Placeholder**

```m
DateTime.FromFileTimeUtc(132537600000000000)
```

**Example**

```m
DateTime.FromFileTimeUtc(129930000000000000)
// Converts Windows file time to datetime
```


***

### **DateTime.AddZone**

**Syntax**

```m
DateTime.AddZone(datetime as datetime, offset as number) as datetimezone
```

**Syntax + Placeholder**

```m
DateTime.AddZone(#datetime(2025,8,20,14,30,0), 5.5)
```

**Example**

```m
DateTime.AddZone(#datetime(2023,5,10,10,0,0), -5)
// Output: 2023-05-10 10:00:00 -05:00
```


***
### **DateTimeZone.From**

**Syntax**

```m
DateTimeZone.From(value as any) as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.From("2025-08-20T14:30:00+05:30")
```

**Example**

```m
DateTimeZone.From(#datetime(2023,5,10,14,30,0))
// Output: 2023-05-10 14:30:00 +00:00
```


***

### **DateTimeZone.FromFileTimeUtc**

**Syntax**

```m
DateTimeZone.FromFileTimeUtc(filetime as number) as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.FromFileTimeUtc(132537600000000000)
```

**Example**

```m
DateTimeZone.FromFileTimeUtc(129930000000000000)
// Converts Windows file time to datetimezone
```


***

### **DateTimeZone.SwitchZone**

**Syntax**

```m
DateTimeZone.SwitchZone(datetimezone as datetimezone, offset as number) as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.SwitchZone(#datetimezone(2025,8,20,14,30,0,0,0), 5.5)
```

**Example**

```m
DateTimeZone.SwitchZone(#datetimezone(2023,5,10,18,0,0,0,0), -4)
// Changes timezone offset to -4
```


***

### **DateTimeZone.ToLocal**

**Syntax**

```m
DateTimeZone.ToLocal(datetimezone as datetimezone) as datetime
```

**Syntax + Placeholder**

```m
DateTimeZone.ToLocal(DateTimeZone.UtcNow())
```

**Example**

```m
DateTimeZone.ToLocal(DateTimeZone.FixedUtcNow())
// Converts UTC time to system local time
```


***

### **DateTimeZone.RemoveZone**

**Syntax**

```m
DateTimeZone.RemoveZone(datetimezone as datetimezone) as datetime
```

**Syntax + Placeholder**

```m
DateTimeZone.RemoveZone(DateTimeZone.UtcNow())
```

**Example**

```m
DateTimeZone.RemoveZone(#datetimezone(2023,5,10,18,0,0,0,0))
// Output: 2023-05-10 18:00:00
```


***

### **DateTimeZone.UtcNow**

**Syntax**

```m
DateTimeZone.UtcNow() as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.UtcNow()
```

**Example**

```m
DateTimeZone.UtcNow()
// Output: Current UTC datetime
```


***

### **DateTimeZone.FixedUtcNow**

**Syntax**

```m
DateTimeZone.FixedUtcNow() as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.FixedUtcNow()
```

**Example**

```m
DateTimeZone.FixedUtcNow()
// Output: Fixed UTC time (does not change during evaluation)
```


***

### **DateTimeZone.LocalNow**

**Syntax**

```m
DateTimeZone.LocalNow() as datetimezone
```

**Syntax + Placeholder**

```m
DateTimeZone.LocalNow()
```

**Example**

```m
DateTimeZone.LocalNow()
// Output: Current local datetime with timezone
```


***
<section id="-duration-functions"><h2>📂 Duration Functions</h2></section>


***

### **Duration.From**

**Syntax**

```m
Duration.From(value as any) as duration
```

**Syntax + Placeholder**

```m
Duration.From("1.02:30:00") // 1 day, 2 hours, 30 mins
```

**Example**

```m
Duration.From(#datetime(2023,5,10,12,0,0) - #datetime(2023,5,9,10,0,0))
// Output: #duration(1,2,0,0)
```


***

### **Duration.FromText**

**Syntax**

```m
Duration.FromText(text as text) as duration
```

**Syntax + Placeholder**

```m
Duration.FromText("2.01:00:00")  // 2 days, 1 hour
```

**Example**

```m
Duration.FromText("0.12:30:15")
// Output: #duration(0,12,30,15)
```


***

### **Duration.ToText**

**Syntax**

```m
Duration.ToText(duration as duration) as text
```

**Syntax + Placeholder**

```m
Duration.ToText(#duration(1,2,30,0))
```

**Example**

```m
Duration.ToText(#duration(2,5,45,0))
// Output: "2.05:45:00"
```


***

### **Duration.Days**

**Syntax**

```m
Duration.Days(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.Days(#duration(5,12,0,0))
```

**Example**

```m
Duration.Days(#duration(3,0,0,0))
// Output: 3
```


***

### **Duration.Hours**

**Syntax**

```m
Duration.Hours(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.Hours(#duration(1,12,30,0))
```

**Example**

```m
Duration.Hours(#duration(0,5,45,0))
// Output: 5
```


***

### **Duration.Minutes**

**Syntax**

```m
Duration.Minutes(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.Minutes(#duration(0,1,30,0))
```

**Example**

```m
Duration.Minutes(#duration(0,0,45,0))
// Output: 45
```


***

### **Duration.Seconds**

**Syntax**

```m
Duration.Seconds(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.Seconds(#duration(0,0,1,30))
```

**Example**

```m
Duration.Seconds(#duration(0,0,0,59))
// Output: 59
```


***

### **Duration.TotalDays**

**Syntax**

```m
Duration.TotalDays(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.TotalDays(#duration(3,12,0,0))
```

**Example**

```m
Duration.TotalDays(#duration(1,12,0,0))
// Output: 1.5
```


***

### **Duration.TotalHours**

**Syntax**

```m
Duration.TotalHours(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.TotalHours(#duration(1,12,0,0))
```

**Example**

```m
Duration.TotalHours(#duration(2,0,0,0))
// Output: 48
```


***

### **Duration.TotalMinutes**

**Syntax**

```m
Duration.TotalMinutes(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.TotalMinutes(#duration(0,2,0,0))
```

**Example**

```m
Duration.TotalMinutes(#duration(1,1,0,0))
// Output: 1500
```


***

### **Duration.TotalSeconds**

**Syntax**

```m
Duration.TotalSeconds(duration as duration) as number
```

**Syntax + Placeholder**

```m
Duration.TotalSeconds(#duration(0,0,2,0))
```

**Example**

```m
Duration.TotalSeconds(#duration(0,1,0,0))
// Output: 3600
```


***
<section id="-logical--conditional-functions"><h2>📂 Logical &amp; Conditional Functions</h2></section>


***

### **if…then…else**

**Syntax**

```m
if condition then result else alternative
```

**Syntax + Placeholder**

```m
if [Score] >= 50 then "Pass" else "Fail"
```

**Example**

```m
if 5 > 3 then "Yes" else "No"
// Output: "Yes"
```


***

### **try…otherwise**

**Syntax**

```m
try expression otherwise fallback
```

**Syntax + Placeholder**

```m
try Number.FromText("abc") otherwise 0
```

**Example**

```m
try 10 / 0 otherwise "Error handled"
// Output: "Error handled"
```


***

### **and**

**Syntax**

```m
logical1 and logical2
```

**Syntax + Placeholder**

```m
([Age] > 18) and ([Score] >= 50)
```

**Example**

```m
(5 > 3) and (2 < 10)
// Output: true
```


***

### **or**

**Syntax**

```m
logical1 or logical2
```

**Syntax + Placeholder**

```m
([Status] = "Active") or ([Balance] > 0)
```

**Example**

```m
(5 > 10) or (2 < 10)
// Output: true
```


***

### **not**

**Syntax**

```m
not logical
```

**Syntax + Placeholder**

```m
not ([Age] > 20)
```

**Example**

```m
not (5 > 10)
// Output: true
```


***

### **Value.Equals**

**Syntax**

```m
Value.Equals(a as any, b as any, optional precision as any) as logical
```

**Syntax + Placeholder**

```m
Value.Equals(10, 10)
```

**Example**

```m
Value.Equals(3.14159, 3.14159)
// Output: true
```


***

### **Value.NullableEquals**

**Syntax**

```m
Value.NullableEquals(a as any, b as any) as logical
```

**Syntax + Placeholder**

```m
Value.NullableEquals(null, null)
```

**Example**

```m
Value.NullableEquals(null, 5)
// Output: false
```


***

### **Value.Compare**

**Syntax**

```m
Value.Compare(a as any, b as any, optional comparer as any) as number
```

**Syntax + Placeholder**

```m
Value.Compare(5, 10)
```

**Example**

```m
Value.Compare(10, 5)
// Output: 1 (greater than)
```


***

### **List.AnyTrue**

**Syntax**

```m
List.AnyTrue(list as list) as logical
```

**Syntax + Placeholder**

```m
List.AnyTrue({false, false, true})
```

**Example**

```m
List.AnyTrue({false, true})
// Output: true
```


***

### **List.AllTrue**

**Syntax**

```m
List.AllTrue(list as list) as logical
```

**Syntax + Placeholder**

```m
List.AllTrue({true, true, true})
```

**Example**

```m
List.AllTrue({true, false})
// Output: false
```


***

### **Record.HasFields**

**Syntax**

```m
Record.HasFields(record as record, fields as list) as logical
```

**Syntax + Placeholder**

```m
Record.HasFields([Name="John", Age=30], {"Age"})
```

**Example**

```m
Record.HasFields([A=1, B=2], {"A"})
// Output: true
```


***

### **Value.Is**

**Syntax**

```m
Value.Is(value as any, type as type) as logical
```

**Syntax + Placeholder**

```m
Value.Is(123, type number)
```

**Example**

```m
Value.Is("Hello", type text)
// Output: true
```


***

### **Value.Type**

**Syntax**

```m
Value.Type(value as any) as type
```

**Syntax + Placeholder**

```m
Value.Type("Hello")
```

**Example**

```m
Value.Type(123)
// Output: type number
```


***

### **Error.Record**

**Syntax**

```m
Error.Record(reason as text, message as text, detail as any) as record
```

**Syntax + Placeholder**

```m
Error.Record("Invalid Input", "Value should be positive", 123)
```

**Example**

```m
Error.Record("DataError", "Invalid Data Found", [Row=5])
// Creates a custom error record
```


***

### **Error.Raise**

**Syntax**

```m
Error.Raise(reason as text, message as text, optional detail as any) as none
```

**Syntax + Placeholder**

```m
Error.Raise("ValidationError", "Age cannot be negative")
```

**Example**

```m
Error.Raise("CustomError", "Manual error raised")
// Raises an error with message
```


***

### **Diagnostics.Trace**

**Syntax**

```m
Diagnostics.Trace(level as number, message as text, details as any) as any
```

**Syntax + Placeholder**

```m
Diagnostics.Trace(1, "Process started", [])
```

**Example**

```m
Diagnostics.Trace(2, "Debug Info", [Step="Load Data"])
// Returns data with trace message
```


***

### **Diagnostics.ActivityId**

**Syntax**

```m
Diagnostics.ActivityId() as text
```

**Syntax + Placeholder**

```m
Diagnostics.ActivityId()
```

**Example**

```m
Diagnostics.ActivityId()
// Output: A unique trace activity ID string
```


***
<section id="-data-type--type-system-functions"><h2>📂 Data Type &amp; Type System Functions</h2></section>


***

### **Value.Type**

**Syntax**

```m
Value.Type(value as any) as type
```

**Syntax + Placeholder**

```m
Value.Type("Hello")
```

**Example**

```m
Value.Type(123)
// Output: type number
```


***

### **Value.ReplaceType**

**Syntax**

```m
Value.ReplaceType(value as any, type as type) as any
```

**Syntax + Placeholder**

```m
Value.ReplaceType(123, type text)
```

**Example**

```m
Value.ReplaceType("Hello", type number)
// Forces value to be treated as a number type
```


***

### **Value.As**

**Syntax**

```m
Value.As(value as any, type as type) as any
```

**Syntax + Placeholder**

```m
Value.As("123", type number)
```

**Example**

```m
Value.As(123, type number)
// Output: 123
```


***

### **Value.Is**

**Syntax**

```m
Value.Is(value as any, type as type) as logical
```

**Syntax + Placeholder**

```m
Value.Is(123, type number)
```

**Example**

```m
Value.Is("PowerQuery", type text)
// Output: true
```


***

### **Type.Is**

**Syntax**

```m
Type.Is(type1 as type, type2 as type) as logical
```

**Syntax + Placeholder**

```m
Type.Is(type number, type any)
```

**Example**

```m
Type.Is(type text, type any)
// Output: true
```


***

### **Type.Equals**

**Syntax**

```m
Type.Equals(type1 as type, type2 as type) as logical
```

**Syntax + Placeholder**

```m
Type.Equals(type number, Int64.Type)
```

**Example**

```m
Type.Equals(type text, type text)
// Output: true
```


***

### **Type.ForRecord**

**Syntax**

```m
Type.ForRecord(fields as record, open as logical) as type
```

**Syntax + Placeholder**

```m
Type.ForRecord([Name = type text, Age = type number], false)
```

**Example**

```m
Type.ForRecord([ID = type number, Value = type text], true)
// Returns a record type definition
```


***

### **Type.ForTable**

**Syntax**

```m
Type.ForTable(columns as type, open as logical) as type
```

**Syntax + Placeholder**

```m
Type.ForTable(type table [ID = Int64.Type, Name = type text], true)
```

**Example**

```m
Type.ForTable(type table [ProductID=Int64.Type, Price=type number], false)
// Defines a table type
```


***

### **Type.TableRow**

**Syntax**

```m
Type.TableRow(tableType as type) as type
```

**Syntax + Placeholder**

```m
Type.TableRow(type table [ID=Int64.Type, Name=type text])
```

**Example**

```m
Type.TableRow(type table [Product=text, Price=number])
// Output: type [Product=text, Price=number]
```


***

### **Type.FunctionReturn**

**Syntax**

```m
Type.FunctionReturn(functionType as type) as type
```

**Syntax + Placeholder**

```m
Type.FunctionReturn(type function(number) as text)
```

**Example**

```m
Type.FunctionReturn(type function(text) as number)
// Output: type number
```


***

### **Type.ListItem**

**Syntax**

```m
Type.ListItem(listType as type) as type
```

**Syntax + Placeholder**

```m
Type.ListItem(type list)
```

**Example**

```m
Type.ListItem(type list number)
// Output: type number
```


***

### **Type.Nullable**

**Syntax**

```m
Type.Nullable(type as type) as type
```

**Syntax + Placeholder**

```m
Type.Nullable(type number)
```

**Example**

```m
Type.Nullable(type text)
// Allows null values
```


***

### **Type.NonNullable**

**Syntax**

```m
Type.NonNullable(type as type) as type
```

**Syntax + Placeholder**

```m
Type.NonNullable(type nullable number)
```

**Example**

```m
Type.NonNullable(type nullable text)
// Output: type text (disallows nulls)
```


***

### **Type.Any**

**Syntax**

```m
type any
```

**Example**

```m
Value.Is(123, type any)
// Output: true
```


***

### **Type.None**

**Syntax**

```m
type none
```

**Example**

```m
Value.Is(123, type none)
// Output: false
```


***

### **Type.Number**

**Syntax**

```m
type number
```

**Example**

```m
Value.Is(3.14, type number)
// Output: true
```


***

### **Type.Text**

**Syntax**

```m
type text
```

**Example**

```m
Value.Is("abc", type text)
// Output: true
```


***

### **Type.Logical**

**Syntax**

```m
type logical
```

**Example**

```m
Value.Is(true, type logical)
// Output: true
```


***

### **Type.Date**

**Syntax**

```m
type date
```

**Example**

```m
Value.Is(#date(2023,5,10), type date)
// Output: true
```


***

### **Type.Time**

**Syntax**

```m
type time
```

**Example**

```m
Value.Is(#time(12,30,0), type time)
// Output: true
```


***

### **Type.DateTime**

**Syntax**

```m
type datetime
```

**Example**

```m
Value.Is(#datetime(2023,5,10,12,0,0), type datetime)
// Output: true
```


***

### **Type.DateTimeZone**

**Syntax**

```m
type datetimezone
```

**Example**

```m
Value.Is(DateTimeZone.UtcNow(), type datetimezone)
// Output: true
```


***

### **Type.Duration**

**Syntax**

```m
type duration
```

**Example**

```m
Value.Is(#duration(1,2,0,0), type duration)
// Output: true
```


***

### **Type.Function**

**Syntax**

```m
type function
```

**Example**

```m
Value.Is((x)=> x + 1, type function)
// Output: true
```


***

### **Type.List**

**Syntax**

```m
type list
```

**Example**

```m
Value.Is({1,2,3}, type list)
// Output: true
```


***

### **Type.Record**

**Syntax**

```m
type record
```

**Example**

```m
Value.Is([Name="John"], type record)
// Output: true
```


***

### **Type.Table**

**Syntax**

```m
type table
```

**Example**

```m
Value.Is(#table({"Col1"}, {{1},{2}}), type table)
// Output: true
```


***

### **Type.Binary**

**Syntax**

```m
type binary
```

**Example**

```m
Value.Is(Text.ToBinary("Hello"), type binary)
// Output: true
```


***
<section id="-list-functions"><h2>📂 List Functions</h2></section>
***
### **List.Transform**

**Syntax**

```m
List.Transform(list as list, transform as function) as list
```

**Syntax + Placeholder**

```m
List.Transform({1,2,3}, each _ * 2)
```

**Example**

```m
List.Transform({1,2,3}, each _ + 1)
// Output: {2,3,4}
```


***

### **List.Select**

**Syntax**

```m
List.Select(list as list, predicate as function) as list
```

**Syntax + Placeholder**

```m
List.Select({1,2,3,4}, each _ > 2)
```

**Example**

```m
List.Select({10,15,20}, each _ >= 15)
// Output: {15,20}
```


***

### **List.RemoveItems**

**Syntax**

```m
List.RemoveItems(list as list, items as list) as list
```

**Syntax + Placeholder**

```m
List.RemoveItems({1,2,3,4}, {2,4})
```

**Example**

```m
List.RemoveItems({"A","B","C"}, {"B"})
// Output: {"A","C"}
```


***

### **List.RemoveMatchingItems**

**Syntax**

```m
List.RemoveMatchingItems(list as list, items as list) as list
```

**Syntax + Placeholder**

```m
List.RemoveMatchingItems({1,2,2,3}, {2})
```

**Example**

```m
List.RemoveMatchingItems({"X","X","Y"}, {"X"})
// Output: {"Y"}
```


***

### **List.Sort**

**Syntax**

```m
List.Sort(list as list, optional comparer as any) as list
```

**Syntax + Placeholder**

```m
List.Sort({3,1,2})
```

**Example**

```m
List.Sort({"banana","apple","carrot"})
// Output: {"apple","banana","carrot"}
```


***

### **List.Distinct**

**Syntax**

```m
List.Distinct(list as list, optional comparer as any) as list
```

**Syntax + Placeholder**

```m
List.Distinct({1,2,2,3})
```

**Example**

```m
List.Distinct({"A","A","B"})
// Output: {"A","B"}
```


***

### **List.Buffer**

**Syntax**

```m
List.Buffer(list as list) as list
```

**Syntax + Placeholder**

```m
List.Buffer(SourceList)
```

**Example**

```m
List.Buffer({1..100})
// Buffers list in memory
```


***

### **List.Count**

**Syntax**

```m
List.Count(list as list) as number
```

**Syntax + Placeholder**

```m
List.Count({1,2,3})
```

**Example**

```m
List.Count({"A","B","C"})
// Output: 3
```


***

### **List.Sum**

**Syntax**

```m
List.Sum(list as list) as any
```

**Syntax + Placeholder**

```m
List.Sum({1,2,3,4})
```

**Example**

```m
List.Sum({10,20,30})
// Output: 60
```


***

### **List.Average**

**Syntax**

```m
List.Average(list as list) as any
```

**Syntax + Placeholder**

```m
List.Average({5,10,15})
```

**Example**

```m
List.Average({10,20,30})
// Output: 20
```


***

### **List.Max**

**Syntax**

```m
List.Max(list as list) as any
```

**Syntax + Placeholder**

```m
List.Max({1,5,3})
```

**Example**

```m
List.Max({100,200,150})
// Output: 200
```


***

### **List.Min**

**Syntax**

```m
List.Min(list as list) as any
```

**Syntax + Placeholder**

```m
List.Min({1,5,3})
```

**Example**

```m
List.Min({100,200,150})
// Output: 100
```


***

### **List.Product**

**Syntax**

```m
List.Product(list as list) as any
```

**Syntax + Placeholder**

```m
List.Product({2,3,4})
```

**Example**

```m
List.Product({1,5,10})
// Output: 50
```


***

### **List.Accumulate**

**Syntax**

```m
List.Accumulate(list as list, seed as any, accumulator as function) as any
```

**Syntax + Placeholder**

```m
List.Accumulate({1,2,3}, 0, (state, current) => state + current)
```

**Example**

```m
List.Accumulate({1,2,3,4}, 1, (s,c) => s * c)
// Output: 24
```


***

### **List.Generate**

**Syntax**

```m
List.Generate(initial as function, condition as function, next as function, optional selector as function) as list
```

**Syntax + Placeholder**

```m
List.Generate(()=>0, each _ < 5, each _ + 1)
```

**Example**

```m
List.Generate(()=>1, each _ <= 5, each _ + 1)
// Output: {1,2,3,4,5}
```


***

### **List.Zip**

**Syntax**

```m
List.Zip(lists as list) as list
```

**Syntax + Placeholder**

```m
List.Zip({{1,2,3},{"A","B","C"}})
```

**Example**

```m
List.Zip({{1,2},{"X","Y"}})
// Output: {{1,"X"},{2,"Y"}}
```


***

### **List.Combine**

**Syntax**

```m
List.Combine(lists as list) as list
```

**Syntax + Placeholder**

```m
List.Combine({{1,2},{3,4}})
```

**Example**

```m
List.Combine({{"A","B"},{"C","D"}})
// Output: {"A","B","C","D"}
```


***

### **List.Split**

**Syntax**

```m
List.Split(list as list, size as number) as list
```

**Syntax + Placeholder**

```m
List.Split({1,2,3,4,5}, 2)
```

**Example**

```m
List.Split({10,20,30,40}, 2)
// Output: {{10,20},{30,40}}
```


***

### **List.Contains**

**Syntax**

```m
List.Contains(list as list, value as any, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
List.Contains({1,2,3}, 2)
```

**Example**

```m
List.Contains({"A","B","C"}, "B")
// Output: true
```


***
### **List.ContainsAll**

**Syntax**

```m
List.ContainsAll(list as list, values as list, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
List.ContainsAll({1,2,3,4}, {2,3})
```

**Example**

```m
List.ContainsAll({"A","B","C"}, {"A","C"})
// Output: true
```


***

### **List.ContainsAny**

**Syntax**

```m
List.ContainsAny(list as list, values as list, optional comparer as any) as logical
```

**Syntax + Placeholder**

```m
List.ContainsAny({1,2,3}, {5,2})
```

**Example**

```m
List.ContainsAny({"X","Y","Z"}, {"A","Z"})
// Output: true
```


***

### **List.PositionOf**

**Syntax**

```m
List.PositionOf(list as list, value as any, optional occurrence as any, optional comparer as any) as any
```

**Syntax + Placeholder**

```m
List.PositionOf({"A","B","C"}, "B")
```

**Example**

```m
List.PositionOf({10,20,30}, 30)
// Output: 2
```


***

### **List.PositionOfAny**

**Syntax**

```m
List.PositionOfAny(list as list, values as list, optional occurrence as any, optional comparer as any) as any
```

**Syntax + Placeholder**

```m
List.PositionOfAny({"A","B","C"}, {"X","B"})
```

**Example**

```m
List.PositionOfAny({1,2,3,4}, {3,5})
// Output: 2
```


***

### **List.First**

**Syntax**

```m
List.First(list as list, optional default as any) as any
```

**Syntax + Placeholder**

```m
List.First({1,2,3})
```

**Example**

```m
List.First({"A","B","C"})
// Output: "A"
```


***

### **List.FirstN**

**Syntax**

```m
List.FirstN(list as list, count as any) as list
```

**Syntax + Placeholder**

```m
List.FirstN({1,2,3,4}, 2)
```

**Example**

```m
List.FirstN({"X","Y","Z"}, 2)
// Output: {"X","Y"}
```


***

### **List.Last**

**Syntax**

```m
List.Last(list as list, optional default as any) as any
```

**Syntax + Placeholder**

```m
List.Last({1,2,3})
```

**Example**

```m
List.Last({"A","B","C"})
// Output: "C"
```


***

### **List.LastN**

**Syntax**

```m
List.LastN(list as list, count as any) as list
```

**Syntax + Placeholder**

```m
List.LastN({1,2,3,4}, 2)
```

**Example**

```m
List.LastN({"A","B","C","D"}, 2)
// Output: {"C","D"}
```


***

### **List.Skip**

**Syntax**

```m
List.Skip(list as list, count as any) as list
```

**Syntax + Placeholder**

```m
List.Skip({1,2,3,4}, 2)
```

**Example**

```m
List.Skip({"A","B","C"}, 1)
// Output: {"B","C"}
```


***

### **List.Take**

**Syntax**

```m
List.Take(list as list, count as any) as list
```

**Syntax + Placeholder**

```m
List.Take({1,2,3,4}, 2)
```

**Example**

```m
List.Take({"X","Y","Z"}, 1)
// Output: {"X"}
```


***

### **List.Range**

**Syntax**

```m
List.Range(list as list, offset as number, optional count as number) as list
```

**Syntax + Placeholder**

```m
List.Range({1,2,3,4,5}, 2, 2)
```

**Example**

```m
List.Range({"A","B","C","D"}, 1, 2)
// Output: {"B","C"}
```


***

### **List.Repeat**

**Syntax**

```m
List.Repeat(value as any, count as number) as list
```

**Syntax + Placeholder**

```m
List.Repeat("X", 3)
```

**Example**

```m
List.Repeat(5, 4)
// Output: {5,5,5,5}
```


***

### **List.Reverse**

**Syntax**

```m
List.Reverse(list as list) as list
```

**Syntax + Placeholder**

```m
List.Reverse({1,2,3})
```

**Example**

```m
List.Reverse({"A","B","C"})
// Output: {"C","B","A"}
```


***

### **List.RemoveNulls**

**Syntax**

```m
List.RemoveNulls(list as list) as list
```

**Syntax + Placeholder**

```m
List.RemoveNulls({1,null,3})
```

**Example**

```m
List.RemoveNulls({"A", null, "B"})
// Output: {"A","B"}
```


***

### **List.Alternate**

**Syntax**

```m
List.Alternate(list as list, skip as number, take as number, optional offset as number) as list
```

**Syntax + Placeholder**

```m
List.Alternate({1,2,3,4,5,6}, 1, 2)
```

**Example**

```m
List.Alternate({"A","B","C","D","E","F"}, 1, 2)
// Output: {"B","C","E","F"}
```


***

### **List.Difference**

**Syntax**

```m
List.Difference(list1 as list, list2 as list, optional equationCriteria as any) as list
```

**Syntax + Placeholder**

```m
List.Difference({1,2,3}, {2,4})
```

**Example**

```m
List.Difference({"A","B","C"}, {"B"})
// Output: {"A","C"}
```


***

### **List.Intersect**

**Syntax**

```m
List.Intersect(lists as list, optional equationCriteria as any) as list
```

**Syntax + Placeholder**

```m
List.Intersect({{1,2,3},{2,3,4}})
```

**Example**

```m
List.Intersect({{"A","B"},{"B","C"}})
// Output: {"B"}
```


***

### **List.Union**

**Syntax**

```m
List.Union(lists as list, optional equationCriteria as any) as list
```

**Syntax + Placeholder**

```m
List.Union({{1,2},{2,3}})
```

**Example**

```m
List.Union({{"A","B"},{"B","C"}})
// Output: {"A","B","C"}
```


***

### **List.MatchesAll**

**Syntax**

```m
List.MatchesAll(list as list, predicate as function) as logical
```

**Syntax + Placeholder**

```m
List.MatchesAll({2,4,6}, each _ mod 2 = 0)
```

**Example**

```m
List.MatchesAll({10,20,30}, each _ > 5)
// Output: true
```


***

### **List.MatchesAny**

**Syntax**

```m
List.MatchesAny(list as list, predicate as function) as logical
```

**Syntax + Placeholder**

```m
List.MatchesAny({1,3,5}, each _ = 3)
```

**Example**

```m
List.MatchesAny({"A","B","C"}, each _ = "B")
// Output: true
```


***

### **List.FindText**

**Syntax**

```m
List.FindText(list as list, text as text) as list
```

**Syntax + Placeholder**

```m
List.FindText({"apple","banana","pear"}, "an")
```

**Example**

```m
List.FindText({"Power Query","Excel","M"}, "er")
// Output: {"Power Query"}
```


***

### **List.Median**

**Syntax**

```m
List.Median(list as list) as any
```

**Syntax + Placeholder**

```m
List.Median({1,2,3,4,5})
```

**Example**

```m
List.Median({10,20,30})
// Output: 20
```


***

### **List.Mode**

**Syntax**

```m
List.Mode(list as list) as any
```

**Syntax + Placeholder**

```m
List.Mode({1,2,2,3})
```

**Example**

```m
List.Mode({"A","B","A","C"})
// Output: "A"
```


***

### **List.Percentile**

**Syntax**

```m
List.Percentile(list as list, percentile as number) as any
```

**Syntax + Placeholder**

```m
List.Percentile({1,2,3,4,5}, 0.5)
```

**Example**

```m
List.Percentile({10,20,30,40}, 0.75)
// Output: 30
```


***

### **List.Variance**

**Syntax**

```m
List.Variance(list as list) as any
```

**Syntax + Placeholder**

```m
List.Variance({1,2,3,4,5})
```

**Example**

```m
List.Variance({10,20,30})
// Output: 100
```


***

### **List.VarianceN**

**Syntax**

```m
List.VarianceN(list as list) as any
```

**Syntax + Placeholder**

```m
List.VarianceN({1,2,3,4,5})
```

**Example**

```m
List.VarianceN({10,20,30})
// Output: 66.67
```


***

### **List.StandardDeviation**

**Syntax**

```m
List.StandardDeviation(list as list) as any
```

**Syntax + Placeholder**

```m
List.StandardDeviation({1,2,3,4,5})
```

**Example**

```m
List.StandardDeviation({10,20,30})
// Output: 10
```


***

### **List.StandardDeviationN**

**Syntax**

```m
List.StandardDeviationN(list as list) as any
```

**Syntax + Placeholder**

```m
List.StandardDeviationN({1,2,3,4,5})
```

**Example**

```m
List.StandardDeviationN({10,20,30})
// Output: 8.165
```


***

### **List.Covariance**

**Syntax**

```m
List.Covariance(list1 as list, list2 as list) as any
```

**Syntax + Placeholder**

```m
List.Covariance({1,2,3}, {4,5,6})
```

**Example**

```m
List.Covariance({10,20,30}, {15,25,35})
// Output: 50
```


***

### **List.Numbers**

**Syntax**

```m
List.Numbers(start as number, count as number, optional step as number) as list
```

**Syntax + Placeholder**

```m
List.Numbers(1, 5, 1)
```

**Example**

```m
List.Numbers(0,5)
// Output: {0,1,2,3,4}
```


***

### **List.RepeatEach**

**Syntax**

```m
List.RepeatEach(list as list, count as number) as list
```

**Syntax + Placeholder**

```m
List.RepeatEach({1,2}, 3)
```

**Example**

```m
List.RepeatEach({"A","B"}, 2)
// Output: {"A","A","B","B"}
```


***

### **List.TransformMany**

**Syntax**

```m
List.TransformMany(list as list, transform as function, resultSelector as function) as list
```

**Syntax + Placeholder**

```m
List.TransformMany({1,2}, each {_, _*2}, (x,y)=> [x=x, y=y])
```

**Example**

```m
List.TransformMany({1,2}, each {_,_+10}, (x,y)=> [Input=x, Output=y])
// Output: {[Input=1,Output=1],[Input=1,Output=11],[Input=2,Output=2],[Input=2,Output=12]}
```


***

### **List.NonNullCount**

**Syntax**

```m
List.NonNullCount(list as list) as number
```

**Syntax + Placeholder**

```m
List.NonNullCount({1,null,3,null,5})
```

**Example**

```m
List.NonNullCount({"A",null,"B"})
// Output: 2
```
***
### **List.AnyTrue**

**Syntax**

```m
List.AnyTrue(list as list) as logical
```

**Syntax + Placeholder**

```m
List.AnyTrue({true, false, false})
```

**Example**

```m
List.AnyTrue({false, false, true})
// Output: true
```


***
<section id="-record-functions"><h2>📂 Record Functions</h2></section>


***

### **Record.Field**

**Syntax**

```m
Record.Field(record as record, field as text) as any
```

**Syntax + Placeholder**

```m
Record.Field([Field1 = Value1, Field2 = Value2], "Field1")
```

**Example**

```m
Record.Field([Name = "John", Age = 30], "Age")
// Output: 30
```


***

### **Record.FieldOrDefault**

**Syntax**

```m
Record.FieldOrDefault(record as record, field as text, default as any) as any
```

**Syntax + Placeholder**

```m
Record.FieldOrDefault([Field1 = Value1], "FieldX", "DefaultValue")
```

**Example**

```m
Record.FieldOrDefault([Name = "Maria"], "Age", 25)
// Output: 25
```


***

### **Record.FieldNames**

**Syntax**

```m
Record.FieldNames(record as record) as list
```

**Syntax + Placeholder**

```m
Record.FieldNames([Field1 = Value1, Field2 = Value2])
```

**Example**

```m
Record.FieldNames([Name = "Alex", Salary = 50000])
// Output: {"Name","Salary"}
```


***

### **Record.FieldValues**

**Syntax**

```m
Record.FieldValues(record as record) as list
```

**Syntax + Placeholder**

```m
Record.FieldValues([Field1 = Value1, Field2 = Value2])
```

**Example**

```m
Record.FieldValues([Name = "Sara", Age = 28])
// Output: {"Sara",28}
```


***

### **Record.AddField**

**Syntax**

```m
Record.AddField(record as record, field as text, value as any) as record
```

**Syntax + Placeholder**

```m
Record.AddField([Field1 = Value1], "NewField", "NewValue")
```

**Example**

```m
Record.AddField([Name = "Emma"], "City", "London")
// Output: [Name="Emma", City="London"]
```


***

### **Record.RemoveField**

**Syntax**

```m
Record.RemoveField(record as record, field as text) as record
```

**Syntax + Placeholder**

```m
Record.RemoveField([Field1 = Value1, Field2 = Value2], "Field2")
```

**Example**

```m
Record.RemoveField([Name="John", Age=30], "Age")
// Output: [Name="John"]
```


***

### **Record.RemoveFields**

**Syntax**

```m
Record.RemoveFields(record as record, fields as list) as record
```

**Syntax + Placeholder**

```m
Record.RemoveFields([Field1 = Value1, Field2 = Value2, Field3 = Value3], {"Field2","Field3"})
```

**Example**

```m
Record.RemoveFields([Name="Jack", Age=32, City="NY"], {"Age","City"})
// Output: [Name="Jack"]
```


***

### **Record.RenameFields**

**Syntax**

```m
Record.RenameFields(record as record, renames as list, optional missingField as any) as record
```

**Syntax + Placeholder**

```m
Record.RenameFields([Field1 = Value1], {{"Field1","NewField"}}, MissingField.Ignore)
```

**Example**

```m
Record.RenameFields([FirstName="Tom", Age=40], {{"FirstName","Name"}})
// Output: [Name="Tom", Age=40]
```


***

### **Record.SelectFields**

**Syntax**

```m
Record.SelectFields(record as record, fields as list, optional missingField as any) as record
```

**Syntax + Placeholder**

```m
Record.SelectFields([Field1=Value1, Field2=Value2], {"Field1"})
```

**Example**

```m
Record.SelectFields([Name="Liam", Age=29, Country="UK"], {"Name","Country"})
// Output: [Name="Liam", Country="UK"]
```


***

### **Record.TransformFields**

**Syntax**

```m
Record.TransformFields(record as record, transformations as list, optional missingField as any) as record
```

**Syntax + Placeholder**

```m
Record.TransformFields([Field1=Value1], {{"Field1", each _ + 10}})
```

**Example**

```m
Record.TransformFields([Name="Anna", Age=25], {{"Age", each _ + 5}})
// Output: [Name="Anna", Age=30]
```


***

### **Record.ToTable**

**Syntax**

```m
Record.ToTable(record as record) as table
```

**Syntax + Placeholder**

```m
Record.ToTable([Field1=Value1, Field2=Value2])
```

**Example**

```m
Record.ToTable([Name="Paul", Score=85])
/*
Output:
Name      Value
"Name"    "Paul"
"Score"   85
*/
```


***

### **Record.FromTable**

**Syntax**

```m
Record.FromTable(table as table) as record
```

**Syntax + Placeholder**

```m
Record.FromTable(Table.FromRows({{"Name","Paul"},{"Age",30}}, {"Name","Value"}))
```

**Example**

```m
Record.FromTable(
    #table({"Name","Value"}, {{"City","Paris"},{"Country","France"}})
)
// Output: [City="Paris", Country="France"]
```


***

### **Record.FromList**

**Syntax**

```m
Record.FromList(list as list, fields as list, optional missingField as any) as record
```

**Syntax + Placeholder**

```m
Record.FromList({"A","B"}, {"Field1","Field2"})
```

**Example**

```m
Record.FromList({"Tom",30}, {"Name","Age"})
// Output: [Name="Tom", Age=30]
```


***

### **Record.HasFields**

**Syntax**

```m
Record.HasFields(record as record, fields as list) as logical
```

**Syntax + Placeholder**

```m
Record.HasFields([Field1=Value1, Field2=Value2], {"Field1","Field2"})
```

**Example**

```m
Record.HasFields([Name="Eve", Age=27], {"Name","Age"})
// Output: true
```


***

### **Record.Combine**

**Syntax**

```m
Record.Combine(records as list) as record
```

**Syntax + Placeholder**

```m
Record.Combine({[Field1=Value1], [Field2=Value2]})
```

**Example**

```m
Record.Combine({[Name="Leo"], [Age=31, Country="CA"]})
// Output: [Name="Leo", Age=31, Country="CA"]
```


***

### **Record.ReorderFields**

**Syntax**

```m
Record.ReorderFields(record as record, fieldOrder as list) as record
```

**Syntax + Placeholder**

```m
Record.ReorderFields([Field1=Value1, Field2=Value2, Field3=Value3], {"Field3","Field1","Field2"})
```

**Example**

```m
Record.ReorderFields([Name="Sophia", Age=22, City="LA"], {"City","Name","Age"})
// Output: [City="LA", Name="Sophia", Age=22]
```


***

### **Record.ToList**

**Syntax**

```m
Record.ToList(record as record) as list
```

**Syntax + Placeholder**

```m
Record.ToList([Field1=Value1, Field2=Value2])
```

**Example**

```m
Record.ToList([Name="Victor", Score=90])
// Output: {"Victor",90}
```


***

### **Record.Contains**

**Syntax**

```m
Record.Contains(record as record, fields as list) as logical
```

**Syntax + Placeholder**

```m
Record.Contains([Field1=Value1, Field2=Value2], {"Field1"})
```

**Example**

```m
Record.Contains([Name="Olivia", Age=26], {"Age"})
// Output: true
```


***
<section id="-function--parameter-handling"><h2>📂 Function &amp; Parameter Handling</h2></section>


***

### **let … in**

**Syntax**

```m
let variable = expression in variable
```

**Syntax + Placeholder**

```m
let x = 10, y = 20 in x + y
```

**Example**

```m
let  
    a = 5,  
    b = 15  
in  
    a * b  
// Output: 75
```


***

### **Anonymous Function**

**Syntax**

```m
(x) => expression
```

**Syntax + Placeholder**

```m
(x) => x * 2
```

**Example**

```m
(x) => x + 5
// if applied to 7 → returns 12
```


***

### **each**

**Syntax**

```m
each expression
```

**Syntax + Placeholder**

```m
each _ * 2
```

**Example**

```m
List.Transform({1,2,3}, each _ * 3)
// Output: {3,6,9}
```


***

### **Function.Invoke**

**Syntax**

```m
Function.Invoke(function as function, arguments as list) as any
```

**Syntax + Placeholder**

```m
Function.Invoke(MyFunction, {arg1, arg2})
```

**Example**

```m
MySum = (a,b) => a + b,  
Function.Invoke(MySum, {10, 20})  
// Output: 30
```


***

### **Function.InvokeAfter**

**Syntax**

```m
Function.InvokeAfter(function as function, delay as duration) as function
```

**Syntax + Placeholder**

```m
Function.InvokeAfter(MyFunction, #duration(0,0,0,5))
```

**Example**

```m
Function.InvokeAfter(() => "Done", #duration(0,0,0,2))
// Executes after a 2-second delay
```


***

### **Function.InvokeWithErrorContext**

**Syntax**

```m
Function.InvokeWithErrorContext(function as function, context as record) as any
```

**Syntax + Placeholder**

```m
Function.InvokeWithErrorContext(MyFunction, [Context="Test"])
```

**Example**

```m
Function.InvokeWithErrorContext((x)=> x*10, [Info="My Run"])(5)
// Output 50 (with error context tracking in engine)
```


***

### **Function.From**

**Syntax**

```m
Function.From(functionType as type, handler as function, optional options as record) as function
```

**Syntax + Placeholder**

```m
Function.From(type function (x as number) as number, each _ * 2)
```

**Example**

```m
DoubleIt = Function.From(type function(x as number) as number, each _ * 2)  
DoubleIt(6)  
// Output: 12
```


***

### **Function.IsDataSource**

**Syntax**

```m
Function.IsDataSource(function as function) as logical
```

**Syntax + Placeholder**

```m
Function.IsDataSource(MyFunction)
```

**Example**

```m
Function.IsDataSource(Web.Contents)
// Output: true
```


***

### **Function.Type**

**Syntax**

```m
Function.Type(function as function) as type
```

**Syntax + Placeholder**

```m
Function.Type((x as number) => x * 2)
```

**Example**

```m
Function.Type((x as text) => Text.Upper(x))
// Output: type function (x as text) as text
```


***

### **parameter = value**

**Syntax**

```m
parameter = value
```

**Syntax + Placeholder**

```m
MyParam = 10
```

**Example**

```m
let threshold = 100 in threshold * 2  
// Output: 200
```


***

***
<section id="-expression-advanced--metadata-functions"><h2>📂 Expression, Advanced &amp; Metadata Functions</h2></section>


***

### **Expression.Evaluate**

**Syntax**

```m
Expression.Evaluate(text as text, optional environment as record) as any
```

**Syntax + Placeholder**

```m
Expression.Evaluate("1+2")
```

**Example**

```m
Expression.Evaluate("3*5")
// Output: 15
```


***

### **Expression.Constant**

**Syntax**

```m
Expression.Constant(value as any) as any
```

**Syntax + Placeholder**

```m
Expression.Constant(123)
```

**Example**

```m
Expression.Constant("Hello")
// Output: "Hello"
```


***

### **Expression.Identifier**

**Syntax**

```m
Expression.Identifier(name as text) as any
```

**Syntax + Placeholder**

```m
Expression.Identifier("MyVariable")
```

**Example**

```m
let MyVar = 99 in Expression.Identifier("MyVar")
// Output: MyVar reference (not value)
```


***

### Section.Section

**Syntax**
```m
Section.Section(name as text) as section
```
**Syntax + Placeholder**
```m
Section.Section("MySection")
```
**Example**
```m
Section.Section("MySection")


```

### Section.Members

**Syntax**
```m
Section.Members(section as section) as record
```
**Syntax + Placeholder**
```m
Section.Members(\#sections[MySection])
```
**Example**
```m
Section.Members(\#sections[MySection])


```

### sections

**Syntax + Example**
```m
\#sections


```

### shared

**Syntax + Example**
```m
\#shared


```

### Value.Metadata

**Syntax**
```m
Value.Metadata(value as any) as record
```
**Syntax + Placeholder**
```m
Value.Metadata("X")
```
**Example**
```m
Value.Metadata(123)


```

### Value.AddMetadata

**Syntax**
```m
Value.AddMetadata(value as any, metadata as record) as any
```
**Syntax + Placeholder**
```m
Value.AddMetadata("X", [Source="User"])
```
**Example**
```m
Value.AddMetadata(100, [Source="User"])


```

### Table.View

**Syntax**
```m
Table.View(name as text, handlers as record) as table
```
**Syntax + Placeholder**
```m
Table.View("MyView", [GetType=()=> type table [A=number], GetRows=()=> {{1},{2}}])
```
**Example**
```m
Table.View("MyView", [GetType=()=> type table [A=number], GetRows=()=> {{1},{2}}])


```

### Binary.Compress

**Syntax**
```m
Binary.Compress(binary as binary, compressionType as number) as binary
```
**Syntax + Placeholder**
```m
Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate)
```
**Example**
```m
Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate)


```

### Binary.Decompress

**Syntax**
```m
Binary.Decompress(binary as binary, compressionType as number) as binary
```
**Syntax + Placeholder**
```m
Binary.Decompress(Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate), Compression.Deflate)
```
**Example**
```m
Binary.Decompress(Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate), Compression.Deflate)


```

### Diagnostics.Trace

**Syntax**
```m
Diagnostics.Trace(level as number, message as text, details as any) as any
```
**Syntax + Placeholder**
```m
Diagnostics.Trace(1, "Step running", [Detail="Info"])
```
**Example**
```m
Diagnostics.Trace(1, "Step running", [Detail="Log Info"])


```

### Diagnostics.ActivityId

**Syntax**
```m
Diagnostics.ActivityId() as text
```
**Syntax + Placeholder**
```m
Diagnostics.ActivityId()
```
**Example**
```m
Diagnostics.ActivityId()
```

***
<section id="-accessing-data-functions"><h2>📂 Accessing Data Functions</h2></section>


***


### Excel.Workbook

**Syntax**
```m
Excel.Workbook(binary as binary, optional useHeaders as any) as table
```
**Syntax + Placeholder**
```m
Excel.Workbook(File.Contents("C:\Data\Sales.xlsx"), true)
```
**Example**
```m
Excel.Workbook(File.Contents("C:\Data\Sales.xlsx"), true)


```

### Excel.CurrentWorkbook

**Syntax**
```m
Excel.CurrentWorkbook() as table
```
**Syntax + Placeholder**
```m
Excel.CurrentWorkbook()
```
**Example**
```m
Excel.CurrentWorkbook(){[Name="Sales"]}[Content]


```

### Excel.TableDefinedNames

**Syntax**
```m
Excel.TableDefinedNames(workbook as any) as table
```
**Syntax + Placeholder**
```m
Excel.TableDefinedNames(File.Contents("C:\Data\Report.xlsx"))
```
**Example**
```m
Excel.TableDefinedNames(File.Contents("C:\Data\Report.xlsx"))


```

### Excel.SheetNames

**Syntax**
```m
Excel.SheetNames(workbook as any) as list
```
**Syntax + Placeholder**
```m
Excel.SheetNames(File.Contents("C:\Data\Test.xlsx"))
```
**Example**
```m
Excel.SheetNames(File.Contents("C:\Data\Test.xlsx"))


```

### Excel.CurrentWorkbook.Contents

**Syntax**
```m
Excel.CurrentWorkbook.Contents()
```
**Syntax + Placeholder**
```m
Excel.CurrentWorkbook.Contents()
```
**Example**
```m
Excel.CurrentWorkbook.Contents()


```

### Csv.Document

**Syntax**
```m
Csv.Document(binary as binary, optional options as record) as table
```
**Syntax + Placeholder**
```m
Csv.Document(File.Contents("C:\Data\sales.csv"), [Delimiter=",", Columns=5, Encoding=1252])
```
**Example**
```m
Csv.Document(File.Contents("C:\Data\sales.csv"), [Delimiter=",", Columns=5, Encoding=1252])


```

### Csv.PromoteHeaders

**Syntax**
```m
Csv.PromoteHeaders(table as table, optional options as record) as table
```
**Syntax + Placeholder**
```m
Csv.PromoteHeaders(Source)
```
**Example**
```m
Csv.PromoteHeaders(Table.FromRecords({[Col1="A", Col2="B"]}))


```

### Csv.FromRows

**Syntax**
```m
Csv.FromRows(rows as list, optional options as record) as text
```
**Syntax + Placeholder**
```m
Csv.FromRows({{"A","B"},{"C","D"}}, [Delimiter=","])
```
**Example**
```m
Csv.FromRows({{"A","B"},{"C","D"}}, [Delimiter=","])


```

### Json.Document

**Syntax**
```m
Json.Document(source as any, optional encoding as any) as any
```
**Syntax + Placeholder**
```m
Json.Document(File.Contents("C:\Data\data.json"))
```
**Example**
```m
Json.Document(File.Contents("C:\Data\data.json"))


```

### Json.FromValue

**Syntax**
```m
Json.FromValue(value as any) as binary
```
**Syntax + Placeholder**
```m
Json.FromValue([Name="John", Age=30])
```
**Example**
```m
Json.FromValue([Name="John", Age=30])


```

### Xml.Document

**Syntax**
```m
Xml.Document(source as any) as table
```
**Syntax + Placeholder**
```m
Xml.Document(File.Contents("C:\Data\data.xml"))
```
**Example**
```m
Xml.Document(File.Contents("C:\Data\data.xml"))


```

### Xml.Tables

**Syntax**
```m
Xml.Tables(source as any) as table
```
**Syntax + Placeholder**
```m
Xml.Tables(File.Contents("C:\Data\data.xml"))
```
**Example**
```m
Xml.Tables(File.Contents("C:\Data\data.xml"))


```

### Xml.Table

**Syntax**
```m
Xml.Table(source as any, optional options as record) as table
```
**Syntax + Placeholder**
```m
Xml.Table("<root><x>1</x><x>2</x></root>")
```
**Example**
```m
Xml.Table("<root><x>1</x><x>2</x></root>")


```

### Web.Contents

**Syntax**
```m
Web.Contents(url as text, optional options as record) as binary
```
**Syntax + Placeholder**
```m
Web.Contents("https://api.example.com/data")
```
**Example**
```m
Web.Contents("https://api.example.com/data")


```

### Web.Page

**Syntax**
```m
Web.Page(html as any) as table
```
**Syntax + Placeholder**
```m
Web.Page(Web.Contents("https://example.com"))
```
**Example**
```m
Web.Page(Web.Contents("https://example.com"))


```

### Web.BrowserContents

**Syntax**
```m
Web.BrowserContents(url as text) as binary
```
**Syntax + Placeholder**
```m
Web.BrowserContents("https://example.com")
```
**Example**
```m
Web.BrowserContents("https://example.com")


```

### OData.Feed

**Syntax**
```m
OData.Feed(url as any, optional options as record) as table
```
**Syntax + Placeholder**
```m
OData.Feed("https://services.odata.org/V4/Northwind/Northwind.svc")
```
**Example**
```m
OData.Feed("https://services.odata.org/V4/Northwind/Northwind.svc")


```

### ODataV2.Feed / ODataV3.Feed / ODataV4.Feed

**Syntax**
```m
ODataV2.Feed(url as any, optional options as record) as table
ODataV3.Feed(url as any, optional options as record) as table
ODataV4.Feed(url as any, optional options as record) as table
```
**Syntax + Placeholder**
```m
ODataV4.Feed("https://services.odata.org/V4/Northwind/Northwind.svc")
```
**Example**
```m
ODataV4.Feed("https://services.odata.org/V4/Northwind/Northwind.svc")


```

### Odbc.DataSource

**Syntax**
```m
Odbc.DataSource(connection as any, optional options as record) as table
```
**Syntax + Placeholder**
```m
Odbc.DataSource("dsn=MyDsn")
```
**Example**
```m
Odbc.DataSource("dsn=mydb")


```

### Odbc.Query

**Syntax**
```m
Odbc.Query(connection as any, query as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Odbc.Query("dsn=MyDsn", "SELECT 1 AS X")
```
**Example**
```m
Odbc.Query("dsn=mydb", "SELECT * FROM Sales")


```

### Odbc.InferOptions

**Syntax**
```m
Odbc.InferOptions(connection as any) as record
```
**Syntax + Placeholder**
```m
Odbc.InferOptions("dsn=MyDsn")
```
**Example**
```m
Odbc.InferOptions("dsn=mydb")


```

### OleDb.DataSource

**Syntax**
```m
OleDb.DataSource(provider as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
OleDb.DataSource("Provider=SQLOLEDB;Data Source=Server;Initial Catalog=DB;Integrated Security=SSPI;")
```
**Example**
```m
OleDb.DataSource("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\Data\;Extended Properties=""Text;HDR=YES;FMT=Delimited"";")


```

### OleDb.Query

**Syntax**
```m
OleDb.Query(provider as text, query as text) as table
```
**Syntax + Placeholder**
```m
OleDb.Query("Provider=SQLOLEDB;Data Source=Server;Initial Catalog=DB;Integrated Security=SSPI;", "SELECT 1 AS X")
```
**Example**
```m
OleDb.Query("Provider=SQLOLEDB;Data Source=Server;Initial Catalog=DB;Integrated Security=SSPI;", "SELECT TOP 10 * FROM dbo.Table")


```

### Sql.Database

**Syntax**
```m
Sql.Database(server as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Sql.Database("ServerName", "DatabaseName")
```
**Example**
```m
Sql.Database("serverName", "SalesDB")


```

### Sql.Databases

**Syntax**
```m
Sql.Databases(server as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Sql.Databases("ServerName")
```
**Example**
```m
Sql.Databases("ServerName")


```

### Sql.Execute

**Syntax**
```m
Sql.Execute(server as text, database as text, query as text) as table
```
**Syntax + Placeholder**
```m
Sql.Execute("ServerName", "DatabaseName", "SELECT 1 AS X")
```
**Example**
```m
Sql.Execute("serverName", "SalesDB", "SELECT * FROM dbo.Sales")


```

### Sql.Query

**Syntax**
```m
Sql.Query(server as text, query as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Sql.Query("ServerName", "SELECT 1 AS X")
```
**Example**
```m
Sql.Query("serverName", "SELECT TOP 10 * FROM sys.tables")


```

### AnalysisServices.Database

**Syntax**
```m
AnalysisServices.Database(server as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AnalysisServices.Database("asazure://region.asazure.windows.net/Server1", "ModelDB")
```
**Example**
```m
AnalysisServices.Database("asazure://region.asazure.windows.net/Server1", "SalesModel")


```

### AnalysisServices.Databases

**Syntax**
```m
AnalysisServices.Databases(server as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AnalysisServices.Databases("asazure://region.asazure.windows.net/Server1")
```
**Example**
```m
AnalysisServices.Databases("Server1")


```

### ActiveDirectory.Domains

**Syntax**
```m
ActiveDirectory.Domains(optional options as record) as table
```
**Syntax + Placeholder**
```m
ActiveDirectory.Domains()
```
**Example**
```m
ActiveDirectory.Domains()


```

### ActiveDirectory.Domain

**Syntax**
```m
ActiveDirectory.Domain(domain as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
ActiveDirectory.Domain("contoso.com")
```
**Example**
```m
ActiveDirectory.Domain("contoso.com")


```

### Exchange.Contents

**Syntax**
```m
Exchange.Contents(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Exchange.Contents("https://outlook.office365.com/EWS/Exchange.asmx")
```
**Example**
```m
Exchange.Contents("https://outlook.office365.com/EWS/Exchange.asmx")


```

### Exchange.Contacts

**Syntax**
```m
Exchange.Contacts(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Exchange.Contacts("https://outlook.office365.com/EWS/Exchange.asmx")
```
**Example**
```m
Exchange.Contacts("https://outlook.office365.com/EWS/Exchange.asmx")


```

### SharePoint.Contents

**Syntax**
```m
SharePoint.Contents(siteUrl as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
SharePoint.Contents("https://contoso.sharepoint.com/sites/Finance")
```
**Example**
```m
SharePoint.Contents("https://contoso.sharepoint.com/sites/Finance")


```

### SharePoint.Files

**Syntax**
```m
SharePoint.Files(siteUrl as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
SharePoint.Files("https://contoso.sharepoint.com/sites/Finance")
```
**Example**
```m
SharePoint.Files("https://contoso.sharepoint.com/sites/Finance")


```

### SharePoint.Tables

**Syntax**
```m
SharePoint.Tables(siteUrl as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
SharePoint.Tables("https://contoso.sharepoint.com/sites/Finance")
```
**Example**
```m
SharePoint.Tables("https://contoso.sharepoint.com/sites/Finance")


```

### SharePoint.Lists

**Syntax**
```m
SharePoint.Lists(siteUrl as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
SharePoint.Lists("https://contoso.sharepoint.com/sites/Finance")
```
**Example**
```m
SharePoint.Lists("https://contoso.sharepoint.com/sites/Finance")


```

### SharePoint.ContentsWithPath

**Syntax**
```m
SharePoint.ContentsWithPath(siteUrl as text, path as text) as table
```
**Syntax + Placeholder**
```m
SharePoint.ContentsWithPath("https://contoso.sharepoint.com", "/sites/Finance/Shared Documents")
```
**Example**
```m
SharePoint.ContentsWithPath("https://contoso.sharepoint.com", "/sites/Finance/Shared Documents")


```

### Folder.Files

**Syntax**
```m
Folder.Files(path as text) as table
```
**Syntax + Placeholder**
```m
Folder.Files("C:\Data")
```
**Example**
```m
Folder.Files("C:\Data")


```

### Folder.Contents

**Syntax**
```m
Folder.Contents(path as text) as table
```
**Syntax + Placeholder**
```m
Folder.Contents("C:\Data")
```
**Example**
```m
Folder.Contents("C:\Data")


```

### File.Contents

**Syntax**
```m
File.Contents(path as text) as binary
```
**Syntax + Placeholder**
```m
File.Contents("C:\Data\sales.csv")
```
**Example**
```m
File.Contents("C:\Data\sales.csv")


```

### Hdfs.Contents

**Syntax**
```m
Hdfs.Contents(path as text) as table
```
**Syntax + Placeholder**
```m
Hdfs.Contents("/user/data")
```
**Example**
```m
Hdfs.Contents("/user/data")


```

### Hadoop.FileSystem

**Syntax**
```m
Hadoop.FileSystem(contents as any) as table
```
**Syntax + Placeholder**
```m
Hadoop.FileSystem(Hdfs.Contents("/"))
```
**Example**
```m
Hadoop.FileSystem(Hdfs.Contents("/user"))


```

### Python.Execute

**Syntax**
```m
Python.Execute(script as text, optional inputs as record) as table
```
**Syntax + Placeholder**
```m
Python.Execute("import pandas as pd; df=pd.DataFrame({'A':})", [dfInput=\#table({"A"},{{1},{2}})])
```
**Example**
```m
Python.Execute("import pandas as pd; df = pd.DataFrame({'A':})")


```

### RScript.Evaluate

**Syntax**
```m
RScript.Evaluate(script as text, optional inputs as record) as table
```
**Syntax + Placeholder**
```m
RScript.Evaluate("data.frame(A=c(1,2), B=c(3,4))")
```
**Example**
```m
RScript.Evaluate("data.frame(A=c(1,2), B=c(3,4))")


```

### AzureStorage.BlobContents

**Syntax**
```m
AzureStorage.BlobContents(url as text) as binary
```
**Syntax + Placeholder**
```m
AzureStorage.BlobContents("https://account.blob.core.windows.net/container/file.csv")
```
**Example**
```m
AzureStorage.BlobContents("https://account.blob.core.windows.net/container/file.csv")


```

### AzureStorage.Contents

**Syntax**
```m
AzureStorage.Contents(account as text) as table
```
**Syntax + Placeholder**
```m
AzureStorage.Contents("account")
```
**Example**
```m
AzureStorage.Contents("account")


```

### AzureTables.Contents

**Syntax**
```m
AzureTables.Contents(account as text) as table
```
**Syntax + Placeholder**
```m
AzureTables.Contents("account")
```
**Example**
```m
AzureTables.Contents("account")


```

### AzureTable.Storage

**Syntax**
```m
AzureTable.Storage(account as text, table as text) as table
```
**Syntax + Placeholder**
```m
AzureTable.Storage("account", "MyTable")
```
**Example**
```m
AzureTable.Storage("account", "MyTable")


```

### AzureSQL.Database

**Syntax**
```m
AzureSQL.Database(server as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureSQL.Database("myserver.database.windows.net", "SalesDB")
```
**Example**
```m
AzureSQL.Database("myserver.database.windows.net", "SalesDB")


```

### AzureDataLake.Contents

**Syntax**
```m
AzureDataLake.Contents(account as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureDataLake.Contents("accountName")
```
**Example**
```m
AzureDataLake.Contents("accountName")


```

### AzureDataLake.Files

**Syntax**
```m
AzureDataLake.Files(account as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureDataLake.Files("accountName")
```
**Example**
```m
AzureDataLake.Files("accountName")


```

### AzureDataExplorer.Contents

**Syntax**
```m
AzureDataExplorer.Contents(cluster as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureDataExplorer.Contents("https://cluster.region.kusto.windows.net")
```
**Example**
```m
AzureDataExplorer.Contents("https://cluster.region.kusto.windows.net")


```

### AzureCostManagement.Tables

**Syntax**
```m
AzureCostManagement.Tables(scope as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureCostManagement.Tables("/subscriptions/<subId>")
```
**Example**
```m
AzureCostManagement.Tables("/subscriptions/<subId>")


```

### AzureDevOps.AccountContents

**Syntax**
```m
AzureDevOps.AccountContents(organization as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureDevOps.AccountContents("myorg")
```
**Example**
```m
AzureDevOps.AccountContents("myorg")


```

### AzureDevOps.Contents

**Syntax**
```m
AzureDevOps.Contents(organization as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
AzureDevOps.Contents("myorg")
```
**Example**
```m
AzureDevOps.Contents("myorg")


```

### PowerBI.Dataflows

**Syntax**
```m
PowerBI.Dataflows(optional options as record) as table
```
**Syntax + Placeholder**
```m
PowerBI.Dataflows()
```
**Example**
```m
PowerBI.Dataflows()


```

### PowerPlatform.Dataflows

**Syntax**
```m
PowerPlatform.Dataflows(optional options as record) as table
```
**Syntax + Placeholder**
```m
PowerPlatform.Dataflows()
```
**Example**
```m
PowerPlatform.Dataflows()


```

### PowerBI.Datamarts

**Syntax**
```m
PowerBI.Datamarts(optional options as record) as table
```
**Syntax + Placeholder**
```m
PowerBI.Datamarts()
```
**Example**
```m
PowerBI.Datamarts()


```

### Salesforce.Data / Salesforce.Objects / Salesforce.Reports / Salesforce.Query

**Syntax**
```m
Salesforce.Data() as table
Salesforce.Objects() as table
Salesforce.Reports() as table
Salesforce.Query(soql as text) as table
- Placeholders:
Salesforce.Data()
Salesforce.Objects()
Salesforce.Reports()
Salesforce.Query("SELECT Id, Name FROM Account")
- Examples:
Salesforce.Objects()
Salesforce.Query("SELECT Id, Name FROM Contact LIMIT 10")


```

### Dynamics365BusinessCentral.Contents

**Syntax**
```m
Dynamics365BusinessCentral.Contents(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Dynamics365BusinessCentral.Contents("https://api.businesscentral.dynamics.com/v2.0/tenant/sandbox/api/v2.0")
```
**Example**
```m
Dynamics365BusinessCentral.Contents("https://api.businesscentral.dynamics.com/v2.0/tenant/production/api/v2.0")


```

### Dynamics365.Contents

**Syntax**
```m
Dynamics365.Contents(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Dynamics365.Contents("https://org.crm.dynamics.com")
```
**Example**
```m
Dynamics365.Contents("https://org.crm.dynamics.com")


```

### CommonDataService.Database

**Syntax**
```m
CommonDataService.Database(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
CommonDataService.Database("https://org.crm.dynamics.com")
```
**Example**
```m
CommonDataService.Database("https://org.crm.dynamics.com")


```

### Dataverse.Contents

**Syntax**
```m
Dataverse.Contents(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Dataverse.Contents("https://org.crm.dynamics.com")
```
**Example**
```m
Dataverse.Contents("https://org.crm.dynamics.com")


```

### MySql.Database

**Syntax**
```m
MySql.Database(server as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
MySql.Database("localhost", "SalesDB")
```
**Example**
```m
MySql.Database("server", "db")


```

### PostgreSQL.Database

**Syntax**
```m
PostgreSQL.Database(server as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
PostgreSQL.Database("localhost", "SalesDB")
```
**Example**
```m
PostgreSQL.Database("server", "db")


```

### Teradata.Database

**Syntax**
```m
Teradata.Database(server as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Teradata.Database("tdserver")
```
**Example**
```m
Teradata.Database("tdserver")


```

### Snowflake.Databases

**Syntax**
```m
Snowflake.Databases(account as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Snowflake.Databases("myaccount")
```
**Example**
```m
Snowflake.Databases("myaccount")


```

### Snowflake.Database

**Syntax**
```m
Snowflake.Database(account as text, database as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
Snowflake.Database("myaccount", "SALES")
```
**Example**
```m
Snowflake.Database("myaccount", "SALES")


```

### GoogleBigQuery.Database

**Syntax**
```m
GoogleBigQuery.Database(optional options as record) as table
```
**Syntax + Placeholder**
```m
GoogleBigQuery.Database()
```
**Example**
```m
GoogleBigQuery.Database()


```

### GoogleSheets.Contents

**Syntax**
```m
GoogleSheets.Contents(url as text, optional options as record) as table
```
**Syntax + Placeholder**
```m
GoogleSheets.Contents("https://docs.google.com/spreadsheets/d/<id>/edit")
```
**Example**
```m
GoogleSheets.Contents("https://docs.google.com/spreadsheets/d/<id>/edit")

```


***
<section id="-binary-functions"><h2>📂 Binary Functions</h2></section>


**

### Binary.Buffer

**Syntax**
```m
Binary.Buffer(binary as binary) as binary
```
**Syntax + Placeholder**
```m
Binary.Buffer(File.Contents("C:\img.png"))
```
**Example**
```m
Binary.Buffer(File.Contents("C:\Data\image.png"))


```

### Binary.Combine

**Syntax**
```m
Binary.Combine(binaries as list) as binary
```
**Syntax + Placeholder**
```m
Binary.Combine({Text.ToBinary("A"), Text.ToBinary("B")})
```
**Example**
```m
Binary.Combine({Text.ToBinary("Hello"), Text.ToBinary("World")})


```

### Binary.From

**Syntax**
```m
Binary.From(value as any, optional options as record) as binary
```
**Syntax + Placeholder**
```m
Binary.From(123)
```
**Example**
```m
Binary.From(123)


```

### Binary.FromText

**Syntax**
```m
Binary.FromText(text as text, optional encoding as number) as binary
```
**Syntax + Placeholder**
```m
Binary.FromText("SGVsbG8=", BinaryEncoding.Base64)
```
**Example**
```m
Binary.FromText("SGVsbG8=", BinaryEncoding.Base64)


```

### Binary.ToText

**Syntax**
```m
Binary.ToText(binary as binary, optional encoding as number) as text
```
**Syntax + Placeholder**
```m
Binary.ToText(Text.ToBinary("Power"), BinaryEncoding.Base64)
```
**Example**
```m
Binary.ToText(Text.ToBinary("Power"), BinaryEncoding.Base64)


```

### Binary.Length

**Syntax**
```m
Binary.Length(binary as binary) as number
```
**Syntax + Placeholder**
```m
Binary.Length(Text.ToBinary("Test"))
```
**Example**
```m
Binary.Length(Text.ToBinary("Test"))


```

### Binary.Range

**Syntax**
```m
Binary.Range(binary as binary, offset as number, count as number) as binary
```
**Syntax + Placeholder**
```m
Binary.Range(Text.ToBinary("abcdef"), 2, 3)
```
**Example**
```m
Binary.Range(Text.ToBinary("abcdef"), 2, 3)


```

### Binary.Split

**Syntax**
```m
Binary.Split(binary as binary, size as number) as list
```
**Syntax + Placeholder**
```m
Binary.Split(Text.ToBinary("abcdef"), 2)
```
**Example**
```m
Binary.Split(Text.ToBinary("abcdef"), 2)


```

### Binary.ToList

**Syntax**
```m
Binary.ToList(binary as binary) as list
```
**Syntax + Placeholder**
```m
Binary.ToList(Text.ToBinary("AB"))
```
**Example**
```m
Binary.ToList(Text.ToBinary("AB"))


```

### Binary.Compress

- See earlier above (already provided)


```

### Binary.Decompress

- See earlier above (already provided)


```


***
<section id="-binaryformat-functions"><h2>📂 BinaryFormat Functions</h2></section>

These describe **how to read/write binary streams**.

***

### BinaryFormat.Binary

**Syntax**
```m
BinaryFormat.Binary(length as number)
```
**Syntax + Placeholder**
```m
BinaryFormat.Binary(5)
```
**Example**
```m
BinaryFormat.Binary(5)


```

### BinaryFormat.Byte

**Syntax**
```m
BinaryFormat.Byte
```
**Syntax + Placeholder**
```m
BinaryFormat.Byte
```
**Example**
```m
BinaryFormat.Byte


```

### BinaryFormat.SignedInteger8 / UnsignedInteger8

**Syntax**
```m
BinaryFormat.SignedInteger8
BinaryFormat.UnsignedInteger8
```
**Syntax + Placeholder**
```m
BinaryFormat.UnsignedInteger8
```
**Example**
```m
BinaryFormat.SignedInteger8


```

### BinaryFormat.SignedInteger16 / UnsignedInteger16

**Syntax**
```m
BinaryFormat.SignedInteger16
BinaryFormat.UnsignedInteger16
```
**Syntax + Placeholder**
```m
BinaryFormat.UnsignedInteger16
```
**Example**
```m
BinaryFormat.SignedInteger16


```

### BinaryFormat.SignedInteger32/64, UnsignedInteger32/64

**Syntax**
```m
BinaryFormat.SignedInteger32, BinaryFormat.SignedInteger64
BinaryFormat.UnsignedInteger32, BinaryFormat.UnsignedInteger64
```
**Syntax + Placeholder**
```m
BinaryFormat.SignedInteger32
```
**Example**
```m
BinaryFormat.SignedInteger32


```

### BinaryFormat.Single / Double

**Syntax**
```m
BinaryFormat.Single
BinaryFormat.Double
```
**Syntax + Placeholder**
```m
BinaryFormat.Double
```
**Example**
```m
BinaryFormat.Single


```

### BinaryFormat.Text

**Syntax**
```m
BinaryFormat.Text(encoding as number)
```
**Syntax + Placeholder**
```m
BinaryFormat.Text(BinaryEncoding.Utf8)
```
**Example**
```m
BinaryFormat.Text(BinaryEncoding.Utf8)


```

### BinaryFormat.Null

**Syntax**
```m
BinaryFormat.Null
```
**Syntax + Placeholder**
```m
BinaryFormat.Null
```
**Example**
```m
BinaryFormat.Null


```

### BinaryFormat.Choice

**Syntax**
```m
BinaryFormat.Choice(selector as function, choices as list)
```
**Syntax + Placeholder**
```m
BinaryFormat.Choice((b)=> if b<>null then 1 else 0, {BinaryFormat.Byte, BinaryFormat.Binary(4)})
```
**Example**
```m
BinaryFormat.Choice((x)=> if x=0 then 0 else 1, {BinaryFormat.Byte, BinaryFormat.Binary(2)})


```

### BinaryFormat.ChoiceRestart

**Syntax**
```m
BinaryFormat.ChoiceRestart(selector as function, choices as list)
```
**Syntax + Placeholder**
```m
BinaryFormat.ChoiceRestart((_)=>0, {BinaryFormat.Byte})
```
**Example**
```m
BinaryFormat.ChoiceRestart((_)=>0, {BinaryFormat.Byte})


```

### BinaryFormat.List

**Syntax**
```m
BinaryFormat.List(elementFormat as function, count as any)
```
**Syntax + Placeholder**
```m
BinaryFormat.List(BinaryFormat.Byte, 3)
```
**Example**
```m
BinaryFormat.List(BinaryFormat.Byte, 3)


```

### BinaryFormat.Record

**Syntax**
```m
BinaryFormat.Record(fields as record)
```
**Syntax + Placeholder**
```m
BinaryFormat.Record([A=BinaryFormat.Byte, B=BinaryFormat.SignedInteger16])
```
**Example**
```m
BinaryFormat.Record([A=BinaryFormat.Byte, B=BinaryFormat.SignedInteger16])


```

### BinaryFormat.Length

**Syntax**
```m
BinaryFormat.Length(format as function, length as number)
```
**Syntax + Placeholder**
```m
BinaryFormat.Length(BinaryFormat.Binary(10), 5)
```
**Example**
```m
BinaryFormat.Length(BinaryFormat.Binary(10), 5)


```

### BinaryFormat.ByteOrder

**Syntax**
```m
BinaryFormat.ByteOrder(format as function, byteOrder as number)
```
**Syntax + Placeholder**
```m
BinaryFormat.ByteOrder(BinaryFormat.SignedInteger16, ByteOrder.LittleEndian)
```
**Example**
```m
BinaryFormat.ByteOrder(BinaryFormat.SignedInteger32, ByteOrder.BigEndian)


```

### BinaryFormat.Group

**Syntax**
```m
BinaryFormat.Group(format as function)
```
**Syntax + Placeholder**
```m
BinaryFormat.Group(BinaryFormat.Record([A=BinaryFormat.Byte]))
```
**Example**
```m
BinaryFormat.Group(BinaryFormat.Record([A=BinaryFormat.Byte]))


```

### BinaryFormat.Repeat

**Syntax**
```m
BinaryFormat.Repeat(format as function, count as number)
```
**Syntax + Placeholder**
```m
BinaryFormat.Repeat(BinaryFormat.Byte, 4)
```
**Example**
```m
BinaryFormat.Repeat(BinaryFormat.Byte, 4)

```


***
<section id="-combiner-functions"><h2>📂 Combiner Functions</h2></section>


***

### Combiner.CombineTextByDelimiter

**Syntax**
```m
Combiner.CombineTextByDelimiter(delimiter as text, optional quoteStyle as any)
```
**Syntax + Placeholder**
```m
Combiner.CombineTextByDelimiter(",")({"A","B","C"})
```
**Example**
```m
Combiner.CombineTextByDelimiter(",")({"A","B","C"})


```

### Combiner.CombineTextByEachDelimiter

**Syntax**
```m
Combiner.CombineTextByEachDelimiter(delimiters as list, quoteStyle as any, escape as any)
```
**Syntax + Placeholder**
```m
Combiner.CombineTextByEachDelimiter({",",";"}, QuoteStyle.None, "\\")({"A,B","C;D"})
```
**Example**
```m
Combiner.CombineTextByEachDelimiter({","}, QuoteStyle.None, null)({"A","B","C"})


```

### Combiner.CombineTextByLengths

**Syntax**
```m
Combiner.CombineTextByLengths(lengths as list)
```
**Syntax + Placeholder**
```m
Combiner.CombineTextByLengths({2,3})({"AB","CDE"})
```
**Example**
```m
Combiner.CombineTextByLengths({1,2})({"A","BC"})

```


***
<section id="-comparer-functions"><h2>📂 Comparer Functions</h2></section>


***

### Comparer.Equals

**Syntax**
```m
Comparer.Equals(a as any, b as any) as logical
```
**Syntax + Placeholder**
```m
Comparer.Equals("A","a")
```
**Example**
```m
Comparer.Equals("A","a")


```

### Comparer.FromCulture

**Syntax**
```m
Comparer.FromCulture(culture as text, ignoreCase as logical)
```
**Syntax + Placeholder**
```m
Comparer.FromCulture("en-US", true)
```
**Example**
```m
Comparer.FromCulture("en-US", true)


```

### Comparer.Ordinal / Comparer.OrdinalIgnoreCase

**Syntax**
```m
Comparer.Ordinal
Comparer.OrdinalIgnoreCase
```
**Syntax + Placeholder**
```m
Comparer.OrdinalIgnoreCase
```
**Example**
```m
Comparer.Ordinal


```


***
<section id="-lines-functions"><h2>📂 Lines Functions</h2></section>


***

### Lines.FromBinary

**Syntax**
```m
Lines.FromBinary(binary as binary, optional encoding as any) as list
```
**Syntax + Placeholder**
```m
Lines.FromBinary(File.Contents("C:\Data\data.txt"))
```
**Example**
```m
Lines.FromBinary(File.Contents("C:\Data\data.txt"))


```

### Lines.ToBinary

**Syntax**
```m
Lines.ToBinary(lines as list, optional encoding as any)
```
**Syntax + Placeholder**
```m
Lines.ToBinary({"Line1","Line2"})
```
**Example**
```m
Lines.ToBinary({"Line1","Line2"})


```

### Lines.FromText

**Syntax**
```m
Lines.FromText(text as text, optional lineSeparator as any)
```
**Syntax + Placeholder**
```m
Lines.FromText("A;B;C",";")
```
**Example**
```m
Lines.FromText("A;B;C",";")


```

### Lines.ToText

**Syntax**
```m
Lines.ToText(lines as list, optional lineSeparator as any)
```
**Syntax + Placeholder**
```m
Lines.ToText({"A","B","C"}, "|")
```
**Example**
```m
Lines.ToText({"A","B","C"}, "|")
```


***
<section id="-replacer-functions"><h2>📂 Replacer Functions</h2></section>


***

### Replacer.ReplaceText

**Syntax**
```m
Replacer.ReplaceText(old as text, new as text)
```
**Syntax + Placeholder**
```m
Replacer.ReplaceText("old","new")
```
**Example**
```m
Table.ReplaceValue(\#table({"A"},{{"Hello"}}),"Hello","World", Replacer.ReplaceText, {"A"})
```

### Replacer.ReplaceValue

**Syntax**
```m
Replacer.ReplaceValue(old as any, new as any)
```
**Syntax + Placeholder**
```m
Replacer.ReplaceValue(1, 0)
```
**Example**
```m
Table.ReplaceValue(\#table({"A"},{{1}}),1,0, Replacer.ReplaceValue, {"A"})


```


***
<section id="-splitter-functions"><h2>📂 Splitter Functions</h2></section>


***

### Splitter.SplitTextByDelimiter

**Syntax**
```m
Splitter.SplitTextByDelimiter(delimiter as text, optional quoteStyle as any, optional startAt as any)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByDelimiter(",")("A,B,C")
```
**Example**
```m
Splitter.SplitTextByDelimiter(",")("A,B,C")


```

### Splitter.SplitTextByEachDelimiter

**Syntax**
```m
Splitter.SplitTextByEachDelimiter(delimiters as list, optional quoteStyle as any, optional startAt as any, optional comparer as any)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByEachDelimiter({",",";"}, QuoteStyle.None)( "A;B,C")
```
**Example**
```m
Splitter.SplitTextByEachDelimiter({","}, QuoteStyle.None)("A,B,C")


```

### Splitter.SplitTextByWhitespace

**Syntax**
```m
Splitter.SplitTextByWhitespace()
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByWhitespace()("A B  C")
```
**Example**
```m
Splitter.SplitTextByWhitespace()("A B C")


```

### Splitter.SplitTextByCharacterTransition

**Syntax**
```m
Splitter.SplitTextByCharacterTransition(accept as function, reject as function)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByCharacterTransition(Character.IsLetter, Character.IsDigit)("Ab12Cd")
```
**Example**
```m
Splitter.SplitTextByCharacterTransition(Character.IsLetter, Character.IsDigit)("Ab12")


```

### Splitter.SplitTextByLengths

**Syntax**
```m
Splitter.SplitTextByLengths(lengths as list)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByLengths({2,3})("ABCDE")
```
**Example**
```m
Splitter.SplitTextByLengths({2,3})("ABCDE")


```

### Splitter.SplitTextByPositions

**Syntax**
```m
Splitter.SplitTextByPositions(positions as list)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByPositions({2,4})("ABCDEFG")
```
**Example**
```m
Splitter.SplitTextByPositions({2,4})("ABCDEFG")


```

### Splitter.SplitTextByRanges

**Syntax**
```m
Splitter.SplitTextByRanges(ranges as list)
```
**Syntax + Placeholder**
```m
Splitter.SplitTextByRanges({{0,2},{2,3}})("ABCDE")
```
**Example**
```m
Splitter.SplitTextByRanges({{0,2},{2,3}})("ABCDE")
```


***
<section id="-uri-functions"><h2>📂 Uri Functions</h2></section>


***

### Uri.Parts

**Syntax**
```m
Uri.Parts(uri as text) as record
```
**Syntax + Placeholder**
```m
Uri.Parts("https://example.com/page?x=1")
```
**Example**
```m
Uri.Parts("https://example.com/page?x=1")


```

### Uri.BuildQueryString

**Syntax**
```m
Uri.BuildQueryString(record as record) as text
```
**Syntax + Placeholder**
```m
Uri.BuildQueryString([x=1, y=2])
```
**Example**
```m
Uri.BuildQueryString([x=1, y=2])


```

### Uri.EscapeDataString

**Syntax**
```m
Uri.EscapeDataString(text as text) as text
```
**Syntax + Placeholder**
```m
Uri.EscapeDataString("a b")
```
**Example**
```m
Uri.EscapeDataString("a b")


```

### Uri.UnescapeDataString

**Syntax**
```m
Uri.UnescapeDataString(text as text) as text
```
**Syntax + Placeholder**
```m
Uri.UnescapeDataString("a%20b")
```
**Example**
```m
Uri.UnescapeDataString("a%20b")

```


***
<section id="-value-functions"><h2>📂 Value Functions</h2></section>


***

### Value.Type

**Syntax**
```m
Value.Type(value as any) as type
```
**Syntax + Placeholder**
```m
Value.Type("Hello")
```
**Example**
```m
Value.Type("Hello")


```

### Value.ReplaceType

**Syntax**
```m
Value.ReplaceType(value as any, type as type) as any
```
**Syntax + Placeholder**
```m
Value.ReplaceType(123, type text)
```
**Example**
```m
Value.ReplaceType(123, type text)


```

### Value.Metadata

- See earlier (provided)


```

### Value.AddMetadata

- See earlier (provided)


```

### Value.Is

**Syntax**
```m
Value.Is(value as any, type as type) as logical
```
**Syntax + Placeholder**
```m
Value.Is(123, type number)
```
**Example**
```m
Value.Is(123, type number)


```

### Value.As

**Syntax**
```m
Value.As(value as any, type as type) as any
```
**Syntax + Placeholder**
```m
Value.As(123, type number)
```
**Example**
```m
Value.As(123, type number)


```

### Value.FromText

**Syntax**
```m
Value.FromText(text as text, optional culture as text) as any
```
**Syntax + Placeholder**
```m
Value.FromText("123")
```
**Example**
```m
Value.FromText("123")


```

### Value.ToText

**Syntax**
```m
Value.ToText(value as any, optional format as any, optional culture as text) as text
```
**Syntax + Placeholder**
```m
Value.ToText(123, "D4")
```
**Example**
```m
Value.ToText(123, "D4")


```

### Value.Compare

**Syntax**
```m
Value.Compare(a as any, b as any, optional comparer as any) as number
```
**Syntax + Placeholder**
```m
Value.Compare(1,2)
```
**Example**
```m
Value.Compare(1,2)


```

### Value.Equals

**Syntax**
```m
Value.Equals(a as any, b as any, optional precision as any) as logical
```
**Syntax + Placeholder**
```m
Value.Equals(3.1415, 3.1415)
```
**Example**
```m
Value.Equals(3.1415, 3.1415)


```

### Value.NullableEquals

**Syntax**
```m
Value.NullableEquals(a as any, b as any) as logical
```
**Syntax + Placeholder**
```m
Value.NullableEquals(null, null)
```
**Example**
```m
Value.NullableEquals(null, null)


```

### Value.ExpandRecord

**Syntax**
```m
Value.ExpandRecord(record as record) as list
```
**Syntax + Placeholder**
```m
Value.ExpandRecord([a=1,b=2])
```
**Example**
```m
Value.ExpandRecord([a=1,b=2])


```

### Value.ReplaceError

**Syntax**
```m
Value.ReplaceError(value as any, replacement as any) as any
```
**Syntax + Placeholder**
```m
Value.ReplaceError(try 1/0 otherwise null, -1)
```
**Example**
```m
Value.ReplaceError(try 1/0 otherwise null, -1)


```

***
<section id="-expression--error--diagnostics"><h2>📂 Expression &amp; Error &amp; Diagnostics</h2></section>


***

### Expression.Evaluate

**Syntax**
```m
Expression.Evaluate(text as text, optional environment as record)
```
**Syntax + Placeholder**
```m
Expression.Evaluate("2+3")
```
**Example**
```m
Expression.Evaluate("2+3")


```

### Expression.Identifier

**Syntax**
```m
Expression.Identifier(name as text)
```
**Syntax + Placeholder**
```m
Expression.Identifier("My Name")
```
**Example**
```m
Expression.Identifier("My Name")


```

### Expression.Constant

**Syntax**
```m
Expression.Constant(value as any)
```
**Syntax + Placeholder**
```m
Expression.Constant(42)
```
**Example**
```m
Expression.Constant(42)


```

### Error.Record

**Syntax**
```m
Error.Record(reason as text, message as text, detail as any) as record
```
**Syntax + Placeholder**
```m
Error.Record("Invalid", "Something went wrong", [Step="Load"])
```
**Example**
```m
Error.Record("Error", "Message", "Details")


```

### Error.Raise

**Syntax**
```m
Error.Raise(reason as text, message as text, optional detail as any) as none
```
**Syntax + Placeholder**
```m
Error.Raise("InvalidOperation", "Bad input", [Input=null])
```
**Example**
```m
Error.Raise("Invalid", "No data")


```

### Diagnostics.Trace

- See earlier


```

### Diagnostics.ActivityId

- See earlier


```


***

***
<section id="-table-helper-functions"><h2>📂 Table Helper Functions</h2></section>


***

### Table.SelectColumns

**Syntax**
```m
Table.SelectColumns(table as table, columns as any, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.SelectColumns(\#table({"A","B"}, {{1,2}}), {"A"})
```
**Example**
```m
Table.SelectColumns(\#table({"A","B"}, {{1,2},{3,4}}), {"A"})


```

### Table.RemoveColumns

**Syntax**
```m
Table.RemoveColumns(table as table, columns as list, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.RemoveColumns(\#table({"A","B"}, {{1,2}}), {"B"})
```
**Example**
```m
Table.RemoveColumns(\#table({"A","B"}, {{1,2},{3,4}}), {"B"})


```

### Table.RenameColumns

**Syntax**
```m
Table.RenameColumns(table as table, renames as list, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.RenameColumns(\#table({"A"},{{1}}), {{"A","Alpha"}})
```
**Example**
```m
Table.RenameColumns(\#table({"A"},{{1}}), {{"A","Alpha"}})


```

### Table.ReorderColumns

**Syntax**
```m
Table.ReorderColumns(table as table, columns as list, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.ReorderColumns(\#table({"A","B"},{{1,2}}), {"B","A"})
```
**Example**
```m
Table.ReorderColumns(\#table({"A","B"},{{1,2}}), {"B","A"})


```

### Table.TransformColumns

**Syntax**
```m
Table.TransformColumns(table as table, transformations as list, optional defaultTransformation as any, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.TransformColumns(\#table({"A"},{{"x"}}), {{"A", Text.Upper, type text}})
```
**Example**
```m
Table.TransformColumns(\#table({"A"},{{"x"}}), {{"A", Text.Upper, type text}})


```

### Table.TransformColumnTypes

**Syntax**
```m
Table.TransformColumnTypes(table as table, typeTransformations as list, optional culture as text, optional missingField as any)
```
**Syntax + Placeholder**
```m
Table.TransformColumnTypes(\#table({"A"},{{"1"}}), {{"A", Int64.Type}})
```
**Example**
```m
Table.TransformColumnTypes(\#table({"A"},{{"1"}}), {{"A", Int64.Type}})


```

### Table.SplitColumn

**Syntax**
```m
Table.SplitColumn(table as table, column as text, splitter as function, optional newColumnNames as list, optional default as any, optional extraValues as any)
```
**Syntax + Placeholder**
```m
Table.SplitColumn(\#table({"Full"},{{"A,B"}}), "Full", Splitter.SplitTextByDelimiter(","), {"Col1","Col2"})
```
**Example**
```m
Table.SplitColumn(\#table({"Full"},{{"A,B"}}), "Full", Splitter.SplitTextByDelimiter(","), {"Col1","Col2"})


```

### Table.AddColumn

**Syntax**
```m
Table.AddColumn(table as table, newColumnName as text, columnGenerator as function, optional columnType as any)
```
**Syntax + Placeholder**
```m
Table.AddColumn(\#table({"A"},{{1}}), "B", each [A]*2, Int64.Type)
```
**Example**
```m
Table.AddColumn(\#table({"A"},{{1},{2}}), "B", each [A]*2, Int64.Type)


```

### Table.AddIndexColumn

**Syntax**
```m
Table.AddIndexColumn(table as table, newColumnName as text, optional initialValue as number, optional increment as number, optional columnType as any)
```
**Syntax + Placeholder**
```m
Table.AddIndexColumn(\#table({"A"},{{1},{2}}), "Index", 0, 1, Int64.Type)
```
**Example**
```m
Table.AddIndexColumn(\#table({"A"},{{1},{2}}), "Index", 0, 1, Int64.Type)

```


***

***
<section id="-text-helper-functions"><h2>📂 Text Helper Functions</h2></section>


***

### Text.Contains

**Syntax**
```m
Text.Contains(text as text, substring as text, optional comparer as any) as logical
```
**Syntax + Placeholder**
```m
Text.Contains("Hello","ell")
```
**Example**
```m
Text.Contains("Hello","ell")


```

### Text.StartsWith

**Syntax**
```m
Text.StartsWith(text as text, substring as text, optional comparer as any)
```
**Syntax + Placeholder**
```m
Text.StartsWith("Hello","He")
```
**Example**
```m
Text.StartsWith("Hello","He")


```

### Text.EndsWith

**Syntax**
```m
Text.EndsWith(text as text, substring as text, optional comparer as any)
```
**Syntax + Placeholder**
```m
Text.EndsWith("Hello","lo")
```
**Example**
```m
Text.EndsWith("Hello","lo")


```

### Text.Split

**Syntax**
```m
Text.Split(text as text, delimiter as text, optional quoteStyle as any)
```
**Syntax + Placeholder**
```m
Text.Split("A,B,C", ",")
```
**Example**
```m
Text.Split("A,B,C", ",")


```

### Text.SplitAny

**Syntax**
```m
Text.SplitAny(text as text, separators as any)
```
**Syntax + Placeholder**
```m
Text.SplitAny("A;B,C", ",;")
```
**Example**
```m
Text.SplitAny("A;B,C", ",;")


```

### Text.SplitByLengths

**Syntax**
```m
Text.SplitByLengths(text as text, lengths as list)
```
**Syntax + Placeholder**
```m
Text.SplitByLengths("ABCDE", {2,3})
```
**Example**
```m
Text.SplitByLengths("ABCDE", {2,3})


```

### Text.SplitByPositions

**Syntax**
```m
Text.SplitByPositions(text as text, positions as list)
```
**Syntax + Placeholder**
```m
Text.SplitByPositions("ABCDEFG", {2,4})
```
**Example**
```m
Text.SplitByPositions("ABCDEFG", {2,4})


```

### Text.ReplaceEach

**Syntax**
```m
Text.ReplaceEach(text as text, replacements as list)
```
**Syntax + Placeholder**
```m
Text.ReplaceEach("Hello World", {{"Hello","Hi"},{"World","All"}})
```
**Example**
```m
Text.ReplaceEach("Hello World", {{"Hello","Hi"}})
```


***

***
<section id="-number-helper-functions"><h2>📂 Number Helper Functions</h2></section>


***

### Number.Round

**Syntax**
```m
Number.Round(number as nullable number, optional digits as nullable number, optional roundingMode as any)
```
**Syntax + Placeholder**
```m
Number.Round(3.14159, 2)
```
**Example**
```m
Number.Round(3.14159, 2)


```

### Number.Divide

**Syntax**
```m
Number.Divide(number as nullable number, divisor as nullable number, optional precision as any)
```
**Syntax + Placeholder**
```m
Number.Divide(10, 3)
```
**Example**
```m
Number.Divide(10, 3)


```

### Number.ToText

**Syntax**
```m
Number.ToText(number as nullable number, optional format as any, optional culture as text)
```
**Syntax + Placeholder**
```m
Number.ToText(1234.56, "N2", "en-US")
```
**Example**
```m
Number.ToText(1234.56, "N2", "en-US")


```

### Number.FromText

**Syntax**
```m
Number.FromText(text as text, optional culture as text)
```
**Syntax + Placeholder**
```m
Number.FromText("1,234.56", "en-US")
```
**Example**
```m
Number.FromText("1,234.56", "en-US")
```


***

***
<section id="-datetime-overloads"><h2>📂 Date/Time Overloads</h2></section>


***

### Date.ToText

**Syntax**
```m
Date.ToText(date as date, optional format as any, optional culture as text)
```
**Syntax + Placeholder**
```m
Date.ToText(\#date(2025,8,20), "yyyy-MM-dd")
```
**Example**
```m
Date.ToText(\#date(2025,8,20), "yyyy-MM-dd")


```

### Time.ToText

**Syntax**
```m
Time.ToText(time as time, optional format as any, optional culture as text)
```
**Syntax + Placeholder**
```m
Time.ToText(\#time(11,26,0), "HH:mm:ss")
```
**Example**
```m
Time.ToText(\#time(11,26,0), "HH:mm:ss")


```

### DateTime.ToText

**Syntax**
```m
DateTime.ToText(datetime as datetime, optional format as any, optional culture as text)
```
**Syntax + Placeholder**
```m
DateTime.ToText(\#datetime(2025,8,20,11,26,0), "yyyy-MM-dd HH:mm:ss")
```
**Example**
```m
DateTime.ToText(\#datetime(2025,8,20,11,26,0), "yyyy-MM-dd HH:mm:ss")


```

### DateTime.AddZone

**Syntax**
```m
DateTime.AddZone(datetime as datetime, offset as number) as datetimezone
```
**Syntax + Placeholder**
```m
DateTime.AddZone(\#datetime(2025,8,20,11,26,0), +5.5)
```
**Example**
```m
DateTime.AddZone(\#datetime(2025,8,20,11,26,0), +5.5)


```

### DateTimeZone.SwitchZone

**Syntax**
```m
DateTimeZone.SwitchZone(datetimezone as datetimezone, offset as number) as datetimezone
```
**Syntax + Placeholder**
```m
DateTimeZone.SwitchZone(\#datetimezone(2025,8,20,11,26,0,+5.5), 0)
```
**Example**
```m
DateTimeZone.SwitchZone(\#datetimezone(2025,8,20,11,26,0,+5.5), 0)


```

### DateTimeZone.ToLocal

**Syntax**
```m
DateTimeZone.ToLocal(datetimezone as datetimezone) as datetime
```
**Syntax + Placeholder**
```m
DateTimeZone.ToLocal(\#datetimezone(2025,8,20,11,26,0,0))
```
**Example**
```m
DateTimeZone.ToLocal(\#datetimezone(2025,8,20,11,26,0,0))


```

### DateTimeZone.RemoveZone

**Syntax**
```m
DateTimeZone.RemoveZone(datetimezone as datetimezone) as datetime
```
**Syntax + Placeholder**
```m
DateTimeZone.RemoveZone(\#datetimezone(2025,8,20,11,26,0,+5.5))
```
**Example**
```m
DateTimeZone.RemoveZone(\#datetimezone(2025,8,20,11,26,0,+5.5))
```
***


# Other Functions/Syntaxes from powerquery-m.pdf
- 0 
(optional x)
- 0 
(x)
- 0 ("#0.0#;(#0.0#)
- 0 (zero)
- 00
(depends on local or cloud computer
settings)
- 00
(midnight)
- 00 (Desktop)
- 00 (Local)
- 00 (Online)
- 00 (Unspecified)
- 00 (Utc)
- 00 (midnight)
- 00 (noon)
- 0003 ("####")
- 0329112756
("E", en-US)
- 0329112756
("E2", fr-FR)
- 0329112756
("e", fr-FR)
- 03697 ("#0.00‰",
en-US)
- 03697 ("#0.00‰",
ru-RU)
- 1 
(_)
- 1 
(x, optional y)
- 1 ("P", en-US)
- 1 ("P", fr-FR)
- 1 ("X4")
- 1 ("x")
- 111 (222)
- 12 (or
from 1 to 13 for calendars that have 13 months)
- 1234 ("D")
- 1234 ("D6")
- 1234 ("F1", de-DE)
- 1234 ("F1", en-US)
- 1234 ("N1", en-US)
- 1234 ("N1", ru-RU)
- 15 (en-US)
- 15 (ja-JP)
- 2009 (da-DK)
- 2009 (de-DE)
- 2009 (en-US)
- 2009 (fr-FR)
- 2009 (id-ID)
- 2147483647
("##,#", en-US)
- 2147483647
("##,#", es-ES)
- 2147483647 ("#,#,,",
en-US)
- 2147483647 ("#,#,,",
es-ES)
- 25
("G", en-US)
- 25
("G", sv-SE)
- 255 ("X")
- 255 ("x4")
- 3 (5 cubed)
- 3 (refers to shared A from Section1)
- 30 (""arr:"" h:m t)
- 30 (%h)
- 30 ('arr:' h:m t)
- 30 (7 hours and 30 minutes past UTC)
- 30 (Local)
- 30 (Unspecified)
- 30 (Utc)
- 30 (arr hh:mm t)
- 30 (es-ES)
- 30 (h ""h"")
- 30 (h 'h')
- 30 (h \h)
- 30 (hr-HR)
- 30 (sv-SE)
- 30 (zh-CN)
- 333 (444"
Text.BetweenDelimiters("111 (222)
- 333 (444)
- 345 ("#0.0#;
(#0.0#)
- 3697 ("##.0 %",
el-GR)
- 3697 ("##.0 %",
en-US)
- 3697 ("%#0.00",
el-GR)
- 3697 ("%#0.00",
en-US)
- 39678 ("P1", en-US)
- 39678 ("P1", fr-FR)
- 45
(es-ES)
- 45
(zh-CN)
- 45 (hr-HR)
- 45 (sv-SE)
- 4546 ("G4", en-
US)
- 4546 ("G4", sv-SE)
- 456 ("C", en-US)
- 456 ("C", fr-FR)
- 456 ("C", ja-JP)
- 456 ("C3", en-
US)
- 456 ("C3", fr-FR)
- 456 ("C3", ja-JP)
- 456 ("G", en-US)
- 456 ("G", sv-SE)
- 45678 ("#.##", en-
US)
- 45678 ("#.##", fr-
FR)
- 45678 ("0.00", en-
US)
- 45678 ("0.00", fr-
FR)
- 56 ("F4", de-DE)
- 56 ("F4", en-US)
- 56 ("N3", en-
US)
- 56 ("N3", ru-
RU)
- 567 ("F", de-DE)
- 567 ("F", en-US)
- 567 ("N", en-US)
- 567 ("N", ru-RU)
- 5678
("#####")
- 5678
("00000")
- 5807
(positive or negative)
- 647
(2^31–1)
- 648 (–2^31)
- 65001  (UTF-8)
- 65001 (UTF-8)
- 68 ("# 'degrees'")
- 68 ("# °")
- 68 ("#' degrees'")
- 7 
(1 + 2)
- 767 (2^15-1)
- 768 (–2^15)
- 7BitEncodedSignedInteger(binary as binary)
- 7BitEncodedUnsignedInteger(binary as binary)
- 807 (2^63–1)
- 808 (–2^63)
- 92311
("0.0##e+00")
- 987654
("""#""##00""#""")
- 987654
("'#'##00'#'")
- 987654
("\###00\#")
- 987654 ("#0.0e0")
- Abs(-3)
- Abs(x - y)
- Accounts(optional options as nullable record)
- Accumulate(
    list as list,
    seed as any,
    accumulator as function
)
- Accumulate({1, 2, 3, 4, 5}, 0, (state, current)
- Add(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Add(1, 1)
- Add(1, 2)
- AddAndExpandDimensionColumn(
    cube as table,
    dimensionSelector as any,
    attributeNames as list,
    optional newColumnNames as any
)
- AddColumn(
        Source,
        "Email Address", 
        each Text.Combine({
            Text.Start([First Name], 4)
- AddColumn(
        Source, 
        "EndTime", 
        each [StartTime] + #duration(0, 0, 0, [Seconds])
- AddColumn(
    Table.FromRecords({
        [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0, 
Shipping = 10.00],
        [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0, Shipping 
= 15.00],
        [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25.0, Shipping 
= 10.00]
    })
- AddColumn(
    table as table,
    newColumnName as text,
    columnGenerator as function,
    optional columnType as nullable type
)
- AddColumn(Source, "Full Name", each Text.Combine({[First 
Name], [Middle Initial], [Last Name]}, " ")
- AddDays(#date(2011, 5, 14)
- AddDays(dateTime as any, numberOfDays as number)
- AddField(
    record as record,
    fieldName as text,
    value as any,
    optional delayed as nullable logical
)
- AddField([CustomerID = 1, Name = "Bob", Phone = "123-4567"], "Address", 
"123 Main St.")
- AddFuzzyClusterColumn(
        Source, "Fruit", "Cluster", 
        [IgnoreCase = true, IgnoreSpace = true, Threshold = 0.5]
    )
- AddFuzzyClusterColumn(
    Table.FromRecords(
        {
            [EmployeeID = 1, Location = "Seattle"],
            [EmployeeID = 2, Location = "seattl"],
            [EmployeeID = 3, Location = "Vancouver"],
            [EmployeeID = 4, Location = "Seatle"],
            [EmployeeID = 5, Location = "vancover"],
            [EmployeeID = 6, Location = "Seattle"],
            [EmployeeID = 7, Location = "Vancouver"]
        },
        type table [EmployeeID = nullable number, Location = nullable text]
    )
- AddFuzzyClusterColumn(
    table as table,
    columnName as text,
    newColumnName as text,
    optional options as nullable record
)
- AddIndexColumn(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- AddIndexColumn(
    table as table,
    newColumnName as text,
    optional initialValue as nullable number,
    optional increment as nullable number,
    optional columnType as nullable type
)
- AddJoinColumn(
    Table.FromRecords({
        [saleID = 1, item = "Shirt"],
        [saleID = 2, item = "Hat"]
    })
- AddJoinColumn(
    table1 as table,
    key1 as any,
    table2 as function,
    key2 as any,
    newColumnName as text
)
- AddKey(
    table as table,
    columns as list,
    isPrimary as logical
)
- AddKey(table, {"Id"}, true)
- AddMeasureColumn(
    cube as table,
    column as text,
    measureSelector as any
)
- AddMonths(#date(2011, 5, 14)
- AddMonths(#datetime(2011, 5, 14, 8, 15, 22)
- AddMonths(dateTime as any, numberOfMonths as number)
- AddOne(5)
- AddQuarters(#date(2011, 5, 14)
- AddQuarters(dateTime as any, numberOfQuarters as number)
- AddRankColumn(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Revenue = 200],
        [CustomerID = 2, Name = "Jim", Revenue = 100],
        [CustomerID = 3, Name = "Paul", Revenue = 200],
        [CustomerID = 4, Name = "Ringo", Revenue = 50]
    })
- AddRankColumn(
    table as table,
    newColumnName as text,
    comparisonCriteria as any,
    optional options as nullable record
)
- AddTableKey(
    table as type,
    columns as list,
    isPrimary as logical
)
- AddTableKey(BaseType, {"ID"}, true)
- AddTableKey(tableType, {"A", "B"}, false)
- AddTableKey(type table [ID = number, Name = text], {"ID"}, 
true)
- AddWeeks(#date(2011, 5, 14)
- AddWeeks(dateTime as any, numberOfWeeks as number)
- AddYears(#date(2011, 5, 14)
- AddYears(#datetime(2011, 5, 14, 8, 15, 22)
- AddYears(dateTime as any, numberOfYears as number)
- AddZone(
    dateTime as nullable datetime,
    timezoneHours as number,
    optional timezoneMinutes as nullable number
)
- AddZone(#datetime(2010, 12, 31, 11, 56, 02)
- AfterDelimiter("111-222-333", "-")
- AfterDelimiter("111-222-333", "-", 1)
- AfterDelimiter("111-222-333", "-", {1, RelativePosition.FromEnd})
- AfterDelimiter(text as nullable text, delimiter as text, optional index as 
any)
- AggregateTableColumn(
    Table.FromRecords(
        {
            [
                t = Table.FromRecords({
                    [a = 1, b = 2, c = 3],
                    [a = 2, b = 4, c = 6]
                })
- AggregateTableColumn(
    table as table,
    column as text,
    aggregations as list
)
- AllTrue({true, false, 2 < 0})
- AllTrue({true, true, 2 > 0})
- Alternate(
    list as list,
    count as number,
    optional repeatInterval as nullable number,
    optional offset as nullable number
)
- Alternate({1..10}, 1)
- Alternate({1..10}, 1, 1)
- Alternate({1..10}, 1, 1, 1)
- Alternate({1..10}, 1, 2, 1)
- AlternateRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- AlternateRows(
    table as table,
    offset as number,
    skip as number,
    take as number
)
- Alternates(alternates as list)
- AnyTrue({2 = 0, false, 2 < 0})
- AnyTrue({true, false, 2>0})
- ApplyParameter(
    cube as table,
    parameter as any,
    optional arguments as nullable list
)
- ApproximateLength(Binary.FromText("i45WMlSKjQUA", BinaryEncoding.Base64)
- ApproximateLength(binary as nullable binary)
- ApproximateRowCount(Table.Distinct(Table.SelectColumns(sqlTable, {"city", 
"state"})
- ApproximateRowCount(table as table)
- As("abc", type number)
- As(123, Number.Type)
- At("Hello, World", 4)
- At(text as nullable text, index as number)
- Atan2(y as nullable number, x as nullable number)
- AttributeMemberId(attribute as any)
- AttributeMemberProperty(attribute as any, propertyName as text)
- Average(list as list, optional precision as nullable number)
- Average({#date(2011, 1, 1)
- Average({3, 4, 6})
- BeforeDelimiter("111-222-333", "-")
- BeforeDelimiter("111-222-333", "-", 1)
- BeforeDelimiter("111-222-333", "-", {1, RelativePosition.FromEnd})
- BeforeDelimiter(text as nullable text, delimiter as text, optional index as 
any)
- BetweenDelimiters(
    text as nullable text,
    startDelimiter as text,
    endDelimiter as text,
    optional startIndex as any,
    optional endIndex as any
)
- BetweenDelimiters("111 (222)
- Binary(optional length as any)
- BitwiseAnd(number1 as nullable number, number2 as nullable number)
- BitwiseNot(number as any)
- BitwiseOr(number1 as nullable number, number2 as nullable number)
- BitwiseShiftLeft(number1 as nullable number, number2 as nullable number)
- BitwiseShiftRight(number1 as nullable number, number2 as nullable number)
- BitwiseXor(number1 as nullable number, number2 as nullable number)
- BlobContents(url as text, optional options as nullable record)
- Blobs(account as text, optional options as nullable record)
- BrowserContents("https://microsoft.com")
- BrowserContents("https://microsoft.com", [WaitFor = [Selector = "div.ready", 
Timeout = #duration(0,0,0,10)
- BrowserContents("https://microsoft.com", [WaitFor = [Selector = "div.ready"]])
- BrowserContents("https://microsoft.com", [WaitFor = [Timeout = 
#duration(0,0,0,10)
- BrowserContents(url as text, optional options as nullable record)
- Buffer(Binary.FromList({0..10})
- Buffer(MyTable)
- Buffer(binary as nullable binary)
- Buffer(table as table, optional options as nullable record)
- Buffer({1..10})
- BuildQueryString([a = "1", b = "+$"])
- BuildQueryString(query as record)
- Byte(binary as binary)
- ByteOrder(binaryFormat as function, byteOrder as number)
- CCSID (Coded Character Set Identifier)
- Choice(
        BinaryFormat.Byte,
        (length)
- Choice(
    binaryFormat as function,
    chooseFunction as function,
    optional type as nullable type,
    optional combineFunction as nullable function
)
- Clean("ABC#(lf)
- Clean(text as nullable text)
- ClosedRecord(type [A = number, ...])
- ClosedRecord(type as type)
- CollapseAndRemoveColumns(cube as table, columnNames as list)
- Column(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- Column("CustomerName")
- Column(columnName as text)
- Column(columnName)
- ColumnCount(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- ColumnNames(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- ColumnsOfType(
    Table.FromRecords(
        {[CustomerID = 1, Name = "Bob"]},
        type table[CustomerID = Number.Type, Name = Text.Type]
    )
- ColumnsOfType(
    Table.FromRecords(
        {[a = 1, b = "hello"]},
        type table[a = Number.Type, b = Text.Type]
    )
- ColumnsOfType(table as table, listOfTypes as list)
- Combinations(5, 3)
- Combinations(setSize as nullable number, combinationSize as nullable 
number)
- Combine(
    {
        Table.FromRecords({[Name = "Bob", Phone = "123-4567"]})
- Combine(baseUri as text, relativeUri as text)
- Combine(tables as list, optional columns as any)
- Combine(texts as list, optional separator as nullable text)
- Combine({
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- Combine({
    Table.FromRecords({[Name = "Bob", Phone = "123-4567"]})
- Combine({
    [CustomerID = 1, Name = "Bob"],
    [Phone = "123-4567"]
})
- Combine({"OrderID#|#Color", "1#|#Red", "2#|#Blue"}, "#(cr)
- Combine({"OrderID,Item", "1,Fishing rod", "2,1 lb. worms"}, "#(cr)
- Combine({"Seattle", "WA"})
- Combine({"Seattle", "WA"}, ", ")
- Combine({"Seattle", null, "WA"}, ", ")
- Combine({{1, 2}, {3, 4}})
- Combine({{1, 2}, {3, {4, 5}}})
- CombineColumns(
    Table.FromRecords({[FirstName = "Bob", LastName = "Smith"]})
- CombineColumns(
    table as table,
    sourceColumns as list,
    combiner as function,
    column as text
)
- CombineColumns(
Output
Power Query M
        Source,
        {"Column1", "Column2"},
        Combiner.CombineTextByDelimiter(",", QuoteStyle.Csv)
- CombineColumnsToRecord(
    table as table,
    newColumnName as text,
    sourceColumns as list,
    optional options as nullable record
)
- CombineTextByDelimiter(",", QuoteStyle.None)
- CombineTextByDelimiter(";")
- CombineTextByDelimiter(delimiter as text, optional quoteStyle as nullable 
number)
- CombineTextByEachDelimiter(delimiters as list, optional quoteStyle as 
nullable number)
- CombineTextByEachDelimiter({"=", "+"})
- CombineTextByLengths(lengths as list, optional template as nullable text)
- CombineTextByLengths({1, 2, 3})
- CombineTextByLengths({1, 2, 3}, "*********")
- CombineTextByPositions(positions as list, optional template as nullable 
text)
- CombineTextByPositions({0, 5, 10})
- CombineTextByRanges(ranges as list, optional template as nullable text)
- CombineTextByRanges({{0, 1}, {3, 2}, {6, null}})
- Compare(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Compare(1/x, 1/y)
- Compress(Binary.FromList(List.Repeat({10}, 1000)
- Compress(binary as nullable binary, compressionType as number)
- ConditionToIdentities(identityProvider as function, condition 
as function)
- ConformToPageReader(list as list, optional options as nullable record)
- ConformToPageReader(table as table, shapingFunction as function)
- Consortium (OGC)
- Constant("abc")
- Constant(#date(2035, 01, 02)
- Containers(account as text)
- Contains(
        "The rain in spain falls mainly on the plain.", 
        "Spain", 
        Comparer.OrdinalIgnoreCase
    )
- Contains(
        {"Squash", "Pumpkin", "ApPlE", "pear", "orange", "APPLE", "Pear", "pear"},
        "apple",
        Comparer.OrdinalIgnoreCase
    )
- Contains(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- Contains(
    list as list,
    value as any,
    optional equationCriteria as any
)
- Contains(
    table as table,
    row as record,
    optional equationCriteria as any
)
- Contains("Hello World", "Hello")
- Contains("Hello World", "hello")
- Contains("Hello World", "hello", Comparer.OrdinalIgnoreCase)
- Contains(Source, Date.From("4/8/2022")
- Contains([Account Code], "7")
- Contains([Name], "B")
- Contains(text as nullable text, substring as text, optional comparer as 
nullable function)
- Contains({"Pears", "Bananas", "Rhubarb", "Peaches"},
    "rhubarb",
    Comparer.OrdinalIgnoreCase
)
- Contains({1, 2, 3, 4, 5}, 3)
- Contains({1, 2, 3, 4, 5}, 6)
- ContainsAll(
        {"Squash", "Pumpkin", "ApPlE", "pear", "orange", "APPLE", "Pear", "pear"},
        {"apple", "pear", "squash", "pumpkin", "cucumber"},
        Comparer.OrdinalIgnoreCase
    )
- ContainsAll(
        {"Squash", "Pumpkin", "ApPlE", "pear", "orange", "APPLE", "Pear", "pear"},
        {"apple", "pear", "squash", "pumpkin"},
        Comparer.OrdinalIgnoreCase
    )
- ContainsAll(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- ContainsAll(
    table as table,
    rows as list,
    optional equationCriteria as any
)
- ContainsAll(Source, {#date(2022, 4, 8)
- ContainsAll(list as list, values as list, optional equationCriteria as any)
- ContainsAll({"dog", "cat", "racoon", "horse", "rabbit"}, {"DOG", "Horse"}, 
Comparer.OrdinalIgnoreCase)
- ContainsAll({1, 2, 3, 4, 5}, {3, 4})
- ContainsAll({1, 2, 3, 4, 5}, {5, 6})
- ContainsAny(
        {"Squash", "Pumpkin", "ApPlE", "PEAR", "orange", "APPLE", "Pear", "peaR"},
        {"apple","pear"},
        Comparer.OrdinalIgnoreCase
    )
- ContainsAny(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 3, b = 4]
    })
- ContainsAny(
    table as table,
    rows as list,
    optional equationCriteria as any
)
- ContainsAny(Source, {Date.From("Apr 8, 2022")
- ContainsAny(list as list, values as list, optional equationCriteria as any)
- ContainsAny({"dog", "cat", "racoon", "horse", "rabbit"}, {"Horse", "OWL"}, 
Comparer.OrdinalIgnoreCase)
- ContainsAny({1, 2, 3, 4, 5}, {3, 9})
- ContainsAny({1, 2, 3, 4, 5}, {6, 7})
- Contents (optional mailboxAddress as nullable text)
- Contents(
        "https://www.bing.com",
        [
            RelativePath = "search",
            Query = [q = searchText]
        ]
    )
- Contents(
        url,
        [
            Headers = headers,
            Content = postData
        ]
    )
- Contents("https://contoso.com/api/customers/get", [ApiKeyName="api_key"])
- Contents(path as text, optional options as nullable record)
- Contents(table as table)
- Contents(url as text)
- Contents(url as text, optional options as nullable record)
- CorrelationId()
- Cosh(number as nullable number)
- Count([y])
- Count({1, 2, 3})
- Count({true, false})
- Count({})
- Covariance(numberList1 as list, numberList2 as list)
- Covariance({1, 2, 3}, {1, 2, 3})
- Csv (default)
- Cubes(
    server as text,
    systemNumberOrSystemId as text,
    clientId as text,
    optional optionsOrLogonGroup as any,
    optional options as nullable record
)
- Cubes(optional options as nullable record)
- Cubes(url as text, optional options as nullable record)
- Currency ("C")
- Data(optional loginUrl as any, optional options as nullable record)
- DataLake(endpoint as text, optional options as nullable record)
- DataLakeContents(url as text, optional options as nullable record)
- DataSource(
    providerName as text,
    connectionString as any,
    optional options as nullable record
)
- DataSource("dsn=your_dsn")
- DataSource(connectionString as any, optional options as nullable record)
- DataSourceProgress()
- Database(
    server as text,
    database as text,
    optional options as nullable record
)
- Database("SomeSQLServer", "MyDb")
- Database(database as binary, optional options as nullable record)
- Database(server as text, database as text, optional options as nullable 
record)
- Database(server as text, optional options as nullable record)
- Databases(server as text, optional options as nullable record)
- Date(#datetime(2010, 12, 31, 11, 56, 02)
- Date(dateTime as any)
- DateTimeZones(
    start as datetimezone,
    count as number,
    step as duration
)
- DateTimeZones(#datetimezone(2011, 12, 31, 23, 55, 0, -8, 0)
- DateTimes(
    start as datetime,
    count as number,
    step as duration
)
- DateTimes(#datetime(2011, 12, 31, 23, 55, 0)
- Dates(
    start as date,
    count as number,
    step as duration
)
- Dates(#date(2011, 12, 31)
- Day (#datetime(2011, 12,
31, 23, 55, 0)
- Day (#datetimezone(2011,
12, 31, 23, 55, 0, -8, 0)
- Day(#datetime(2011, 5, 14, 17, 0, 0)
- Day(dateTime as any)
- DayOfWeek(#date(2011, 02, 21)
- DayOfWeek(dateTime as any, optional firstDayOfWeek as nullable number)
- DayOfWeekName(#date(2011, 12, 31)
- DayOfWeekName(date as any, optional culture as nullable text)
- DayOfYear(#date(2011, 03, 01)
- DayOfYear(dateTime as any)
- Days(#date(2022, 3, 4)
- Days(<duration>)
- Days(duration as nullable duration)
- DaysInMonth(#date(2011, 12, 01)
- DaysInMonth(dateTime as any)
- Decimal("D")
- Decimal(binary as binary)
- Decompress(#binary({115, 103, 200, 7, 194, 20, 134, 36, 134, 74, 134, 84, 
6, 0})
- Decompress(binary as nullable binary, compressionType as number)
- Default()
- DemoteHeaders(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
    })
- Difference(
    list1 as list,
    list2 as list,
    optional equationCriteria as any
)
- Difference({1, 2, 3, 4, 5}, {4, 5, 3})
- Difference({1, 2}, {1, 2, 3})
- Dimensions(cube as table)
- DisplayFolders(cube as table)
- Displays (123)
- Displays (1234)
- Displays (8)
- Distinct(
        Source,
        {each _{0}, Comparer.OrdinalIgnoreCase}
    )
- Distinct(
        Table.SelectColumns(#"Cluster fuzzy match", "Cluster")
- Distinct(
        {"Squash", "Pumpkin", "ApPlE", "PEAR", "orange", "APPLE", "Pear", "peaR"},
        Comparer.OrdinalIgnoreCase
    )
- Distinct(
    Table.FromRecords({
        [a = "A", b = "a"],
        [a = "B", b = "a"],
        [a = "A", b = "b"]
    })
- Distinct(
    Table.FromRecords({
        [a = "A", b = "a"],
        [a = "B", b = "b"],
        [a = "A", b = "a"]
    })
- Distinct(List.Reverse(Source)
- Distinct(Source, Comparer.OrdinalIgnoreCase)
- Distinct(list as list, optional equationCriteria as any)
- Distinct(table as table, optional equationCriteria as any)
- Distinct({1, 1, 2, 3, 3, 3})
- Divide(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Document(
        File.Contents("C:\test-examples\JSON\Contosoware.json")
- Document(
        Web.Contents("htts://contoso.com/products/Contosoware.json")
- Document(Source)
- Document(contents as any, optional encoding as nullable number)
- Document(jsonText as any, optional encoding as nullable number)
- Document(response)
- Document(source as any, optional columns as any, optional delimiter as any, 
optional extraValues as nullable number, optional encoding as nullable number)
- Domains(optional forestRootDomainName as nullable text)
- Double (but may retain more
precision)
- Double(binary as binary)
- DuplicateColumn(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 3, b = 4]
    })
- DuplicateColumn(
    table as table,
    columnName as text,
    newColumnName as text,
    optional columnType as nullable type
)
- Durations(
    start as duration,
    count as number,
    step as duration
)
- Durations(#duration(0, 1, 0, 0)
- End("Hello, World", 5)
- End(text as nullable text, count as number)
- EndOfDay(#datetime(2011, 5, 14, 17, 0, 0)
- EndOfDay(#datetimezone(2011, 5, 17, 5, 0, 0, -7, 0)
- EndOfDay(dateTime as any)
- EndOfHour(#datetime(2011, 5, 14, 17, 0, 0)
- EndOfHour(#datetimezone(2011, 5, 17, 5, 0, 0, -7, 0)
- EndOfHour(dateTime as any)
- EndOfMonth(#date(2011, 5, 14)
- EndOfMonth(#datetimezone(2011, 5, 17, 5, 0, 0, -7, 0)
- EndOfMonth(dateTime as any)
- EndOfQuarter(#datetime(2011, 10, 10, 8, 0, 0)
- EndOfQuarter(dateTime as any)
- EndOfWeek(#date(2011, 5, 14)
- EndOfWeek(#datetimezone(2011, 5, 17, 5, 0, 0, -7, 0)
- EndOfWeek(dateTime as any, optional firstDayOfWeek as nullable number)
- EndOfYear(#datetime(2011, 5, 14, 17, 0, 0)
- EndOfYear(#datetimezone(2011, 5, 17, 5, 0, 0, -7, 0)
- EndOfYear(dateTime as any)
- EndsWith("Hello, World", "World")
- EndsWith("Hello, World", "world")
- EndsWith(text as nullable text, substring as text, optional comparer as 
nullable function)
- English (United States)
- Equals(
    comparer as function,
    x as any,
    y as any
)
- Equals(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Equals(Comparer.FromCulture("en-US")
- Equals(Comparer.Ordinal, "encyclopædia", "encyclopaedia")
- EscapeDataString("+money$")
- EscapeDataString(data as text)
- Evaluate("1 + 1")
- Evaluate("List.Sum({1, 2, 3})
- Evaluate(Expression.Constant("""abc")
- Evaluate(document as text, optional environment as nullable record)
- Eve (#date(2011, 12, 31)
- Exp(3)
- ExpandListColumn(
    #table(
        {"Part", "Components"},
        {
            {"Tool", #table({"Name", "Quantity"}, {{"Thingamajig", 2}, {"Widget", 
3}})
- ExpandListColumn(
    Table.FromRecords({[Name = {"Bob", "Jim", "Paul"}, Discount = .15]})
- ExpandRecordColumn(
    Table.FromRecords({
        [
            a = [aa = 1, bb = 2, cc = 3],
            b = 2
        ]
    })
- ExpandRecordColumn(
    table as table,
    column as text,
    fieldNames as list,
    optional newColumnNames as nullable list
)
- ExpandTableColumn(
    Table.FromRecords({
        [
            t = Table.FromRecords({
                [a = 1, b = 2, c = 3],
                [a = 2, b = 4, c = 6]
            })
- ExpandTableColumn(
    table as table,
    column as text,
    columnNames as list,
    optional newColumnNames as nullable list
)
- Exponential
("E")
- Exponential
(scientific)
- Expression(Value.Optimize(...)
- Expression(value as any)
- Facets(type as type)
- Factorial(10)
- Factorial(3)
- Factorial(5)
- Factorial(n - 1)
- Factorial(number as nullable number)
- Factorial(x - 1)
- Factorial2(x)
- Feed("https://services.odata.org/V4/TripPinService")
- Feed(serviceUri as text, optional headers as nullable record, optional 
options as any)
- Feed(url as text)
- Field([CustomerID = 1, Name = "Bob", Phone = "123-4567"], "CustomerID")
- FieldCount([ x = 1, y = 2 })
- FieldCount([CustomerID = 1, Name = "Bob"])
- FieldCount([])
- FieldCount(record as record)
- FieldNames([ x = 1, y = 2 ])
- FieldNames([ y = 1, x = 2 ])
- FieldNames([OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 
100.0])
- FieldOrDefault(
    record as nullable record,
    field as text,
    optional defaultValue as any
)
- FieldOrDefault([CustomerID = 1, Name = "Bob"], "Phone")
- FieldOrDefault([CustomerID = 1, Name = "Bob"], "Phone", "123-4567")
- FieldValues([CustomerID = 1, Name = "Bob", Phone = "123-4567"])
- Files("C:\test-examples\example-folder")
- Files(account as text, containerName as text)
- Files(path as text, optional options as nullable record)
- Files(url as text)
- Files(url as text, optional options as nullable record)
- FillDown(
    Table.FromRecords({
        [Place = 1, Name = "Bob"],
        [Place = null, Name = "John"],
        [Place = 2, Name = "Brad"],
        [Place = 3, Name = "Mark"],
        [Place = null, Name = "Tom"],
        [Place = null, Name = "Adam"]
    })
- FillUp(
    Table.FromRecords({
        [Column1 = 1, Column2 = 2],
        [Column1 = 3, Column2 = null],
        [Column1 = 5, Column2 = 3]
    })
- FilterWithDataTable(table as table, dataTableIdentifier as text)
- FindText(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- FindText(table as table, text as text)
- FindText({"a", "b", "ab"}, "a")
- Firewall(key as text)
- First(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- First(GreaterThan5)
- First(Table.FromRecords({})
- First(list as list, optional defaultValue as any)
- First(table as table, optional default as any)
- First({1, 2, 3})
- First({}, -1)
- FirstGreaterThan5({1,3,4})
- FirstGreaterThan5({3,7,9})
- FirstN(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- FirstN(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 3, b = 4],
        [a = -5, b = -6]
    })
- FirstN(list as list, countOrCondition as any)
- FirstN(table as table, countOrCondition as any)
- FirstN({3, 4, 5, -1, 7, 8, 2}, each _ > 0)
- FirstValue(table as table, optional default as any)
- ForFunction([ReturnType = type number, Parameters = [X = type number]], 1)
- ForFunction(signature as record, min as number)
- ForRecord(Record.FromList(rowColumnTypes, columnNames)
- Format(
        "Duration = #{0} days, #{1} hours, #{2} minutes, and #{3} seconds.",
        {
            Duration.Days(Source)
- Format(
        "Round-tripped #{0} Local to #{1} Local.", 
        {
            DateTimeZone.ToText(#"Origin Local Date")
- Format(
        "Round-tripped #{0} UTC to #{1} UTC.", 
        {
            DateTimeZone.ToText(#"Origin UTC Date")
- Format(
        "Round-tripped #{0} to #{1}.", 
Back to table
The "R" or "r" standard format specifier represents a custom date and time format string
that's not defined by a specific culture. It is always the same, regardless of the culture
used or the format provider supplied. The custom format string is "ddd, dd MMM yyyy
HH':'mm':'ss 'GMT'". When this standard format specifier is used, the formatting or
parsing operation always uses the invariant culture.
Although the RFC 1123 standard expresses a time as Coordinated Universal Time (UTC)
- Format(
    "The time for the #[distance] km run held in #[city] on #[date] was #
[duration].",
Output
"The time for the 10 km run held in Seattle on 3/10/2015 was 00:54:40."
How culture affects text formatting
    [
        city = "Seattle",
        date = #date(2015, 3, 10)
- Format(
    formatString as text,
    arguments as any,
    optional culture as nullable text
)
- Format("    Beginning Balance           Ending Balance#
(cr,lf)
- Format("#{0} (#{1})
- Format("#{0} (Local)
- Format("#{0} (Unspecified)
- Format("#{0} (Utc)
- Format("#{0}", { Date.FromText("24-Jan-49", [Format = 
fmt])
- Format("#{0}", { Date.FromText("24-Jan-50", [Format = 
fmt])
- Format("#{0}, #{1}, and #{2}.", {17, 7, 22})
- Format("'#{0}'", {DateTime.ToText(DateTime.LocalNow()
- Format("'#{0}'", {DateTime.ToText(date, [Format = " h"])
- Format("'#{0}'", {DateTime.ToText(date, [Format = "%h"])
- Format("'#{0}'", {DateTime.ToText(date, [Format = "h "])
- Format("C: #{0}", {Number.ToText(floating, "C", culture)
- Format("C: #{0}", {Number.ToText(integral, "C", culture)
- Format("Converted '#{0}' to #{1}.", {dateValue, 
DateTime.FromText(dateValue, [Format=pattern])
- Format("D: #{0}", {Number.ToText(integral, "D6", culture)
- Format("E: #{0}", {Number.ToText(floating, "E03", culture)
- Format("E: #{0}", {Number.ToText(integral, "E03", culture)
- Format("F: #{0}", {Number.ToText(floating, "F04", culture)
- Format("F: #{0}", {Number.ToText(integral, "F01", culture)
- Format("G: #{0}", {Number.ToText(floating, "G", culture)
- Format("G: #{0}", {Number.ToText(integral, "G", culture)
- Format("N: #{0}", {Number.ToText(floating, "N03", culture)
- Format("N: #{0}", {Number.ToText(integral, "N01", culture)
- Format("P: #{0}", {Number.ToText(floating/10000, "P02", 
culture)
- Format("P: #{0}", {Number.ToText(integral/10000, "P02", 
culture)
- Format("The current date and time: #{0}", {DateTimeZone.ToText(
            #datetimezone(2011, 6, 10, 15, 24, 16, 0, 0)
- Format("The value is: '#{0}'", 
{Text.PadStart(Number.ToText(.324, "#.###")
- Format("Unable to convert '#{0}' to a date and 
time.", {dateValue})
- Format("X: 0x#{0}", {Number.ToText(integral, "X", culture)
- From(
    longitude as number,
    latitude as number,
    optional z as nullable number,
    optional m as nullable number,
    optional srid as nullable number
)
- From(
    value as any,
    optional culture as nullable text,
    optional roundingMode as nullable number
)
- From(
    x as number,
    y as number,
    optional z as nullable number,
    optional m as nullable number,
    optional srid as nullable number
)
- From("(05FE1DAD-C8C2-4F3B-A4C2-D194116B4967)
- From("05FE1DAD-C8C2-4F3B-A4C2-D194116B4967")
- From("05FE1DADC8C24F3BA4C2D194116B4967")
- From("1.23455")
- From("1.23455", "en-US", RoundingMode.Down)
- From("1.5")
- From("1011")
- From("12.3%")
- From("2.05:55:20.242")
- From("2.05:55:20.34567")
- From("2020-10-30T01:30:00-08:00")
- From("4")
- From("4.5")
- From("4.5", null, RoundingMode.AwayFromZero)
- From("Jan 11, 2021")
- From("Today is " & Date.ToText(#date(2011, 6, 10)
- From("{05FE1DAD-C8C2-4F3B-A4C2-D194116B4967}")
- From(#date(1975, 4, 4)
- From(#date(2025, 7, 23)
- From(#datetime(1899, 12, 30, 06, 45, 12)
- From(#datetime(2020, 3, 20, 6, 0, 0)
- From(#datetime(2024, 6, 24, 14, 32, 22)
- From(#time(06, 45, 12)
- From(0.7575)
- From(1.5)
- From(10761.937554)
- From(2)
- From(2.525)
- From(3)
- From(43910)
- From(8395)
- From(Binary.FromText("10FF", BinaryEncoding.Hex)
- From(_ + 1)
- From(_, "fr-FR")
- From(each [CustomerName] = "ALFKI")
- From(each _ <> null)
- From(function as function)
- From(functionType as type, function as function)
- From(identityProvider as function, value as any)
- From(type function (a as number, b as number)
- From(type function (a as text, b as text)
- From(value as any, optional culture as nullable text)
- From(value as any, optional culture as nullable text, optional roundingMode 
as nullable number)
- From(value as any, optional encoding as nullable number)
- From(value as nullable text)
- From(value as text)
- From(value)
- FromBinary(
    binary as binary,
    optional quoteStyle as any,
    optional includeLineSeparators as nullable logical,
    optional encoding as nullable number
)
- FromBinary(Json.FromValue([A = {1, true, "3"}, B = #date(2012, 3, 25)
- FromBinary(binary as nullable binary, optional encoding as nullable number)
- FromBinary(stream as binary)
- FromColumns(
    {
        {1, "Bob", "123-4567"},
        {2, "Jim", "987-6543"},
        {3, "Paul", "543-7890"}
    },
    {"CustomerID", "Name", "Phone"}
)
- FromColumns(
    {
        {1, 2, 3},
        {4, 5},
        {6, 7, 8, 9}
    },
    {"column1", "column2", "column3"}
)
- FromColumns(lists as list, optional columns as any)
- FromColumns({
    {1, "Bob", "123-4567"},
    {2, "Jim", "987-6543"},
    {3, "Paul", "543-7890"}
})
- FromCulture("en-US")
- FromCulture(culture as text, optional ignoreCase as nullable logical)
- FromFileTime(129876402529842245)
- FromFileTime(fileTime as nullable number)
- FromList(
        {1..5},
        each {
            _,
            Function.InvokeAfter(()
- FromList(
    list as list,
    optional splitter as nullable function,
    optional columns as any,
    optional default as any,
    optional extraValues as nullable number
)
- FromList(
    {
        [CustomerID = 1, Name = "Bob"],
        [CustomerID = 2, Name = "Jim"]
    },
    Record.FieldValues,
    {"CustomerID", "Name"}
)
- FromList(
    {"a,apple", "b,ball", "c,cookie", "d,door"},
    Splitter.SplitByNothing()
- FromList(
    {"a,apple", "b,ball", "c,cookie", "d,door"},
    null,
    {"Letter", "Example Word"}
)
- FromList(
The output of this example is:
If you look at the output, you might notice that even though the DateTime.LocalNow  function
appears first in the code, the value returned for DateTime.FixedLocalNow  shows a time that
occurs before the DateTime.LocalTime  time. Even though DateTime.LocalNow  is listed first in the
table construction, the order of evaluation in Power Query M isn't guaranteed to follow the
order of fields in a table. Instead, Power Query uses a lazy evaluation model. Using this model
means that fields are only evaluated when needed and the engine determines the evaluation
order, not the order in your code. In this case, the DateTime.FixedLocalNow  function is
evaluated first, so the first time returned for this function occurs before the first time returned
for DateTime.LocalNow .
        {1..5},
        each {
            _,
            Function.InvokeAfter(()
- FromList(list as list)
- FromList(list as list, fields as any)
- FromList({1, "Bob", "123-4567"}, type [CustomerID = number, Name = text, 
Phone = number])
- FromList({1, "Bob", "123-4567"}, {"CustomerID", "Name", "Phone"})
- FromList({1, 2}, {"a", "b"})
- FromNumber(0x1F600)
- FromNumber(9)
- FromNumber(Character.ToNumber("A")
- FromNumber(number as nullable number)
- FromPartitions(
                            "Day",
                            {
                                {3, #table({"Foo"}, {{"Bar"}})
- FromPartitions(
    "Year",
    {
        {
            1994,
            Table.FromPartitions(
                "Month",
                {
                    {
                        "Jan",
                        Table.FromPartitions(
                            "Day",
                            {
                                {1, #table({"Foo"}, {{"Bar"}})
- FromPartitions(
    partitionColumn as text,
    partitions as list,
    optional partitionColumnType as nullable type
)
- FromRecords(
        {
            [CustomerStateID = 1, FirstName2 = "Bob", State = "TX"],
            [CustomerStateID = 2, FirstName2 = "bOB", State = "CA"]
        },
Output
Power Query M
How culture affects text formatting
        type table [CustomerStateID = nullable number, FirstName2 = nullable text, 
State = nullable text]
    )
- FromRecords(
        {
Output
Power Query M
How culture affects text formatting
            [CustomerStateID = 1, FirstName2 = "Bob", State = "TX"],
            [CustomerStateID = 2, FirstName2 = "bOB", State = "CA"]
        },
        type table [CustomerStateID = nullable number, FirstName2 = nullable text, 
State = nullable text]
    )
- FromRecords(
    records as list,
    optional columns as any,
    optional missingField as nullable number
)
- FromRecords(
    {
        [CustomerID = 1, total = 30],
        [CustomerID = 2, total = 30],
        [CustomerID = 3, total = 25]
    },
    {"CustomerID", "total"}
)
- FromRecords(
    {
        [EmployeeID = 1, Location = "Seattle", Location_Cleaned = "Seattle"],
        [EmployeeID = 2, Location = "seattl", Location_Cleaned = "Seattle"],
        [EmployeeID = 3, Location = "Vancouver", Location_Cleaned = "Vancouver"],
        [EmployeeID = 4, Location = "Seatle", Location_Cleaned = "Seattle"],
        [EmployeeID = 5, Location = "vancover", Location_Cleaned = "Vancouver"],
        [EmployeeID = 6, Location = "Seattle", Location_Cleaned = "Seattle"],
        [EmployeeID = 7, Location = "Vancouver", Location_Cleaned = "Vancouver"]
    },
    type table [EmployeeID = nullable number, Location = nullable text, 
Location_Cleaned = nullable text]
)
- FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
    })
- FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Cristina", Phone = "232-1550"],
        [CustomerID = 5, Name = "Anita", Phone = "530-1459"]
    })
- FromRecords({
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Cristina", Phone = "232-1550"]
    })
- FromRecords({
        [CustomerID = 5, Name = "Anita", Phone = "530-1459"]
    })
- FromRecords({
        [First Name = "Doug", Middle Initial = "J", Last Name = "Elis"],
        [First Name = "Anna", Middle Initial = "M", Last Name = "Jorayew"],
        [First Name = "Rada", Middle Initial = null, Last Name = "Mihaylova"]
    })
- FromRecords({
        [Id = 1, Name = "Hello There"],
        [Id = 2, Name = "Good Bye"]
    })
- FromRecords({
        [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0],
        [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0],
        [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25.0],
        [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200.0],
        [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2.0],
        [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20.0],
        [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25]
    })
- FromRecords({
        [OrderID = 1, CustomerID = 1, Item = "fishing rod", Price = 100.0],
          [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0],
          [OrderID = 3, CustomerID = 2, Item = "fishing net", Price = 
25.0]})
- FromRecords({
        [TenantID = 1, CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [TenantID = 1, CustomerID = 2, Name = "Jim", Phone = "987-6543"]
    })
- FromRecords({
        [TenantID = 1, OrderID = 1, CustomerID = 1, Name = "Fishing rod", Price = 
100.0],
        [TenantID = 1, OrderID = 2, CustomerID = 1, Name = "1 lb. worms", Price = 
5.0],
        [TenantID = 1, OrderID = 3, CustomerID = 2, Name = "Fishing net", Price = 
25.0]
    })
- FromRecords({
        [a = 1, b = 4],
        [a = 1, b = 4]
    })
- FromRecords({
        [a = 2, b = 4],
        [a = 2, b = 4]
    })
- FromRecords({
        [saleID = 1, price = 20, stock = 1234],
        [saleID = 2, price = 10, stock = 5643]
    })
- FromRecords({
    [
        CustomerID = 1,
        FirstName1 = "Bob",
        Phone = "555-1234",
        CustomerStateID = 1,
        FirstName2 = "Bob",
        State = "TX"
    ],
    [
        CustomerID = 1,
        FirstName1 = "Bob",
        Phone = "555-1234",
        CustomerStateID = 2,
        FirstName2 = "bOB",
        State = "CA"
    ],
    [
        CustomerID = 2,
        FirstName1 = "Robert",
        Phone = "555-4567",
        CustomerStateID = null,
        FirstName2 = null,
        State = null
    ]
})
- FromRecords({
    [
        CustomerID = 1,
        FirstName1 = "Bob",
        Phone = "555-1234",
        NestedTable = Table.FromRecords({
            [
                CustomerStateID = 1,
                FirstName2 = "Bob",
                State = "TX"
            ],
            [
                CustomerStateID = 2,
                FirstName2 = "bOB",
                State = "CA"
            ]
        })
- FromRecords({
    [
        Foo = "Bar",
        Day = 1,
        Month = "Jan",
        Year = 1994
    ],
    [
        Foo = "Bar",
        Day = 2,
        Month = "Jan",
        Year = 1994
    ],
    [
        Foo = "Bar",
        Day = 3,
        Month = "Feb",
        Year = 1994
    ],
    [
        Foo = "Bar",
        Day = 4,
        Month = "Feb",
        Year = 1994
    ]
})
- FromRecords({
    [
        saleID = 1,
        item = "Shirt",
        price = Table.FromRecords({[saleID = 1, price = 20, stock = 1234]})
- FromRecords({
    [#"Letter and Example Word" = "a,apple"],
    [#"Letter and Example Word" = "b,ball"],
    [#"Letter and Example Word" = "c,cookie"],
    [#"Letter and Example Word" = "d,door"]
})
- FromRecords({
    [A = "1", B = 2, X = null],
    [A = "5", B = 10, X = null]
})
- FromRecords({
    [A = "1", B = 2],
    [A = "5", B = 10]
})
- FromRecords({
    [A = "hello", B = "world"],
    [A = 1, B = 2]
})
- FromRecords({
    [A = 1, B = "2"],
    [A = 5, B = "10"]
})
- FromRecords({
    [A = 1, B = "3"],
    [A = 5, B = "11"]
})
- FromRecords({
    [A = 1, B = "hello"],
    [A = 2, B = "world"]
})
- FromRecords({
    [A = 1, B = "hello"],
    [A = 3, B = "world"]
})
- FromRecords({
    [A = 1, B = "hello"],
Replace the text "ur" with "or" in column B, matching any part of the value.
Usage
Power Query M
Output
Power Query M
Anonymize the names of US employees.
Usage
Power Query M
    [A = 2, B = "world"],
    [A = 3, B = "goodbyes"]
})
- FromRecords({
    [Column1 = "CustomerID", Column2 = "Name", Column3 = "Phone"],
    [Column1 = 1, Column2 = "Bob", Column3 = "123-4567"],
    [Column1 = 2, Column2 = "Jim", Column3 = "987-6543"]
})
- FromRecords({
    [Column1 = "Full Name", Column2 = "Age", Column3 = "Country"],
    [Column1 = "Fred", Column2 = 42, Column3 = "UK"]
})
- FromRecords({
    [Column1 = "ID", Column2 = "Name", Column3 = "Phone"],
    [Column1 = 1, Column2 = "Bob", Column3 = "123-4567"],
    [Column1 = 3, Column2 = "Pam", Column3 = "543-7890"],
    [Column1 = 2, Column2 = "Jim", Column3 = "987-6543"]
})
- FromRecords({
    [Column1 = 1, Column2 = 2, Column3 = 3],
    [Column1 = "Bob", Column2 = "Jim", Column3 = "Paul"],
    [Column1 = "123-4567", Column2 = "987-6543", Column3 = "543-7890"]
})
- FromRecords({
    [Column1 = 1, Column2 = 2],
    [Column1 = 3, Column2 = 3],
    [Column1 = 5, Column2 = 3]
})
- FromRecords({
    [Column1 = 1],
    [Column1 = 6],
    [Column1 = 7],
    [Column1 = 5]
})
- FromRecords({
    [Column1 = 2],
    [Column1 = 3]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567", Index = 0],
Add an index column named "index", starting at value 10 and incrementing by 5, to the table.
Usage
Power Query M
Output
Power Query M
Types and type conversion
    [CustomerID = 2, Name = "Jim", Phone = "987-6543", Index = 1],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890", Index = 2],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550", Index = 3]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567", Index = 10],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543", Index = 15],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890", Index = 20],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550", Index = 25]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567", OrderID = 1, Item = 
"Fishing rod", Price = 100],
    [CustomerID = 1, Name = "Bob", Phone = "123-4567", OrderID = 2, Item = "1 lb. 
worms", Price = 5],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543", OrderID = 3, Item = 
"Fishing net", Price = 25],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890", OrderID = 4, Item = "Fish 
tazer", Price = 200],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890", OrderID = 5, Item = 
"Bandaids", Price = 2],
    [CustomerID = 1, Name = "Bob", Phone = "123-4567", OrderID = 6, Item = "Tackle 
box", Price = 20]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
Remove the last rows where [CustomerID] > 2 of the table.
Usage
Power Query M
Output
Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- FromRecords({
    [CustomerID = 1, Name = "Bob", Revenue = 200, RevenueRank = 1],
    [CustomerID = 3, Name = "Paul", Revenue = 200, RevenueRank = 1],
    [CustomerID = 2, Name = "Jim", Revenue = 100, RevenueRank = 3],
    [CustomerID = 4, Name = "Ringo", Revenue = 50, RevenueRank = 4]
})
- FromRecords({
    [CustomerID = 1, Name = "Bob"],
    [CustomerID = 2, Name = "Jim"]
})
- FromRecords({
    [CustomerID = 1, Name = 2, Phone = 3],
    [CustomerID = "Bob", Name = "Jim", Phone = "Paul"],
    [CustomerID = "123-4567", Name = "987-6543", Phone = "543-7890"]
})
- FromRecords({
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
})
- FromRecords({
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
})
- FromRecords({
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
Remove the row at position 1 from the table.
Usage
Power Query M
Output
Power Query M
Remove two rows starting at position 1 from the table.
Usage
Power Query M
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
})
- FromRecords({
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
Return one row starting at offset 1 in the table.
Usage
Power Query M
Output
Table.FromRecords({[CustomerID = 2, Name = "Jim", Phone = "987-6543"]})
- FromRecords({
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
})
- FromRecords({
    [CustomerID = 4, Name = "Ringo", Phone = "232-1550"],
    [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
    [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
    [CustomerID = 1, Name = "Bob", Phone = "123-4567"]
})
- FromRecords({
    [CustomerID = null, Name = "Bob"],
    [CustomerID = null, Name = null],
    [CustomerID = null, Name = null]
})
- FromRecords({
    [CustomerToCall = 1, CustomerDetails = Table.FromRecords({[CustomerID = 1, 
Name = "Bob", Phone = "123-4567"]})
- FromRecords({
    [First Name = "Doug", Middle Initial = "J", Last Name = "Elis", Full Name = 
"Doug J Elis"],
    [First Name = "Anna", Middle Initial = "M", Last Name = "Jorayew", Full Name = 
"Anna M Jorayew"],
    [First Name = "Rada", Middle Initial = null, Last Name = "Mihaylova", Full 
Name = "Rada Mihaylova"]
})
- FromRecords({
    [Id = 1, Name = "Hello There"],
    [Id = 2, Name = "Good Bye"]
})
- FromRecords({
    [Letter = "a", #"Example Word" = "apple"],
    [Letter = "b", #"Example Word" = "ball"],
    [Letter = "c", #"Example Word" = "cookie"],
Create a table from a list using a custom splitter.
Usage
Power Query M
Output
Power Query M
Create a table from the list using the Record.FieldValues splitter.
Usage
Power Query M
    [Letter = "d", #"Example Word" = "door"]
})
- FromRecords({
    [Location = "Seattle", Count = 4],
    [Location = "Vancouver", Count = 3]
})
- FromRecords({
    [Name = "*****", Country = "US"],
    [Name = "Bob", Country = "CA"]
})
- FromRecords({
    [Name = "?????", Country = "??"],
    [Name = "Bob", Country = "CA"]
})
- FromRecords({
    [Name = "Bob", Discount = 0.15],
    [Name = "Jim", Discount = 0.15],
    [Name = "Paul", Discount = 0.15]
})
- FromRecords({
    [Name = "Bob", Phone = "123-4567", Fax = null, Cell = null],
    [Name = null, Phone = "838-7171", Fax = "987-6543", Cell = null],
    [Name = null, Phone = null, Fax = null, Cell = "543-7890"]
})
- FromRecords({
    [Name = "Bob"],
    [Name = "Jim"],
    [Name = "Paul"],
    [Name = "Ringo"]
})
- FromRecords({
    [Name = "OrderID", Value = 1],
    [Name = "CustomerID", Value = 1],
    [Name = "Item", Value = "Fishing rod"],
    [Name = "Price", Value = 100]
})
- FromRecords({
    [OrderID = "1", Color = "Red"],
    [OrderID = "2", Color = "Blue"]
})
- FromRecords({
    [OrderID = "1", Item = "Fishing rod"],
    [OrderID = "2", Item = "1 lb. worms"]
})
- FromRecords({
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100, Shipping = 
10, TotalPrice = 110],
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5, Shipping = 15, 
TotalPrice = 20],
    [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25, Shipping = 10, 
TotalPrice = 35]
})
- FromRecords({
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100],
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5],
    [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25],
Sort the table on column "OrderID" in descending order.
Usage
Power Query M
Output
Power Query M
    [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200],
    [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2],
    [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20],
    [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
    [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100],
    [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25]
})
- FromRecords({
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100],
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5],
    [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20],
    [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25],
    [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200],
    [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2],
    [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
    [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100],
    [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25]
})
- FromRecords({
    [OrderID = 1, CustomerID = 1, Item = "fishing rod", Price = 100.0],
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0],
    [OrderID = 3, CustomerID = 2, Item = "fishing net", Price = 25.0]})
- FromRecords({
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5],
    [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25],
    [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200],
    [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2],
    [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20],
    [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
    [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100],
    [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25]
})
- FromRecords({
    [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25],
    [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100],
    [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
    [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20],
    [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2],
    [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200],
    [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25],
    [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5],
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100]
})
- FromRecords({
    [Part = "Tool", Components = [Name = "Thingamajig", Quantity = 2]],
    [Part = "Tool", Components = [Name = "Widget", Quantity = 3]]
})
- FromRecords({
    [Place = 1, Name = "Bob"],
    [Place = 1, Name = "John"],
    [Place = 2, Name = "Brad"],
    [Place = 3, Name = "Mark"],
    [Place = 3, Name = "Tom"],
    [Place = 3, Name = "Adam"]
})
- FromRecords({
    [TenantID = 1, CustomerID = 1, Name = "Bob", Phone = "123-4567", 
Order.TenantID = 1, Order.OrderID = 1, Order.CustomerID = 1, Order.Name = "Fishing 
rod", Order.Price = 100],
    [TenantID = 1, CustomerID = 1, Name = "Bob", Phone = "123-4567", 
Order.TenantID = 1, Order.OrderID = 2, Order.CustomerID = 1, Order.Name = "1 lb. 
worms", Order.Price = 5],
    [TenantID = 1, CustomerID = 2, Name = "Jim", Phone = "987-6543", 
Order.TenantID = 1, Order.OrderID = 3, Order.CustomerID = 2, Order.Name = "Fishing 
net", Order.Price = 25]
})
- FromRecords({
    [Value = 1],
    [Value = "Bob"],
    [Value = "123-4567"]
})
- FromRecords({
    [a = "A", b = "a"],
    [a = "A", b = "b"]
})
- FromRecords({
    [a = "A", b = "a"],
    [a = "B", b = "b"]
})
- FromRecords({
    [a = -1, b = -2],
    [a = -2, b = -3],
    [a = 3, b = 4],
    [a = -1, b = -2]
})
- FromRecords({
    [a = 0, b = 0],
    [a = 2, b = 4]
})
- FromRecords({
    [a = 1, b = "hello"],
    [a = 3, b = "world"],
    [a = 1, b = "hello"],
    [a = 3, b = "world"]
})
- FromRecords({
    [a = 1, b = 2, #"copied column" = 1],
Types and type conversion
    [a = 3, b = 4, #"copied column" = 3]
})
- FromRecords({
    [a = 1, b = 2],
    [a = 3, b = 4]
})
- FromRecords({
    [a = 3, b = 4],
    [a = 5, b = 6]
})
- FromRecords({
    [a = 6, b = 2],
    [a = 2, b = 4]
})
- FromRecords({
    [column1 = 1, column2 = 4, column3 = 6],
    [column1 = 2, column2 = 5, column3 = 7],
    [column1 = 3, column2 = null, column3 = 8],
    [column1 = null, column2 = null, column3 = 9]
})
- FromRecords({
    [key = "key1", column1 = "attribute1", column2 = 1],
    [key = "key1", column1 = "attribute2", column2 = 2],
    [key = "key1", column1 = "attribute3", column2 = 3],
    [key = "key2", column1 = "attribute1", column2 = 4],
    [key = "key2", column1 = "attribute2", column2 = 5],
    [key = "key2", column1 = "attribute3", column2 = 6]
})
- FromRecords({
    [key = "x", a = 1, b = null, c = 3],
Take the values "a", "b", and "c" in the attribute column of table ({ [ key = "x", attribute =
"a", value = 1 ], [ key = "x", attribute = "c", value = 3 ], [ key = "x", attribute =
"c", value = 5 ], [ key = "y", attribute = "a", value = 2 ], [ key = "y", attribute =
"b", value = 4 ] })
- FromRecords({
    [key = "x", a = 1, b = null, c = 5],
    [key = "y", a = 2, b = 4, c = null]
})
- FromRecords({
    [key = "x", attribute = "a", value = 1],
    [key = "x", attribute = "c", value = 3],
    [key = "y", attribute = "a", value = 2],
    [key = "y", attribute = "b", value = 4]
})
- FromRecords({
    [t.a = 1, t.b = 2, t.c = 3, b = 2],
    [t.a = 2, t.b = 4, t.c = 6, b = 2]
})
- FromRecords({
Output
Power Query M
Join kind
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- FromRecords({[#"sum of t.a" = 3, #"min of t.b" = 2, #"max of t.b" = 4, #"count of
t.a" = 2, b = 2]})
- FromRecords({[1 = 1, Name = "Bob", #"1/1/1980" = #date(1980, 1, 1)
- FromRecords({[Cell = "543-7890"]})
- FromRecords({[Column = 1, cOlum1 = 2, coLum2 = 3]})
- FromRecords({[Column = 1]})
- FromRecords({[CustomerID = 1, Name = "Bob", Column3 = #date(1980, 1, 1)
- FromRecords({[CustomerID = 1, Name = "Bob", Phone = 
"123-4567"]})
- FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- FromRecords({[CustomerID = 1, Name = "Bob"]})
- FromRecords({[CustomerID = 1, NewColumn = null]})
- FromRecords({[CustomerID = 2, Name = "Jim", Phone = "987-6543"]})
- FromRecords({[CustomerID = 3, 
Name = "Paul", Phone = "543-7890"]})
- FromRecords({[CustomerID = 3, Name = "Paul", Phone = "543-7890"]})
- FromRecords({[Fax = "987-6543", Phone = "838-7171"]})
- FromRecords({[FullName = "Smith,Bob"]})
- FromRecords({[MyTable.CustomerID = 1, MyTable.Name = "Bob", MyTable.Phone = "123-
4567"]})
- FromRecords({[MyValue = 1]})
- FromRecords({[Name = "CustomerID", Value =
1], [Name = "Name", Value = "Bob"], [Name = "Phone", Value = "123-4567"]})
- FromRecords({[Value = 1]})
- FromRecords({[a = 3, b = 4]})
- FromRecords({[aa = 1, bb = 2, cc = 3, b = 2]})
- FromRecords({[saleID = 2, price = 10, stock = 5643]})
- FromRecords({})
- FromRows(
    {
        {1, "Bob", "123-4567"},
        {2, "Jim", "987-6543"}
    },
    type table [CustomerID = number, Name = text, Phone = text]
)
- FromRows(
    {
        {1, "Bob", "123-4567"},
        {2, "Jim", "987-6543"}
    },
    {"CustomerID", "Name", "Phone"}
)
- FromRows(DistinctByCountry, {"Country", "Date", "Value"})
- FromTable(
    Table.FromRecords({
        [Name = "CustomerID", Value = 1],
        [Name = "Name", Value = "Bob"],
        [Name = "Phone", Value = "123-4567"]
    })
- FromText("10")
- FromText("1011")
- FromText("1011", BinaryEncoding.Base64)
- FromText("1011", BinaryEncoding.Hex)
- FromText("1012")
- FromText("10:12:31am")
- FromText("12345.6789")
- FromText("1400", [Format="yyyy", Culture="ar-SA"])
- FromText("2.05:55:20")
- FromText("2000-02-08T03:45:12Z", [Format="yyyy-MM-dd'T'HH:mm:ss'Z'", 
Culture="en-US"])
- FromText("2009-06-15T13:45:30.0000000-07:00", [Format="O", 
Culture="en-US"])
- FromText("2010-12-31")
- FromText("2010-12-31T01:30:00-08:00")
- FromText("2010-12-31T01:30:25")
- FromText("20101231T013000", [Format="yyyyMMdd'T'HHmmss", Culture="en-
US"])
- FromText("24 Dez 2024 14:33:20", "de-DE")
- FromText("25.4%")
- FromText("30 Dez 2010 02:04:50.369730 +02:00", [Format="dd MMM yyyy 
HH:mm:ss.ffffff zzz", Culture="de-DE"])
- FromText("30 Dez 2010 02:04:50.369730", [Format="dd MMM yyyy 
HH:mm:ss.ffffff", Culture="de-DE"])
- FromText("30 Dez 2010", [Format="dd MMM yyyy", Culture="de-DE"])
- FromText("4")
- FromText("5.0e-10")
- FromText("EBE=", BinaryEncoding.Base64)
- FromText("a")
- FromText("true")
- FromText("€1,190", "fr-FR")
- FromText(#"Local Date Text")
- FromText(#"Offset Date Text")
- FromText(#"UTC Date Text")
- FromText(text as any, optional culture as nullable text)
- FromText(text as nullable text)
- FromText(text as nullable text, optional culture as nullable text)
- FromText(text as nullable text, optional encoding as nullable number)
- FromText(text as nullable text, optional options as any)
- FromText(text as text, optional quoteStyle as any, optional 
includeLineSeparators as nullable logical)
- FromValue(1)
- FromValue(1, [DefaultColumnName = "MyValue"])
- FromValue([x = 235.7, y = 41.53])
- FromValue(value as any, optional encoding as nullable number)
- FromValue(value as any, optional options as nullable record)
- FromValue({1, "Bob", "123-4567"})
- FromWellKnownText(input as nullable text)
- Function
(x)
- FunctionParameters(
        type function (x as number, optional y as text)
- FunctionParameters(type as type)
- FunctionParameters(type function (x as number, y as text)
- FunctionRequiredParameters(
        type function (x as number, optional y as text)
- FunctionRequiredParameters(type as type)
- FunctionRequiredParameters(type function (x as number, optional y as text)
- FunctionReturn(
        type function (x as number, optional y as text)
- FunctionReturn(type as type)
- FunctionReturn(type function ()
- Functions
(x)
- FuzzyGroup(
    Table.FromRecords(
        {
            [EmployeeID = 1, Location = "Seattle"],
            [EmployeeID = 2, Location = "seattl"],
            [EmployeeID = 3, Location = "Vancouver"],
            [EmployeeID = 4, Location = "Seatle"],
            [EmployeeID = 5, Location = "vancover"],
            [EmployeeID = 6, Location = "Seattle"],
            [EmployeeID = 7, Location = "Vancouver"]
        },
        type table [EmployeeID = nullable number, Location = nullable text]
    )
- FuzzyGroup(table as table, key as any, aggregatedColumns as list, optional 
options as nullable record)
- FuzzyJoin(
    Table.FromRecords(
        {
            [CustomerID = 1, FirstName1 = "Bob", Phone = "555-1234"],
            [CustomerID = 2, FirstName1 = "Robert", Phone = "555-4567"]
        },
        type table [CustomerID = nullable number, FirstName1 = nullable text, 
Phone = nullable text]
    )
- FuzzyJoin(table1 as table, key1 as any, table2 as table, key2 as any, 
optional joinKind as nullable number, optional joinOptions as nullable record)
- FuzzyNestedJoin(
    Table.FromRecords(
        {
            [CustomerID = 1, FirstName1 = "Bob", Phone = "555-1234"],
            [CustomerID = 2, FirstName1 = "Robert", Phone = "555-4567"]
        },
        type table [CustomerID = nullable number, FirstName1 = nullable text, 
Phone = nullable text]
    )
- FuzzyNestedJoin(table1 as table, key1 as any, table2 as table, key2 as any, 
newColumnName as text, optional joinKind as nullable number, optional joinOptions 
as nullable record)
- GET (when no Content is specified)
- General ("G")
- Generate(
    ()
- Generate(initial as function, condition as function, next as function, 
optional selector as nullable function)
- GetRelationships(tables as table, optional dataColumn as nullable text)
- Group(
        BinaryFormat.Byte,
        {
            {1, BinaryFormat.Byte, BinaryOccurrence.Repeating,
              0, (list)
- Group(
        BinaryFormat.Byte,
        {
            {1, BinaryFormat.Byte, BinaryOccurrence.Required},
            {2, BinaryFormat.Byte, BinaryOccurrence.Repeating},
            {3, BinaryFormat.Byte, BinaryOccurrence.Optional},
            {4, BinaryFormat.Byte, BinaryOccurrence.Repeating}
        },
        (extra)
- Group(
    Table.FromRecords({
        [CustomerID = 1, price = 20],
        [CustomerID = 2, price = 10],
        [CustomerID = 2, price = 20],
        [CustomerID = 1, price = 10],
        [CustomerID = 3, price = 20],
        [CustomerID = 3, price = 5]
    })
- Group(
    binaryFormat as function,
    group as list,
    optional extra as nullable function,
    optional lastKey as any
)
- Group(table as table, key as any, aggregatedColumns as list, optional 
groupKind as nullable number, optional comparer as nullable function)
- HasColumns(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- HasColumns(table as table, columns as any)
- HasFields([CustomerID = 1, Name = "Bob", Phone = "123-4567"], 
{"CustomerID", "Address"})
- HasFields([CustomerID = 1, Name = "Bob", Phone = "123-4567"], "CustomerID")
- HasFields(record as record, fields as any)
- Headers(
        "https://www.bing.com",
        [
            RelativePath = "search",
            Query = [q = searchText]
        ]
    )
- Headers(url as text, optional options as nullable record)
- Hexadecimal
("X")
- Hour(#datetime(2011, 12, 31, 9, 15, 36)
- Hour(dateTime as any)
- Hours(#duration(5, 4, 3, 2)
- Hours(<duration>)
- Hours(Source)
- Hours(duration as nullable duration)
- Identifier("My Identifier")
- Identifier("MyIdentifier")
- Identifier("x")
- InferContentType(source as binary)
- InferNumberType(text as text, optional culture as nullable text)
- InferOptions("dsn=your_dsn")
- InferOptions(connectionString as any)
- Insert(
    text as nullable text,
    offset as number,
    newText as text
)
- Insert("ABD", 2, "C")
- InsertRange(list as list, index as number, values as list)
- InsertRange({1, 2, 5}, 2, {3, 4})
- InsertRange({2, 3, 4}, 0, {1, {1.1, 1.2}})
- InsertRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
    })
- InsertRows(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- InsertRows(
    table as table,
    offset as number,
    rows as list
)
- IntegerDivide(
    number1 as nullable number,
    number2 as nullable number,
    optional precision as nullable number
)
- IntegerDivide(6, 4)
- IntegerDivide(8.3, 3)
- Intersect({{1..5}, {2..6}, {3..7}})
- Invoke(Record.FieldNames, {[A = 1, B = 2]})
- Invoke(function as function, args as list)
- InvokeWithErrorContext(function as function, context as text)
- Is(123, Number.Type)
- Is(type [a=any], type list)
- Is(type [a=any], type record)
- Is(type any, type number)
- Is(type nullable text, type text)
- Is(type number, type text)
- Is(type text, type nullable text)
- IsDistinct(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- IsDistinct(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 5, Name = "Bob", Phone = "232-1550"]
    })
- IsDistinct(list as list, optional equationCriteria as any)
- IsDistinct(table as table, optional comparisonCriteria as any)
- IsDistinct({1, 2, 3, 3})
- IsDistinct({1, 2, 3})
- IsEmpty(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- IsEmpty(Table.FromRecords({})
- IsEmpty(list as list)
- IsEmpty(table as table)
- IsEmpty({1, 2})
- IsEmpty({})
- IsEven(625)
- IsEven(82)
- IsEven(number as number)
- IsInCurrentDay(DateTime.FixedLocalNow()
- IsInCurrentDay(dateTime as any)
- IsInCurrentHour(DateTime.FixedLocalNow()
- IsInCurrentHour(dateTime as any)
- IsInCurrentMinute(DateTime.FixedLocalNow()
- IsInCurrentMinute(dateTime as any)
- IsInCurrentMonth(DateTime.FixedLocalNow()
- IsInCurrentMonth(dateTime as any)
- IsInCurrentQuarter(DateTime.FixedLocalNow()
- IsInCurrentQuarter(dateTime as any)
- IsInCurrentSecond(DateTime.FixedLocalNow()
- IsInCurrentSecond(dateTime as any)
- IsInCurrentWeek(DateTime.FixedLocalNow()
- IsInCurrentWeek(dateTime as any)
- IsInCurrentYear(DateTime.FixedLocalNow()
- IsInCurrentYear(dateTime as any)
- IsInNextDay(Date.AddDays(DateTime.FixedLocalNow()
- IsInNextDay(dateTime as any)
- IsInNextHour(DateTime.FixedLocalNow()
- IsInNextHour(dateTime as any)
- IsInNextMinute(DateTime.FixedLocalNow()
- IsInNextMinute(dateTime as any)
- IsInNextMonth(Date.AddMonths(DateTime.FixedLocalNow()
- IsInNextMonth(dateTime as any)
- IsInNextNDays(Date.AddDays(DateTime.FixedLocalNow()
- IsInNextNDays(dateTime as any, days as number)
- IsInNextNHours(DateTime.FixedLocalNow()
- IsInNextNHours(dateTime as any, hours as number)
- IsInNextNMinutes(DateTime.FixedLocalNow()
- IsInNextNMinutes(dateTime as any, minutes as number)
- IsInNextNMonths(Date.AddMonths(DateTime.FixedLocalNow()
- IsInNextNMonths(dateTime as any, months as number)
- IsInNextNQuarters(Date.AddQuarters(DateTime.FixedLocalNow()
- IsInNextNQuarters(dateTime as any, quarters as number)
- IsInNextNSeconds(DateTime.FixedLocalNow()
- IsInNextNSeconds(dateTime as any, seconds as number)
- IsInNextNWeeks(Date.AddDays(DateTime.FixedLocalNow()
- IsInNextNWeeks(dateTime as any, weeks as number)
- IsInNextNYears(Date.AddYears(DateTime.FixedLocalNow()
- IsInNextNYears(dateTime as any, years as number)
- IsInNextQuarter(Date.AddQuarters(DateTime.FixedLocalNow()
- IsInNextQuarter(dateTime as any)
- IsInNextSecond(DateTime.FixedLocalNow()
- IsInNextSecond(dateTime as any)
- IsInNextWeek(Date.AddDays(DateTime.FixedLocalNow()
- IsInNextWeek(dateTime as any)
- IsInNextYear(Date.AddYears(DateTime.FixedLocalNow()
- IsInNextYear(dateTime as any)
- IsInPreviousDay(Date.AddDays(DateTime.FixedLocalNow()
- IsInPreviousDay(dateTime as any)
- IsInPreviousHour(DateTime.FixedLocalNow()
- IsInPreviousHour(dateTime as any)
- IsInPreviousMinute(DateTime.FixedLocalNow()
- IsInPreviousMinute(dateTime as any)
- IsInPreviousMonth(Date.AddMonths(DateTime.FixedLocalNow()
- IsInPreviousMonth(dateTime as any)
- IsInPreviousNDays(Date.AddDays(DateTime.FixedLocalNow()
- IsInPreviousNDays(dateTime as any, days as number)
- IsInPreviousNHours(DateTime.FixedLocalNow()
- IsInPreviousNHours(dateTime as any, hours as number)
- IsInPreviousNMinutes(DateTime.FixedLocalNow()
- IsInPreviousNMinutes(dateTime as any, minutes as number)
- IsInPreviousNMonths(Date.AddMonths(DateTime.FixedLocalNow()
- IsInPreviousNMonths(dateTime as any, months as number)
- IsInPreviousNQuarters(Date.AddQuarters(DateTime.FixedLocalNow()
- IsInPreviousNQuarters(dateTime as any, quarters as number)
- IsInPreviousNSeconds(DateTime.FixedLocalNow()
- IsInPreviousNSeconds(dateTime as any, seconds as number)
- IsInPreviousNWeeks(Date.AddDays(DateTime.FixedLocalNow()
- IsInPreviousNWeeks(dateTime as any, weeks as number)
- IsInPreviousNYears(Date.AddYears(DateTime.FixedLocalNow()
- IsInPreviousNYears(dateTime as any, years as number)
- IsInPreviousQuarter(Date.AddQuarters(DateTime.FixedLocalNow()
- IsInPreviousQuarter(dateTime as any)
- IsInPreviousSecond(DateTime.FixedLocalNow()
- IsInPreviousSecond(dateTime as any)
- IsInPreviousWeek(Date.AddDays(DateTime.FixedLocalNow()
- IsInPreviousWeek(dateTime as any)
- IsInPreviousYear(Date.AddYears(DateTime.FixedLocalNow()
- IsInPreviousYear(dateTime as any)
- IsInYearToDate(DateTime.FixedLocalNow()
- IsInYearToDate(dateTime as any)
- IsLeapYear(#date(2012, 01, 01)
- IsLeapYear(dateTime as any)
- IsMemberOf(identity as record, collection as record)
- IsNaN(1/0)
- IsNaN(number as number)
- IsNullable(type as type)
- IsNullable(type nullable number)
- IsNullable(type number)
- IsOdd(625)
- IsOdd(82)
- IsOdd(number as number)
- IsOpenRecord(type [A = number, ...])
- IsOpenRecord(type as type)
- Join(
        customers,
        {"TenantID", "CustomerID"},
        Table.PrefixColumns(orders, "Order")
- Join(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- Join(
    table1 as table,
    key1 as any,
    table2 as table,
    key2 as any,
    optional joinKind as nullable number,
    optional joinAlgorithm as nullable number,
    optional keyEqualityComparers as nullable list
)
- Jun (en-US)
- Jun (zu-ZA)
- June (en-US)
- Juni (id-ID)
- Juni (zu-ZA)
- Keys(table as table)
- Keys(tableWithKeys)
- Last(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- Last(Table.FromRecords({})
- Last(list as list, optional defaultValue as any)
- Last(table as table, optional default as any)
- Last({1, 2, 3})
- Last({}, -1)
- LastN(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- LastN(
    Table.FromRecords({
        [a = -1, b = -2],
        [a = 3, b = 4],
        [a = 5, b = 6]
    })
- LastN(list as list, optional countOrCondition as any)
- LastN(table as table, countOrCondition as any)
- LastN({3, 4, 5, -1, 7, 8, 2}, 1)
- LastN({3, 4, 5, -1, 7, 8, 2}, each _ > 0)
- Length(
        BinaryFormat.List(BinaryFormat.Byte)
- Length("Hello World")
- Length(_)
- Length(binary as nullable binary)
- Length(binaryFormat as function, length as any)
- Length(text as nullable text)
- Lineage(value as any)
- List(BinaryFormat.Byte)
- List(BinaryFormat.Byte, (x)
- List(BinaryFormat.Byte, 2)
- List(BinaryFormat.Byte, length)
- List(binaryFormat as function, optional countOrCondition as any)
- ListItem( type {number} )
- ListItem(type as type)
- ListItem(type {number})
- Ln(15)
- Log(2)
- Log(2, 10)
- Log(number as nullable number, optional base as nullable number)
- Log10(2)
- Lower("AbCd")
- Lower("The quick brown fox jumps over the lazy dog.")
- Lower(text as nullable text, optional culture as nullable text)
- M
()
- M
(It turns out that both record-initializer-expression and let-expression actually define two
environments, one of which does include the variable being initialized. This is useful for
advanced recursive definitions and is covered in Identifier references .
To form the environments for the sub-expressions, the new variables are "merged" with
the variables in the parent environment. The following example shows the environments
for nested records:
Power Query M
[  
    x = 1,          // environment: y, z 
    y = 2,          // environment: x, z 
    z = x + y       // environment: x, y
] 
let 
    x = 1,          // environment: y, z 
    y = 2,          // environment: x, z 
    z = x + y       // environment: x, y
in
    x + y + z       // environment: x, y, z
[
    a = 
    [ 
        x = 1,      // environment: b, y, z 
        y = 2,      // environment: b, x, z 
        z = x + y   // environment: b, x, y 
    ], 
The following example shows the environments for a record nested within a let:
Power Query M
Merging variables with an environment may introduce a conflict between variables
(since each variable in an environment must have a unique name)
- M (which would pose a security risk)
- Mark
(BOM)
- MatchesAll(Source, each Date.Year(_)
- MatchesAll(Source, each Text.Contains(_, "anna", 
Comparer.OrdinalIgnoreCase)
- MatchesAll(list as list, condition as function)
- MatchesAll({1, 2, 3}, each _  > 10)
- MatchesAll({11, 12, 13}, each _  > 10)
- MatchesAllRows(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = -3, b = 4]
    })
- MatchesAllRows(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 6, b = 8]
    })
- MatchesAllRows(table as table, condition as function)
- MatchesAny(Source, each Date.Year(_)
- MatchesAny(Source, each Text.Contains(_, "cat", 
Comparer.OrdinalIgnoreCase)
- MatchesAny(list as list, condition as function)
- MatchesAny({1, 2, 3}, each _  > 10)
- MatchesAny({9, 10, 11}, each _  > 10)
- MatchesAnyRows(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = -3, b = 4]
    })
- MatchesAnyRows(
    Table.FromRecords({
        [a = 1, b = 4],
        [a = 3, b = 8]
    })
- MatchesAnyRows(Source,
        each Text.Contains([FRUIT], "pear", Comparer.OrdinalIgnoreCase)
- MatchesAnyRows(table as table, condition as function)
- Max(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 6, b = 8]
    })
- Max(
    list as list,
    optional default as any,
    optional comparisonCriteria as any,
    optional includeNulls as nullable logical
)
- Max(
    table as table,
    comparisonCriteria as any,
    optional default as any
)
- Max(#table({"a"}, {})
- Max({1, 4, 7, 3, -2, 5}, 1)
- Max({}, -1)
- MaxN(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 0, b = 0],
        [a = 6, b = 2]
    })
- MaxN(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 8, b = 0],
        [a = 6, b = 2]
    })
- MaxN(
    list as list,
    countOrCondition as any,
    optional comparisonCriteria as any,
    optional includeNulls as nullable logical
)
- MaxN(table as table, comparisonCriteria as any, countOrCondition as any)
- MeasureProperties(cube as table)
- MeasureProperty(measure as any, propertyName as text)
- Measures(cube as any)
- Median(list as list, optional comparisonCriteria as any)
- Median({5, 3, 1, 7, 9})
- Metadata(
    Value.RemoveMetadata("abc" meta [a = 1, b = 2])
- Metadata(
    Value.RemoveMetadata("abc" meta [a = 1, b = 2], {"a"})
- Metadata( "Mozart" )
- Metadata( "Mozart" meta [ Rating = 5 ] )
- Metadata(Composer)
- Metadata(table as table)
- Middle(
    text as nullable text,
    start as number,
    optional count as nullable number
)
- Middle("Hello World", 0, 2)
- Middle("Hello World", 6, 20)
- Middle("Hello World", 6, 5)
- Min(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 6, b = 8]
    })
- Min(
    list as list,
    optional default as any,
    optional comparisonCriteria as any,
    optional includeNulls as nullable logical
)
- Min(
    table as table,
    comparisonCriteria as any,
    optional default as any
)
- Min(#table({"a"}, {})
- Min({1, 4, 7, 3, -2, 5})
- Min({}, -1)
- MinN(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 8, b = 0],
        [a = 6, b = 2]
    })
- MinN(
    table as table,
    comparisonCriteria as any,
    countOrCondition as any
)
- MinN( 
    Table.FromRecords({ 
        [a = 2, b = 4],
        [a = 0, b = 0],
        [a = 6, b = 4]
    })
- MinN(list as list, countOrCondition as any, optional comparisonCriteria as 
any, optional includeNulls as nullable logical)
- MinN({3, 4, 5, -1, 7, 8, 2}, 5)
- Minute(#datetime(2011, 12, 31, 9, 15, 36)
- Minute(dateTime as any)
- Minutes(#duration(5, 4, 3, 2)
- Minutes(<duration>)
- Minutes(Source)
- Minutes(duration as nullable duration)
- Mod(
    number as nullable number,
    divisor as nullable number,
    optional precision as nullable number
)
- Mod(5, 3)
- Mod([a], 2)
- Mode(list as list, optional equationCriteria as any)
- Mode({"A", 1, 2, 3, 3, 4, 5, 5})
- Mode({"A", 1, 2, 3, 3, 4, 5})
- Modes(list as list, optional equationCriteria as any)
- Modes({"A", 1, 2, 3, 3, 4, 5, 5})
- Mon (en-US)
- Monday (en-US)
- Month(#datetime(2011, 12, 31, 9, 15, 36)
- Month(dateTime as any)
- MonthName(#datetime(2011, 12, 31, 5, 0, 0)
- MonthName(date as any, optional culture as nullable text)
- Multiply(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- MyFunction()
- MyFunction(1)
- MyFunction(1, 1)
- MyFunction(1, 2, 3)
- MyFunction(1, 2, null)
- MyFunction(1, 2, {3, 4})
- MyFunction(1, null)
- MyFunction(2)
- MyFunction(2, 2)
- MyFunction(2, 4)
- MyFunction(null)
- MyFunction(null, 2)
- MyFunction1()
- MyFunction2()
- NaN (Not a
Number)
- NaN (Not a Number)
- NaN (Not a number)
- NativeQuery(target as any, query as text, optional parameters as any, 
optional options as nullable record)
- NestedJoin(
    Table.FromRecords({
        [CustomerToCall = 1],
        [CustomerToCall = 3]
    })
- NestedJoin(
    table1 as table,
    key1 as any,
    table2 as any,
    key2 as any,
    newColumnName as text,
    optional joinKind as nullable number,
    optional keyEqualityComparers as nullable list
)
- Nodes(graph as record)
- NonNullable( type nullable text )
- NonNullable(Type.NonNullable(type T)
- NonNullable(any)
- NonNullable(nullable t ∈ T)
- NonNullable(t )
- NonNullable(t)
- NonNullable(type T)
- NonNullable(type any)
- NonNullable(type null)
- NonNullable(type nullable T)
- Null(binary as binary)
- NullableEquals(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Numbers(
    start as number,
    count as number,
    optional increment as nullable number
)
- Numbers(1, 10)
- Numbers(1, 10, 2)
- Numeric ("N")
- OpenRecord(type [A = number])
- OpenRecord(type as type)
- Optimize(value as any)
- Ordinal(x as any, y as any)
- OrdinalIgnoreCase("Abc", "abc")
- OrdinalIgnoreCase(x as any, y as any)
- P
(19)
- P (en-US)
- PM (en-
US)
- PM (en-US)
- PM (h "h" m "m")
- PM (h 'h' m 'm')
- PM (h \h m \m)
- POST (when
there is Content)
- PadEnd(
    text as nullable text,
    count as number,
    optional character as nullable text
)
- PadEnd("Name", 10)
- PadEnd("Name", 10, "|")
- PadEnd(Number.ToText(amounts{0}, "C2")
- PadStart(
    text as nullable text,
    count as number,
    optional character as nullable text
)
- PadStart("Name", 10)
- PadStart("Name", 10, "|")
- PadStart(Number.ToText(amounts{1}, "C2")
- Parameters(cube as table)
- Partition(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 1, b = 4],
        [a = 2, b = 4],
        [a = 1, b = 4]
    })
- Partition(table as table, column as text, groups as number, hash as 
function)
- PartitionKey(table as table)
- PartitionValues(table as table)
- Parts("http://contoso?
a=" & data)
- Parts("www.adventure-works.com")
- Parts(absoluteUri as text)
- Percent ("P")
- Percentile(list as list, percentiles as any, optional options as nullable 
record)
- Percentile({5, 3, 1, 7, 9}, 0.25)
- Percentile({5, 3, 1, 7, 9}, {0.25, 0.5, 0.75}, 
[PercentileMode=PercentileMode.ExcelExc])
- Permutations(5, 3)
- Permutations(setSize as nullable number, permutationSize as nullable 
number)
- Pivot(
    Table.FromRecords({
        [key = "x", attribute = "a", value = 1],
        [key = "x", attribute = "c", value = 3],
        [key = "x", attribute = "c", value = 5],
        [key = "y", attribute = "a", value = 2],
        [key = "y", attribute = "b", value = 4]
    })
- Pivot(
    Table.FromRecords({
        [key = "x", attribute = "a", value = 1],
        [key = "x", attribute = "c", value = 3],
        [key = "y", attribute = "a", value = 2],
        [key = "y", attribute = "b", value = 4]
    })
- Pivot(table as table, pivotValues as list, attributeColumn as text, 
valueColumn as text, optional aggregationFunction as nullable function)
- Point
("F")
- PositionOf(
        "THE RAIN IN SPAIN FALLS MAINLY ON THE PLAIN.", 
        "the", 
        Occurrence.Last, 
        Comparer.OrdinalIgnoreCase
    )
- PositionOf(
        Source, 
        28,
        Occurrence.First, 
        (x, y)
- PositionOf(
        {"dog", "cat", "DOG", "pony", "bat", "rabbit", "dOG"}, 
        "dog", 
        Occurrence.Last, 
        Comparer.OrdinalIgnoreCase
    )
- PositionOf(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 1, b = 4],
        [a = 2, b = 4],
        [a = 1, b = 4]
    })
- PositionOf(
    list as list,
    value as any,
    optional occurrence as nullable number,
    optional equationCriteria as any
)
- PositionOf(
    table as table,
    row as record,
    optional occurrence as any,
    optional equationCriteria as any
)
- PositionOf(
    text as text,
    substring as text,
    optional occurrence as nullable number,
    optional comparer as nullable function
)
- PositionOf("Hello", "ll")
- PositionOf("Hello, World! Hello, World!", "World")
- PositionOf("Hello, World! Hello, World!", "World", Occurrence.Last)
- PositionOf(YearList, TargetYear, Occurrence.All)
- PositionOf({1, 2, 3}, 3)
- PositionOfAny(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 1, b = 4],
        [a = 2, b = 4],
        [a = 1, b = 4]
    })
- PositionOfAny(
    list as list,
    values as list,
    optional occurrence as nullable number,
    optional equationCriteria as any
)
- PositionOfAny(
    text as text,
    characters as list,
    optional occurrence as nullable number
)
- PositionOfAny("Hello, World!", {"H", "W"})
- PositionOfAny("Hello, World!", {"H", "W"}, Occurrence.All)
- PositionOfAny(table as table, rows as list, optional occurrence as nullable 
number, optional equationCriteria as any)
- PositionOfAny({1, 2, 3}, {2, 3})
- Positions(list as list)
- Positions({1, 2, 3, 4, null, 5})
- Power(5, 3)
- Power(number as nullable number, power as nullable number)
- PrefixColumns(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- Product(numbersList as list, optional precision as nullable number)
- Product({1, 2, 3, 3, 4, 5, 5})
- Profile(table as table, optional additionalAggregates as nullable list)
- PromoteHeaders(
    Table.FromRecords({
        [Column1 = "CustomerID", Column2 = "Name", Column3 = #date(1980, 1, 1)
- PromoteHeaders(
    Table.FromRecords({
        [Rank = 1, Name = "Name", Date = #date(1980, 1, 1)
- PromoteHeaders(Csv.Document(csv)
- PromoteHeaders(Csv.Document(csv, null, "#|#")
- PromoteHeaders(Excel.Workbook(File.Contents("C:\myfile.xlsx", null,
true)
- PromoteHeaders(table as table, optional options as nullable record)
- Proper("The quick brown fox jumps over the lazy dog.")
- Proper("the QUICK BrOWn fOx jUmPs oVER tHe LAzy DoG")
- Proper(text as nullable text, optional culture as nullable text)
- Properties(cube as table)
- PropertyKey(property as any)
- QuarterOfYear(#date(2011, 12, 31)
- QuarterOfYear(dateTime as any)
- Query(
    connectionString as any,
    query as text,
    optional options as nullable record
)
- Query(
    providerName as text,
    connectionString as any,
    query as text,
    optional options as nullable record
)
- Query("dsn=your_dsn", "select * from Customers")
- QuoteAfterDelimiter (default)
- RFC1123
("R", "r")
- RFC1123 ("R", "r")
- Random(3)
- Random(3, 2)
- Random(count as number, optional seed as nullable number)
- RandomBetween(1, 5)
- RandomBetween(bottom as number, top as number)
- Range(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- Range(
    binary as binary,
    offset as number,
    optional count as nullable number
)
- Range(
    list as list,
    offset as number,
    optional count as nullable number
)
- Range(
    table as table,
    offset as number,
    optional count as nullable number
)
- Range(
    text as nullable text,
    offset as number,
    optional count as nullable number
)
- Range("Hello World Hello", 6, 5)
- Range("Hello World", 6)
- Range(#binary({0..10})
- Range({1..10}, 6)
- Range({1..10}, 6, 2)
- Record(
    reason as text,
    optional message as nullable text,
    optional detail as any,
    optional parameters as nullable list,
    optional errorCode as nullable text
)
- Record("Expression.Error", 
            "Not Implemented")
- Record("Expression.Error", 
//         "A cyclic reference was encountered during evaluation")
- Record("FileNotFound", "File my.txt not found",
     "my.txt")
- Record([
            length = length,
            list = BinaryFormat.List(BinaryFormat.Byte, length)
- Record([
        A = BinaryFormat.UnsignedInteger16,
        B = BinaryFormat.UnsignedInteger32
    ])
- Record(record as record)
- RecordFields(
    Value.Type(
        Value.ReplaceType(
            [Column1 = 123],
            type [Column1 = number]
        )
- RecordFields( type [A=text, B=time] )
- RecordFields(tableRowType)
- RecordFields(type [A = number, optional B = any])
- RecordFields(type as type)
- Remove("a,b;c", {",",";"})
- Remove(text as nullable text, removeChars as any)
- RemoveColumns(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- RemoveColumns(
    table as table,
    columns as any,
    optional missingField as nullable number
)
- RemoveFields(
    record as record,
    fields as any,
    optional missingField as nullable number
)
- RemoveFields([CustomerID = 1, Item = "Fishing rod", Price = 18.00], 
"Price")
- RemoveFields([CustomerID = 1, Item = "Fishing rod", Price = 18.00], 
Output
[CustomerID = 1]
{"Price", "Item"})
- RemoveFirstN(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- RemoveFirstN(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"], 
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"] , 
Output
Power Query M
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"] , 
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- RemoveFirstN(list as list, optional countOrCondition as any)
- RemoveFirstN(table as table, optional countOrCondition as any)
- RemoveFirstN({1, 2, 3, 4, 5}, 3)
- RemoveFirstN({5, 4, 2, 6, 1}, each _ > 3)
- RemoveItems(list1 as list, list2 as list)
- RemoveItems({1, 2, 3, 4, 2, 5, 5}, {2, 4, 6})
- RemoveLastN(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- RemoveLastN(list as list, optional countOrCondition as any)
- RemoveLastN(table as table, optional countOrCondition as any)
- RemoveLastN({1, 2, 3, 4, 5}, 3)
- RemoveLastN({5, 4, 2, 6, 4}, each _ > 3)
- RemoveMatchingItems(
    list1 as list,
    list2 as list,
    optional equationCriteria as any
)
- RemoveMatchingItems({1, 2, 3, 4, 5, 5}, {1, 5})
- RemoveMatchingRows(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 3, b = 4],
        [a = 1, b = 6]
    })
- RemoveMatchingRows(
    table as table,
    rows as list,
    optional equationCriteria as any
)
- RemoveMetadata(value as any, optional metaValue as any)
- RemoveMetadata(x)
- RemoveNulls({1, 2, 3, null, 4, 5, null, 6})
- RemoveRange(
    list as list,
    index as number,
    optional count as nullable number
)
- RemoveRange(
    text as nullable text,
    offset as number,
    optional count as nullable number
)
- RemoveRange("ABEFC", 2)
- RemoveRange("ABEFC", 2, 2)
- RemoveRange({1, 2, 3, 4, -6, -2, -1, 5}, 4, 3)
- RemoveRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- RemoveRows(
    table as table,
    offset as number,
    optional count as nullable number
)
- RemoveRowsWithErrors(
    Table.FromRecords({
        [Column1 = ...],
        [Column1 = 2],
        [Column1 = 3]
    })
- RemoveRowsWithErrors(table as table, optional columns as nullable list)
- RemoveZone(#datetimezone(2011, 12, 31, 9, 15, 36, -7, 0)
- RemoveZone(dateTimeZone as nullable datetimezone)
- RenameColumns(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- RenameColumns(
    Table.FromRecords({[CustomerNum = 1, Name = "Bob", Phone = "123-4567"]})
- RenameColumns(
    Table.FromRecords({[CustomerNum = 1, Name = "Bob", PhoneNum = "123-4567"]})
- RenameColumns(
    table as table,
    renames as list,
    optional missingField as nullable number
)
- RenameFields(
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", UnitPrice = 100.0],
    {"UnitPrice", "Price"}
)
- RenameFields(
    [OrderNum = 1, CustomerID = 1, Item = "Fishing rod", UnitPrice = 100.0],
    {
        {"UnitPrice", "Price"},
        {"OrderNum", "OrderID"}
    }
)
- RenameFields(
    record as record,
    renames as list,
    optional missingField as nullable number
)
- ReorderColumns(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- ReorderColumns(
    Table.FromRecords({[CustomerID = 1, Phone = "123-4567", Name = "Bob"]})
- ReorderColumns(
    table as table,
    columnOrder as list,
    optional missingField as nullable number
)
- ReorderFields(
        Source, 
        {"Purchase", "Last Name", "First Name"}, 
        MissingField.UseNull
    )
- ReorderFields(
    [CustomerID = 1, OrderID = 1, Item = "Fishing rod", Price = 100.0],
    {"OrderID", "CustomerID"}
)
- ReorderFields(
    record as record,
    fieldOrder as list,
    optional missingField as nullable number
)
- Repeat(
    Table.FromRecords({
        [a = 1, b = "hello"],
        [a = 3, b = "world"]
    })
- Repeat("*", Text.Length([Name])
- Repeat("a", 5)
- Repeat("helloworld.", 3)
- Repeat(list as list, count as number)
- Repeat(replacementValue, Text.Length(currentValue)
- Repeat(table as table, count as number)
- Repeat(text as nullable text, count as number)
- Repeat({1, 2}, 3)
- Replace(
    text as nullable text,
    old as text,
    new as text
)
- Replace("the quick brown fox jumps over the lazy dog", "the", "a")
- ReplaceDimensions(cube as table, dimensions as table)
- ReplaceErrorValues(
    Table.FromRows({{..., ...}, {1, 2}}, {"A", "B"})
- ReplaceErrorValues(
    Table.FromRows({{1, "hello"}, {3, ...}}, {"A", "B"})
- ReplaceErrorValues(table as table, errorReplacement as list)
- ReplaceFacets(type as type, facets as record)
- ReplaceKeys(tableWithKeys, {[Columns = {"Id"}, Primary = 
false]})
- ReplaceMatchingItems(
    list as list,
    replacements as list,
    optional equationCriteria as any
)
- ReplaceMatchingItems({1, 2, 3, 4, 5}, {{5, -5}, {1, -1}})
- ReplaceMatchingRows(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 2, b = 3],
        [a = 3, b = 4],
        [a = 1, b = 2]
    })
- ReplaceMatchingRows(
    table as table,
    replacements as list,
    optional equationCriteria as any
)
- ReplaceMetadata(value as any, metaValue as any)
- ReplaceMetadata(x, Value.Metadata(x)
- ReplacePartitionKey(table as table, partitionKey as nullable list)
- ReplaceRange(
    list as list,
    index as number,
    count as number,
    replaceWith as list
)
- ReplaceRange(
    text as nullable text,
    offset as number,
    count as number,
    newText as text
)
- ReplaceRange("ABGF", 2, 1, "CDE")
- ReplaceRange({1, 2, 7, 8, 9, 5}, 2, 3, {3, 4})
- ReplaceRelationshipIdentity(value as any, identity as text)
- ReplaceRows(
    Table.FromRecords({
        [Column1 = 1],
        [Column1 = 2],
        [Column1 = 3],
        [Column1 = 4],
        [Column1 = 5]
    })
- ReplaceRows(
    table as table,
    offset as number,
    count as number,
    rows as list
)
- ReplaceTableKeys(
        BaseType, 
        {
            [Columns = {"ID"}, Primary = true],
            [Columns = {"FirstName", "LastName"}, Primary = false]
        }
    )
- ReplaceTableKeys(TypeWithKey, {})
- ReplaceTableKeys(tableType as type, keys as list)
- ReplaceTableKeys(tableType, {})
- ReplaceTablePartitionKey(tableType as type, partitionKey as nullable list)
- ReplaceText(
    text as nullable text,
    old as text,
    new as text
)
- ReplaceText("hEllo world", "hE", "He")
- ReplaceValue(
    Table.FromRecords({
        [A = 1, B = "hello"],
        [A = 2, B = "goodbye"],
        [A = 3, B = "goodbyes"]
    })
- ReplaceValue(
    Table.FromRecords({
        [A = 1, B = "hello"],
        [A = 2, B = "wurld"]
    })
- ReplaceValue(
    Table.FromRecords({
        [Name = "Cindy", Country = "US"],
        [Name = "Bob", Country = "CA"]
    })
- ReplaceValue(
    list as list,
    oldValue as any,
    newValue as any,
    replacer as function
)
- ReplaceValue(
    table as table,
    oldValue as any,
    newValue as any,
    replacer as function,
    columnsToSearch as list
)
- ReplaceValue(
    value as any,
    old as any,
    new as any)
- ReplaceValue(11, 11, 10)
- ReplaceValue({"a", "B", "a", "a"}, "a", "A", Replacer.ReplaceText)
- Reports(optional loginUrl as nullable text, optional options as 
nullable record)
- Request(WebMethod.Get, "https://bing.com")
- Request(method as text, url as text, optional options as nullable 
record)
- Result (12 hours)
- Result (4 hours)
- Result (subtracts two hours)
- Reverse("123")
- Reverse(text as nullable text)
- Reverse({1..10})
- ReverseRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- ReverseRows(table as table)
- Round(1.234)
- Round(1.2345, 2)
- Round(1.2345, 3, RoundingMode.Down)
- Round(1.2345, 3, RoundingMode.Up)
- Round(1.56)
- Round(number as nullable number, optional digits as nullable number, 
optional roundingMode as nullable number)
- RoundAwayFromZero(-1.2)
- RoundAwayFromZero(-1.234, 2)
- RoundAwayFromZero(1.2)
- RoundAwayFromZero(number as nullable number, optional digits as nullable 
number)
- RoundDown(1.234)
- RoundDown(1.999)
- RoundDown(1.999, 2)
- RoundDown(value)
- RoundDown(x)
- RoundTowardZero(-1.2)
- RoundTowardZero(-1.234, 2)
- RoundTowardZero(1.2)
- RoundTowardZero(number as nullable number, optional digits as nullable 
number)
- RoundUp(1.234)
- RoundUp(1.234, 2)
- RoundUp(1.999)
- RoundUp(value)
- RoundUp(x)
- RowCount(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- RowCount(_)
- ScalarVector(scalarFunctionType as type, vectorFunction as function)
- SchemaFrom(schema as any)
- Second(#datetime(2011, 12, 31, 9, 15, 36.5)
- Second(dateTime as any)
- Seconds(#duration(5, 4, 3, 2)
- Seconds(<duration>)
- Seconds(Source)
- Seconds(duration as nullable duration)
- Select( {[a=1, b=1], [a=2, b=4]}, (_)
- Select( {[a=1, b=1], [a=2, b=4]}, each [a] = [b])
- Select("a,b;c", {"a".."z"})
- Select(list as list, selection as function)
- Select(list, (n)
- Select(text as nullable text, selectChars as any)
- Select({1, -3, 4, 9, -2}, each _ > 0)
- SelectColumns(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- SelectColumns(
    Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- SelectColumns(table as table, columns as any, optional missingField as 
nullable number)
- SelectFields(
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0],
    {"Item", "Price"}
)
- SelectFields(
    record as record,
    fields as any,
    optional missingField as nullable number
)
- SelectRows(
        Source, 
        each Date.Year([Posted Date])
- SelectRows(
        Source, 
        each Text.Contains([Account Code], "A-")
- SelectRows(
        Source, each Text.Contains([FRUIT], "pear", Comparer.OrdinalIgnoreCase)
- SelectRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- SelectRows(  
      Table.FromRecords({  
            [CustomerID = 1, Name = "Bob", Phone = "123-4567"],  
            [CustomerID = 2, Name = "Jim", Phone = "987-6543"] ,  
            [CustomerID = 3, Name = "Paul", Phone = "543-7890"] ,  
            [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]  
      })
- SelectRows( aTable, (_)
- SelectRows( aTable, each [Weight] > 12 )
- SelectRows(table as table, condition as function)
- SelectRowsWithErrors(
    Table.FromRecords({
        [CustomerID = ..., Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- SelectRowsWithErrors(table as table, optional columns as nullable list)
- ShapeTable(table as table, optional options as nullable record)
- Sign(-182)
- Sign(0)
- Sign(182)
- SignedInteger16(binary as binary)
- SignedInteger32(binary as binary)
- SignedInteger64(binary as binary)
- Single(binary as binary)
- Single(list as list)
- Single({1, 2, 3})
- Single({1})
- SingleOrDefault(list as list, optional default as any)
- SingleOrDefault({1})
- SingleOrDefault({})
- SingleOrDefault({}, -1)
- SingleRow(Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-
4567"]})
- SingleRow(table as table)
- Sinh(number as nullable number)
- Skip(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"],
        [CustomerID = 4, Name = "Ringo", Phone = "232-1550"]
    })
- Skip(
    Table.FromRecords({
        [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0],
        [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0],
Output
Power Query M
        [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25.0],
        [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200.0],
        [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2.0],
        [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20.0],
        [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
        [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100.0],
        [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25]
    })
- Skip(list as list, optional countOrCondition as any)
- Skip(table as table, optional countOrCondition as any)
- Skip({1, 2, 3, 4, 5}, 3)
- Skip({5, 4, 2, 6, 1}, each _ > 3)
- Sort(
    Table.FromRecords({
        [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0],
        [OrderID = 2, CustomerID = 1, Item = "1 lb. worms", Price = 5.0],
        [OrderID = 3, CustomerID = 2, Item = "Fishing net", Price = 25.0],
        [OrderID = 4, CustomerID = 3, Item = "Fish tazer", Price = 200.0],
        [OrderID = 5, CustomerID = 3, Item = "Bandaids", Price = 2.0],
        [OrderID = 6, CustomerID = 1, Item = "Tackle box", Price = 20.0],
        [OrderID = 7, CustomerID = 5, Item = "Bait", Price = 3.25],
        [OrderID = 8, CustomerID = 5, Item = "Fishing Rod", Price = 100.0],
        [OrderID = 9, CustomerID = 6, Item = "Bait", Price = 3.25]
    })
- Sort(Source, Order.Ascending)
- Sort(list as list, optional comparisonCriteria as any)
- Sort(table as table, comparisonCriteria as any)
- Sort({2, 3, 1})
- Sort({2, 3, 1}, (x, y)
- Sort({2, 3, 1}, Order.Descending)
- Split("Name, the Customer, the Purchase Date", ", the ")
- Split("Name|Address|PhoneNumber", "|")
- Split(Customers, 2)
- Split(list as list, pageSize as number)
- Split(table as table, pageSize as number)
- Split(text as text, separator as text)
- SplitAny("Name|Customer ID|Purchase|Month-Day-Year", "|-")
- SplitAny(text as text, separators as text)
- SplitAt(#table({"a", "b", "c"}, {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}})
- SplitAt(table as table, count as number)
- SplitByNothing()
- SplitColumn(
        Source,
        "Name",
        Splitter.SplitTextByDelimiter(" ")
- SplitColumn(
    table as table,
    sourceColumn as text,
    splitter as function,
    optional columnNamesOrNumber as any,
    optional default as any,
    optional extraColumns as any
)
- SplitTextByAnyDelimiter(
    delimiters as list,
    optional quoteStyle as nullable number,
    optional startAtEnd as nullable logical
)
- SplitTextByAnyDelimiter({",", ";"}, QuoteStyle.Csv)
- SplitTextByAnyDelimiter({",", ";"}, QuoteStyle.Csv, startAtEnd)
- SplitTextByCharacterTransition(before as anynonnull, after as anynonnull)
- SplitTextByCharacterTransition({"A".."Z", "a".."z"}, {"0".."9"})
- SplitTextByDelimiter(
    delimiter as text,
    optional quoteStyle as nullable number,
    optional csvStyle as nullable number
)
- SplitTextByDelimiter(",", QuoteStyle.Csv)
- SplitTextByEachDelimiter(
    delimiters as list,
    optional quoteStyle as nullable number,
    optional startAtEnd as nullable logical
)
- SplitTextByEachDelimiter({",", ";"})
- SplitTextByEachDelimiter({",", ";"}, QuoteStyle.None, startAtEnd)
- SplitTextByLengths(lengths as list, optional startAtEnd as nullable 
logical)
- SplitTextByLengths({2, 3})
- SplitTextByLengths({5, 2}, startAtEnd)
- SplitTextByPositions(positions as list, optional startAtEnd as nullable 
logical)
- SplitTextByPositions({0, 3, 4})
- SplitTextByPositions({0, 5}, startAtEnd)
- SplitTextByRanges(ranges as list, optional startAtEnd as nullable 
logical)
- SplitTextByRanges({{0, 4}, {2, 10}})
- SplitTextByRanges({{0, 5}, {6, 2}}, startAtEnd)
- SplitTextByRepeatedLengths(3)
- SplitTextByRepeatedLengths(3, startAtEnd)
- SplitTextByRepeatedLengths(length as number, optional startAtEnd as 
nullable logical)
- SplitTextByWhitespace(QuoteStyle.None)
- SplitTextByWhitespace(optional quoteStyle as nullable number)
- Sqrt(625)
- Sqrt(85)
- StandardDeviation(numbersList as list)
- StandardDeviation({1..5})
- Start("Hello, World", 5)
- Start([Last Name], 3)
- Start(text as nullable text, count as number)
- StartOfDay(#datetime(2011, 10, 10, 8, 0, 0)
- StartOfDay(dateTime as any)
- StartOfHour(#datetime(2011, 10, 10, 8, 10, 32)
- StartOfHour(dateTime as any)
- StartOfMonth(#datetime(2011, 10, 10, 8, 10, 32)
- StartOfMonth(dateTime as any)
- StartOfQuarter(#datetime(2011, 10, 10, 8, 0, 0)
- StartOfQuarter(dateTime as any)
- StartOfWeek(#datetime(2011, 10, 11, 8, 10, 32)
- StartOfWeek(dateTime as any, optional firstDayOfWeek as nullable number)
- StartOfYear(#datetime(2011, 10, 10, 8, 10, 32)
- StartOfYear(dateTime as any)
- StartsWith(
    text as nullable text,
    substring as text,
    optional comparer as nullable function
)
- StartsWith("Hello, World", "Hello")
- StartsWith("Hello, World", "hello")
- StartsWith("Hello, World", "hello", Comparer.OrdinalIgnoreCase)
- StopFolding(MyTable)
- StopFolding(table as table)
- Subtract(
    value1 as any,
    value2 as any,
    optional precision as nullable number
)
- Sum([price])
- Sum(list as list, optional precision as nullable number)
- Sum(list)
- Sum({1, 2, 3})
- SwitchZone(
    dateTimeZone as nullable datetimezone,
    timezoneHours as number,
    optional timezoneMinutes as nullable number
)
- SwitchZone(#datetimezone(2010, 12, 31, 11, 56, 02, 7, 30)
- Table(
    html as any,
    columnNameSelectorPairs as list,
    optional options as nullable record
)
- Table("<a href=""/test.html"">Test</a>", {{"Link", "a", each [Attributes]
[href]}})
- Table("<div class=""name"">Jo</div><span>Manager</span>", {{"Name", ".name"}, 
{"Title", "span"}}, [RowSelector=".name"])
- Table(directory as table, optional options as nullable record)
- TableColumn(tableType as type, column as text)
- TableKeys(AddKey)
- TableKeys(KeyRemoved)
- TableKeys(KeysAdded)
- TableKeys(tableType as type)
- TablePartitionKey(tableType as type)
- TableRow( type table [X=number, Y=date] )
- TableRow(Value.Type(#table({"Column1"}, {})
- TableRow(table as type)
- TableSchema(tableType as type)
- Tables(
    contents as any,
    optional options as nullable record,
    optional encoding as nullable number
)
- Tables(File.Contents("C:\invoices.xml")
- Tables(File.Contents("c:\sample.pdf")
- Tables(account as text, optional options as nullable record)
- Tables(pdf as binary, optional options as nullable record)
- Tables(url as text, optional options as nullable record)
- Tanh(number as nullable number)
- Text
(WKT)
- Text (WKT)
- Text(
        BinaryFormat.Byte,
        TextEncoding.Ascii
    )
- Text(2, TextEncoding.Ascii)
- Text(length as any, optional encoding as nullable number)
- Time
(UTC)
- Time (UTC)
- Time(#datetime(2010, 12, 31, 11, 56, 02)
- Time(dateTime as any)
- Times(
    start as time,
    count as number,
    step as duration
)
- Times(#time(12, 0, 0)
- ToBinary(
    lines as list,
    optional lineSeparator as nullable text,
    optional encoding as nullable number,
    optional includeByteOrderMark as nullable logical
)
- ToBinary(
    text as nullable text,
    optional encoding as nullable number,
    optional includeByteOrderMark as nullable logical
)
- ToBinary("012")
- ToBinary("hello world!")
- ToColumns(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"]
    })
- ToExpression(sql as text, environment as record)
- ToList(
    Table.FromRows({
        {Number.ToText(1)
- ToList("Hello World")
- ToList([A = 1, B = 2, C = 3])
- ToList(table as table, optional combiner as nullable function)
- ToLocal(
        #datetimezone(2024, 4, 10, 6, 30, 0, 0, 0)
- ToLocal(#datetimezone(2010, 12, 31, 11, 56, 02, 7, 30)
- ToLocal(dateTimeZone as nullable datetimezone)
- ToNumber("#(tab)
- ToNumber(character as nullable text)
- ToRecord(#date(2011, 12, 31)
- ToRecord(#datetime(2011, 12, 31, 11, 56, 2)
- ToRecord(#datetimezone(2011, 12, 31, 11, 56, 2, 8, 0)
- ToRecord(#duration(2, 5, 55, 20)
- ToRecord(#time(11, 56, 2)
- ToRecord(date as date)
- ToRecord(date, time, dateTime, or
dateTimeZone as date, time, datetime, or
datetimezone)
- ToRecord(dateTime as datetime)
- ToRecord(dateTimeZone as datetimezone)
- ToRecord(duration as duration)
- ToRecord(time as time)
- ToRecords(
    Table.FromRows(
        {
            {1, "Bob", "123-4567"},
            {2, "Jim", "987-6543"},
            {3, "Paul", "543-7890"}
        },
        {"CustomerID", "Name", "Phone"}
    )
- ToRows(
    Table.FromRecords({
        [CustomerID = 1, Name = "Bob", Phone = "123-4567"],
        [CustomerID = 2, Name = "Jim", Phone = "987-6543"],
        [CustomerID = 3, Name = "Paul", Phone = "543-7890"]
    })
- ToTable([OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = 100.0])
- ToText(
        #"Origin Local Date", [Format = "o"]
    )
- ToText(
        #"Origin Offset Date", [Format = "o"]
    )
- ToText(
        #"Origin UTC Date", [Format = "o"]
    )
- ToText(
    date as nullable date,
    optional options as any,
    optional culture as nullable text
)
- ToText(
    dateTime as nullable datetime,
    optional options as any,
    optional culture as nullable text
)
- ToText(
    dateTimeZone as nullable datetimezone,
    optional options as any,
    optional culture as nullable text
)
- ToText(
    number as nullable number,
    optional format as nullable text,
    optional culture as nullable text
)
- ToText(#"New Local Date")
- ToText(#"New Offset Date")
- ToText(#"New UTC Date")
- ToText(#"Origin Offset Date")
- ToText(#date(1, 12, 1)
- ToText(#date(2000, 1, 1)
- ToText(#date(2010, 12, 31)
- ToText(#date(2023, 12, 26)
- ToText(#date(2024, 1, 1)
- ToText(#date(2024, 3, 15)
- ToText(#date(2024, 4, 10)
- ToText(#date(2024, 8, 18)
- ToText(#date(70, 08, 04)
- ToText(#datetime(2000, 2, 8, 3, 45, 12)
- ToText(#datetime(2010, 12, 30, 2, 4, 50.36973)
- ToText(#datetime(2010, 12, 31, 01, 30, 25)
- ToText(#datetime(2024, 1, 1, 18, 9, 1)
- ToText(#datetime(2024, 1, 1, 6, 9, 1)
- ToText(#datetime(2024, 1, 1, 9, 18, 1.500)
- ToText(#datetime(2024, 1, 2, 6, 30, 15)
- ToText(#datetime(2024, 4, 10, 6, 30, 0)
- ToText(#datetime(2024, 8, 18, 16, 50, 0)
- ToText(#datetime(2024, 8, 29, 19, 27, 15)
- ToText(#datetime(2024, 8, 29, 19, 27, 15.018)
- ToText(#datetimezone(2000, 2, 8, 3, 45, 12, 2, 0)
- ToText(#datetimezone(2010, 12, 30, 2, 4, 50.36973, -8,0)
- ToText(#datetimezone(2010, 12, 31, 01, 30, 25, 2, 0)
- ToText(#duration(2, 5, 55, 20)
- ToText(#time(11, 56, 2)
- ToText(-0.1234, "P1")
- ToText(-1234, "##;(##)
- ToText(-12345, "D")
- ToText(-12345, "D8")
- ToText(-12445.6789, "N", "")
- ToText(-12445.6789, "N1", "sv-SE")
- ToText(-1898300.1987, "F1", "")
- ToText(-1898300.1987, "F3", "es-ES")
- ToText(-29541, "F3", "")
- ToText(.0000023, "G", "")
- ToText(.0000023, "G", "fr-FR")
- ToText(.0023, "G", "")
- ToText(.00354, "#0.##" & Character.FromNumber(0x2030)
- ToText(.086, "#0.##%", "")
- ToText(.2468013, "P", "")
- ToText(.2468013, "P", "hr-HR")
- ToText(.2468013, "P1", "en-US")
- ToText(.56, "0.0", "")
- ToText(0, "##;(##)
- ToText(0x2045e, "X")
- ToText(0x2045e, "X8")
- ToText(0x2045e, "x")
- ToText(1.2, "#.##", "")
- ToText(1.2, "0.00", "")
- ToText(1.2, "00.00", "")
- ToText(1.2, "00.00", "da-DK")
- ToText(123, """###"" ##0 dollars and ""00"" cents ""###""")
- ToText(123, """\\\"" ##0 dollars and ""00"" cents ""\\\""")
- ToText(123, "#####")
- ToText(123, "'###' ##0 dollars and '00' cents '###'")
- ToText(123, "'\\\' ##0 dollars and '00' cents '\\\'")
- ToText(123, "00000", "")
- ToText(123, "\#\#\# ##0 dollars and \0\0 cents \#\#\#")
- ToText(123, "\\\\\\ ##0 dollars and \0\0 cents \\\\\\")
- ToText(123.456, "C2")
- ToText(123.8, "#,##0.0K")
- ToText(1234, "##;(##)
- ToText(1234, "G2", "")
- ToText(1234.567890, "0,0.00", "")
- ToText(12345, "D")
- ToText(12345, "D8")
- ToText(12345.6789, "C")
- ToText(12345.6789, "C3")
- ToText(12345.6789, "C3", "da-DK")
- ToText(12345.6789, "E", "")
- ToText(12345.6789, "E", "fr-FR")
- ToText(12345.6789, "E10", "")
- ToText(12345.6789, "G", "")
- ToText(12345.6789, "G", "fr-FR")
- ToText(12345.6789, "G7", "")
- ToText(12345.6789, "e4", "")
- ToText(123456, "[##-##-##]")
- ToText(123456789, "N1", "")
- ToText(123456789, "X")
- ToText(123456789, "X2")
- ToText(1234567890, "#")
- ToText(1234567890, "#,#", "")
- ToText(1234567890, "#,##0,,", "")
- ToText(1234567890, "#,,", "")
- ToText(1234567890, "#,,,", "")
- ToText(1234567890, "(###)
- ToText(1234567890, "0,0", "")
- ToText(1234567890, "0,0", "el-GR")
- ToText(1234567890.123456, "0,0.0", "")
- ToText(17843, "F", "")
- ToText(18934.1879, "F", "")
- ToText(18934.1879, "F0", "")
- ToText(2)
- ToText(3)
- ToText(4)
- ToText(4, "e")
- ToText(42, "My Number = #")
- ToText(86000, "0.###E+0", "")
- ToText(86000, "0.###E+000", "")
- ToText(86000, "0.###E-000", "")
- ToText(9.3, "##.0""%""")
- ToText(9.3, "##.0'%'")
- ToText(9.3, "##.0\%")
- ToText(9.3, "'\'##'\'")
- ToText(9.3, "\""##\""")
- ToText(9.3, "\'##\'")
- ToText(9.3, "\\##\\")
- ToText(Character.ToNumber("#(0001F600)
- ToText(DateTime.FromText(
              "25 Dec 2023 12:00 pm pst", [Format = #"Date Format"])
- ToText(DateTime.FromText(
            "25 Dec 2023 12:00 pm PST", [Format = #"Date Formats"{0}])
- ToText(DateTime.LocalNow()
- ToText(DateTimeZone.LocalNow()
- ToText(DateTimeZone.SwitchZone(
            #datetimezone(2024, 8, 1, 0, 0, 0, 0, 0)
- ToText(DateTimeZone.ToLocal(date1)
- ToText(DateTimeZone.ToUtc(date1)
- ToText(DateTimeZone.UtcNow()
- ToText(Double.From(86000)
- ToText(Number.PI, "G5", "")
- ToText(Sales[UnitPrice])
- ToText(binary as nullable binary, optional encoding as nullable number)
- ToText(date)
- ToText(date, format1)
- ToText(date, format2)
- ToText(date, format3)
- ToText(date, time, dateTime, or dateTimeZone
as date, time, datetime, or datetimezone)
- ToText(date1, [Format = "O"])
- ToText(date1, [Format = "r"])
- ToText(dateOffset, [Format = "r"])
- ToText(dateOffset, [Format = "u"])
- ToText(duration as nullable duration, optional format as nullable text)
- ToText(lines as list, optional lineSeparator as nullable text)
- ToText(logical as logical)
- ToText(logicalValue as nullable logical)
- ToText(number as number)
- ToText(row[a])
- ToText(time as nullable time, optional options as any, optional culture as 
nullable text)
- ToText(true)
- ToUtc(
        #datetimezone(2024, 4, 12, 9, 30, 0, 0, 0)
- ToUtc(#datetimezone(2010, 12, 31, 11, 56, 02, 7, 30)
- ToUtc(date1)
- ToUtc(dateTimeZone as nullable datetimezone)
- ToWellKnownText(input as nullable record, optional omitSRID as nullable 
logical)
- TotalDays(#duration(1, 12, 0, 0)
- TotalDays(#duration(5, 4, 3, 2)
- TotalDays(<duration>)
- TotalDays(duration as nullable duration)
- TotalHours(#duration(1, 12, 0, 0)
- TotalHours(#duration(5, 4, 3, 2)
- TotalHours(<duration>)
- TotalHours(duration as nullable duration)
- TotalMinutes(#duration(1, 12, 0, 0)
- TotalMinutes(#duration(5, 4, 3, 2)
- TotalMinutes(<duration>)
- TotalMinutes(duration as nullable duration)
- TotalSeconds(#duration(1, 12, 0, 0)
- TotalSeconds(#duration(5, 4, 3, 2)
- TotalSeconds(<duration>)
- TotalSeconds(duration as nullable duration)
- Trace(
    traceLevel as number,
    message as anynonnull,
    value as any,
    optional delayed as nullable logical
)
- Trace(TraceLevel.Information, "TextValueFromNumber", ()
- Traits(value as any)
- Transform(
        BinaryFormat.Byte,
        (x)
- Transform(Source, Text.Lower)
- Transform(Source, Text.Proper)
- Transform(Source, Text.Upper)
- Transform(Source, each Date.Year(_)
- Transform(binaryFormat as function, function as function)
- Transform(columnTypes, (t)
- Transform(cube as table, transforms as list)
- Transform(dateValues, (dateValue)
- Transform({1, 2}, each _ + 1)
- TransformColumnNames(
    Table.FromRecords({[ColumnNum = 1, cOlumnnum = 2, coLumnNUM = 3]})
- TransformColumnNames(
    table as table,
    nameGenerator as function,
    optional options as nullable record
)
- TransformColumnNames(Table.FromRecords({[#"Col#(tab)
- TransformColumnTypes(
        Source,
Output
Power Query M
Transform the dates in the table to their German text equivalents, and the values in the table to
percentages.
Usage
Power Query M
Output
Power Query M
        {"Date", type text},
        "fr-FR"
    )
- TransformColumnTypes(
        Source, 
        {"a", type text}
    )
- TransformColumnTypes(
        Source, 
        {{"Date", type text}, {"Value", Percentage.Type}},
        "de-DE")
- TransformColumnTypes(
        ToTable, {{"Country", type text}, {"Date", type date}, {"Value", 
Int64.Type}}
    )
- TransformColumnTypes(
    table as table,
    typeTransformations as list,
    optional culture as nullable text
)
- TransformColumnTypes(FormatFixedNow, 
        {{"Index", Int64.Type}, {"LocalNow", type text}, {"FixedLocalNow", type 
text}})
- TransformColumnTypes(FormatFixedNow, 
        {{"Index", Int64.Type}, {"UtcNow", type text}, {"FixedUtcNow", type 
text}})
- TransformColumnTypes(FormatFixedNow, {{"Index", 
Int64.Type}, 
        {"LocalNow", type text}, {"FixedLocalNow", type text}})
- TransformColumns(
        Source, 
        {"Posted Date", each Date.From(_, "de-DE")
- TransformColumns(
        Source, 
        {"Posted Date", each Date.FromText(_, [Culture = "it-IT"])
- TransformColumns(
        Table.SelectRows(Source, each [Country] = "France")
- TransformColumns(
    Table.FromRecords({
        [A = "1", B = 2],
        [A = "5", B = 10]
    })
- TransformColumns(
    table as table,
    transformOperations as list,
    optional defaultTransformation as nullable function,
    optional missingField as nullable number
)
- TransformColumns(#"Customer Case", {"FRUIT", 
Text.Proper})
- TransformColumns(#"Ignore cluster case",
        {"Cluster", Text.Lower}
    )
- TransformColumns(FormatLocalNow, 
        {{"FixedLocalNow", each DateTime.ToText(_, "yyyy-MM-ddThh:mm:ss.fff")
- TransformColumns(FormatLocalNow, 
        {{"FixedLocalNow", each DateTimeZone.ToText(_, "yyyy-MM-
ddThh:mm:ss.fff:zzz")
- TransformColumns(FormatLocalNow, 
        {{"FixedUtcNow", each DateTimeZone.ToText(_, "yyyy-MM-
ddThh:mm:ss.fff:zzz")
- TransformColumns(Orders, {"Item", 
Text.Proper})
- TransformColumns(Source, {"Account Name", each 
Text.TrimEnd(_, {"*", "@"})
- TransformColumns(Source, {"Account Name", each 
Text.TrimStart(_, {"*", "@"})
- TransformColumns(Source, {"CUSTOMER", Text.Lower})
- TransformColumns(Source, {"CUSTOMER", Text.Proper})
- TransformColumns(Source, {"FRUIT", Text.Upper})
- TransformColumns(Source, {"Sales Status", each 
Text.Trim(_, {"#", "@"})
- TransformColumns(TableWithTimes, 
        {{"LocalNow", each DateTime.ToText(_, "yyyy-MM-ddThh:mm:ss.fff")
- TransformColumns(TableWithTimes, 
        {{"LocalNow", each DateTimeZone.ToText(_, "yyyy-MM-
ddThh:mm:ss.fff:zzz")
- TransformColumns(TableWithTimes, 
        {{"UtcNow", each DateTimeZone.ToText(_, "yyyy-MM-ddThh:mm:ss.fff:zzz")
- TransformFields(
    [OrderID = "1", CustomerID = 1, Item = "Fishing rod", Price = "100.0"],
    {{"OrderID", Number.FromText}, {"Price", Number.FromText}}
)
- TransformFields(
    [OrderID = 1, CustomerID = 1, Item = "Fishing rod", Price = "100.0"],
    {"Price", Number.FromText}
)
- TransformFields(record as record, transformOperations as list, optional 
missingField as nullable number)
- TransformMany(
    {
        [Name = "Alice", Pets = {"Scruffy", "Sam"}],
        [Name = "Bob", Pets = {"Walker"}]
    },
    each [Pets],
    (person, pet)
- TransformMany(list as list, collectionTransform as function, resultTransform 
as function)
- TransformRows(
    Table.FromRecords({
        [a = 1],
        [a = 2],
        [a = 3],
        [a = 4],
        [a = 5]
    })
- TransformRows(table as table, transform as function)
- Transpose(
    Table.FromRecords({
        [Name = "Full Name", Value = "Fred"],
        [Name = "Age", Value = 42],
        [Name = "Country", Value = "UK"]
    })
- Transpose(table as table, optional columns as any)
- Trim("     a b c d    ")
- Trim("0000056.4200", "0")
- Trim("<div/>", {"<", ">", "/"})
- Trim(text as nullable text, optional trim as any)
- TrimEnd("     a b c d    ")
- TrimEnd("03.487700000", "0")
- TrimEnd(text as nullable text, optional trim as any)
- TrimStart("   a b c d    ")
- TrimStart("0000056.420", "0")
- TrimStart(text as nullable text, optional trim as any)
- Type( 1 as number )
- Type( 2 )
- Type( Value.ReplaceType( {1}, type {number} )
- Type( [ X = 1, Y = 2 ] )
- Type( {2} )
- Type(#datetime(2010, 12, 31)
- Type(243.448)
- Type(42 as nullable number)
- Type([a = 1, b = 2])
- Type(null as nullable number)
- UTC (for example, +01:00, -07:00)
- UTC (the GMT timezone)
- Union(types as list)
- Union({{1..5}, {2..6}, {3..7}})
- Unpivot(
    Table.FromRecords({
        [key = "x", a = 1, b = null, c = 3],
        [key = "y", a = 2, b = 4, c = null]
    })
- Unpivot(
    table as table,
    pivotColumns as list,
    attributeColumn as text,
    valueColumn as text
)
- UnpivotOtherColumns(
    Table.FromRecords({
        [key = "key1", attribute1 = 1, attribute2 = 2, attribute3 = 3],
        [key = "key2", attribute1 = 4, attribute2 = 5, attribute3 = 6]
    })
- UnpivotOtherColumns(
    table as table,
    pivotColumns as list,
    attributeColumn as text,
    valueColumn as text
)
- UnsignedInteger16(binary as binary)
- UnsignedInteger32(binary as binary)
- UnsignedInteger64(binary as binary)
- Upper("The quick brown fox jumps over the lazy dog.")
- Upper("aBcD")
- Upper(text as nullable text, optional culture as nullable text)
- UriUnescapeDataString("%2Bmoney%24")
- Value(identifier as text)
- Value(value as any, path as text)
- ValueOrDefault(identifier as text, optional defaultValue as any)
- VersionIdentity(value as any)
- Versions()
- Versions(value as any)
- View(
    null,
    [
        GetLength = ()
- View(
    null,
Output
Table.FromRecords({[CustomerID = 1, Name = "Bob", Phone = "123-4567"]})
- View(binary as nullable binary, handlers as record)
- View(table as nullable table, handlers as record)
- ViewError(errorRecord as record)
- ViewFunction(function as function)
- WeekOfMonth(#date(2011, 03, 15)
- WeekOfMonth(dateTime as any, optional firstDayOfWeek as nullable number)
- WeekOfYear(#date(2011, 03, 27)
- WeekOfYear(dateTime as any, optional firstDayOfWeek as nullable number)
- WithErrorContext(action as action, context as text)
- WithErrorContext(value as any, context as text)
- Workbook(File.Contents("C:\Book1.xlsx")
- Workbook(File.Contents("C:\myfile.xlsx",
true, true)
- Workbook(File.Contents("C:\myfile.xlsx", [UseHeaders = true],
Return the contents of Sheet1 from an Excel workbook.
Usage
Power Query M
Output
Power Query M
null)
- Workbook(workbook as binary, optional useHeaders as any, optional delayTypes 
as nullable logical)
- Year(#datetime(2011, 12, 31, 9, 15, 36)
- Year(dateTime as any)
- Zip({{1, 2}, {3, 4}})
- Zip({{1, 2}, {3}})
- ZoneHours(#datetimezone(2024, 4, 28, 13, 24, 22, 7, 30)
- ZoneHours(dateTimeZone as nullable datetimezone)
- ZoneMinutes(#datetimezone(2024, 4, 28, 13, 24, 22, 7, 30)
- ZoneMinutes(dateTimeZone as nullable datetimezone)
- _
(underscore)
- _  ( U+005F )
- _  (for details, see Simplified
[A=1,B=2][B]       // 2 
[A=1,B=2][C]       // error 
[A=1,B=2][C]?      // null
[A=1,B=2][[B]]           // [B=2] 
[A=1,B=2][[C]]           // error 
[A=1,B=2][[B],[C]]?      // [B=2,C=null]
[A]                 
_[A]
let _ = [A=1,B=2] in [A] //1
[[A],[B]]                 
_[[A],[B]]
declarations)
- _  (underscore)
- _ (U+005F)
- a  (ignoring
concurrency here for simplicity)
- affected (unless they access an entry previously marked as having an
error)
- alternative (eg.
MissingField.UseNull or MissingField.Ignore)
- alternative (eg. MissingField.UseNull or MissingField.Ignore)
- alternative (for example,
MissingField.UseNull or MissingField.Ignore)
- and
(fractional)
- and (N <= (Fixed + Optional)
- and (fractional)
- any
(22)
- any
(23)
- apples ( ApPlE  and APPLE )
- as (_)
- available (for security
Syntax
About
reasons)
- available (for security reasons)
- backslash ( \"" )
- backslash ( \' )
- backslash ( \\ )
- base (for example, base-2 or base-10)
- behavior
(for example, MissingField.UseNull or MissingField.Ignore)
- behavior (for example, MissingField.UseNull or MissingField.Ignore)
- binary  (or the resulting view in the case of GetExpression )
- binary (list of number )
- binary( {0x00, 0x01, 0x02, 0x03} )
- binary("1011")
- binary("AQID")
- binary(16)
- binary(value as any)
- binary({
        0x00, 0x01,
        0x00, 0x00, 0x00, 0x02
    })
- binary({
        1, 101,
        1, 102
    })
- binary({
        1, 11,
        2, 22,
        2, 22,
        5, 55,
        1, 11
    })
- binary({0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10})
- binary({0x30, 0x31, 0x32})
- binary({1, 2, 3})
- binary({1})
- binary({2, 3, 4, 5})
- binary({2, 65, 66})
- binary({227, 226, 26, 5, 163, 96, 20, 12, 119, 0, 0})
- binary({6, 7, 8, 9, 10})
- binary({6, 7})
- binary({65, 66, 67})
- binary({71, 0, 111, 0, 111, 0, 100, 0, 98, 0, 121, 0, 101, 0})
- bit (eight-byte)
- bit (four-byte)
- bit (one-byte)
- bit (two-byte)
- blanks ( U+0020 )
- blanks (U+0020)
- boundaries
(when false)
- boundaries
(when true)
- boundary (for
example, just before or after midnight, the start of a new month, or a new year)
- by (  ( U+0028 )
- by ( (U+0028)
- case (ABC)
- case (Abc)
- case (abc)
- casings ("Redmond", "redmond", and
"REDMOND")
- catch ()
- catch (e)
- char(36)
- character ( U+0009 )
- character ( U+000A )
- character ( U+000B )
- character ( U+000C )
- character ( U+000D )
- character ( U+0085 )
- character ( U+2028 )
- character ( U+2029 )
- character (-1 if not found)
- character (U+0009)
- character (U+000A)
- character (U+000B)
- character (U+000C)
- character (U+000D)
- character (U+001A)
- character (U+0085)
- character (U+2028)
- character (U+2029)
- character (which is part of Unicode class Zs)
- character (‰ or \u2030)
- characters
(where each Unicode character is two bytes)
- characters (such a
0)
- collection (default is "NULLID")
- column (for example,
Splitter.SplitTextByDelimiter or Splitter.SplitTextByPositions)
- column (when applicable)
- column(s)
- columns  (and delimiter , extraValues , and encoding  are null)
- columns (and their values)
- columns (i.e. the
schema)
- columns (if false)
- columns (if true)
- columns (that is, the
schema)
- columns (which are identified by name)
- combinations (of any length)
- conversion (default)
- culture  (Optional)
- culture (in this case, the en-
US culture)
- database (if true)
- databases (if false)
- datatype (or
include null, which always compares smallest)
- date
("D")
- date
("d")
- date ("D")
- date ("d")
- date (no time portion)
- date(
    year as number,
    month as number,
    day as number
)
- date(1899, 12, 30)
- date(1975, 4, 4)
- date(1979, 11, 20)
- date(1980, 1, 1)
- date(2010, 12, 30)
- date(2010, 12, 31)
- date(2010,01,15)
- date(2010,01,31)
- date(2010,05,20)
- date(2011, 1, 2)
- date(2011, 1, 3)
- date(2011, 10, 14)
- date(2011, 12, 01)
- date(2011, 12, 31)
- date(2011, 5, 14)
- date(2011, 5, 19)
- date(2011, 5, 28)
- date(2011, 5, 31)
- date(2011, 8, 14)
- date(2012, 01, 01)
- date(2012, 1, 1)
- date(2012, 1, 2)
- date(2012, 1, 3)
- date(2012, 1, 4)
- date(2013,02,26)
- date(2015, 5, 14)
- date(2020, 3, 20)
- date(2021, 1, 14)
- date(2021, 11, 28)
- date(2021, 12, 31)
- date(2021, 5, 10)
- date(2021, 7, 6)
- date(2021, 7, 6)
- date(2022, 1, 12)
- date(2022, 12, 14)
- date(2022, 12, 31)
- date(2022, 2, 25)
- date(2022, 4, 8)
- date(2022, 6, 28)
- date(2022,1,12)
- date(2022,12,14)
- date(2023, 1, 12)
- date(2023, 1, 14)
- date(2023, 12, 14)
- date(2023, 12, 2)
- date(2023, 12, 26)
- date(2023, 12, 31)
- date(2023, 4, 14)
- date(2023, 6, 1)
- date(2023, 6, 2)
- date(2023, 6, 4)
- date(2023, 7, 1)
- date(2023, 7, 15)
- date(2023, 7, 18)
- date(2023, 8, 1)
- date(2023,4,14)
- date(2023,6,4)
- date(2023,7,18)
- date(2024, 1,18)
- date(2024, 10, 2)
- date(2024, 10, 5)
- date(2024, 11, 28)
- date(2024, 2, 23)
- date(2024, 2, 25)
- date(2024, 3, 15)
- date(2024, 3, 20)
- date(2024, 5, 21)
- date(2024, 5, 30)
- date(2024, 6, 4)
- date(2024, 7, 18)
- date(2025, 7, 23)
- date(2025, 7, 24)
- date(2025, 7, 6)
- date(2035, 1, 2)
- date(year, month, day)
- datetime(
    year as number,
    month as number,
    day as number,
    hour as number,
    minute as number,
    second as number
)
- datetime( 2010, 5, 20, 8, 0, 0 )
- datetime(1899, 12, 30, 06, 45, 12)
- datetime(1975, 4, 4, 0, 0, 0)
- datetime(2000, 2, 8, 3, 45, 12)
- datetime(2008,12,15,04,19,19,03,00)
- datetime(2009, 12, 31, 16, 0, 0)
- datetime(2010, 10, 11, 0, 0, 0, 0, 0)
- datetime(2010, 12, 30, 2, 4, 50.36973)
- datetime(2010, 12, 31, 01, 30, 25)
- datetime(2010, 12, 31, 1, 30, 0)
- datetime(2010, 12, 31, 1, 30, 25)
- datetime(2010, 12, 31, 11, 56, 02)
- datetime(2010, 3, 2, 8, 0, 0)
- datetime(2010, 5, 19, 16, 0, 0)
- datetime(2010, 5, 20, 16, 30, 0, -8, 0)
- datetime(2010,05,20,12,00,00,-08)
- datetime(2010,05,20,16,06,00,-08,00)
- datetime(2010,10,10,0,0,0,0)
- datetime(2011, 1, 1, 0, 0, 0)
- datetime(2011, 10, 1, 0, 0, 0)
- datetime(2011, 10, 10, 0, 0, 0)
- datetime(2011, 10, 10, 8, 0, 0)
- datetime(2011, 10, 9, 0, 0, 0)
- datetime(2011, 12, 31, 11, 56, 2)
- datetime(2011, 12, 31, 23, 55, 0)
- datetime(2011, 12, 31, 23, 56, 0)
- datetime(2011, 12, 31, 23, 57, 0)
- datetime(2011, 12, 31, 23, 58, 0)
- datetime(2011, 12, 31, 23, 59, 0)
- datetime(2011, 12, 31, 23, 59, 59.9999999)
- datetime(2011, 12, 31, 9, 15, 36)
- datetime(2011, 5, 14, 17, 59, 59.9999999)
- datetime(2011, 5, 14, 23, 59, 59.9999999)
- datetime(2012, 1, 1, 0, 0, 0)
- datetime(2012, 1, 1, 0, 1, 0)
- datetime(2012, 1, 1, 0, 2, 0)
- datetime(2012, 1, 1, 0, 3, 0)
- datetime(2012, 1, 1, 0, 4, 0)
- datetime(2012, 11, 14, 8, 15, 22)
- datetime(2012, 7, 24, 14, 50, 52.9842245)
- datetime(2013,02,26, 09,15,00)
- datetime(2013,02,26,09,17,00)
- datetime(2020, 3, 20, 6, 0, 0)
- datetime(2021, 5, 14, 8, 15, 22)
- datetime(2024, 12, 24, 14, 33, 20)
- datetime(2024, 6, 15, 13, 45, 0)
- datetime(2024, 6, 15, 13, 45, 30.90)
- datetime(2025, 7, 23, 12, 0, 0)
- datetime(2025, 7, 24, 10, 0, 0)
- datetime(2025, 7, 24, 12, 0, 0)
- datetime(2025, 7, 24, 14, 0, 0)
- datetime(2025, 7, 24, 22, 30, 0)
- datetime(2025, 7, 25, 13, 15, 0)
- datetime(year, month, day, hour, minute, second)
- datetimezone(
       year, month, day,
       hour, minute, second,
       offset-hours, offset-minutes)
- datetimezone(
    year as number,
    month as number,
    day as number,
    hour as number,
    minute as number,
    second as number,
    offsetHours as number,
    offsetMinutes as number
)
- datetimezone(2009, 6, 15, 13, 45, 30, -7, 0)
- datetimezone(2010, 12, 30, 2, 4, 50.36973, 2, 0)
- datetimezone(2010, 12, 31, 01, 30, 25, 2, 0)
- datetimezone(2010, 12, 31, 1, 30, 0, -8, 0)
- datetimezone(2010, 12, 31, 11, 56, 02, 7, 30)
- datetimezone(2010, 12, 31, 11, 56, 2, 7, 30)
- datetimezone(2010, 12, 31, 12, 26, 2, -8, 0)
- datetimezone(2010, 12, 31, 12, 26, 2, 8, 0)
- datetimezone(2010, 12, 31, 3, 56, 2, 0, -30)
- datetimezone(2010, 12, 31, 4, 26, 2, 0, 0)
- datetimezone(2011, 12, 31, 11, 56, 2, 8, 0)
- datetimezone(2011, 12, 31, 23, 55, 0, -8, 0)
- datetimezone(2011, 12, 31, 23, 56, 0, -8, 0)
- datetimezone(2011, 12, 31, 23, 57, 0, -8, 0)
- datetimezone(2011, 12, 31, 23, 58, 0, -8, 0)
- datetimezone(2011, 12, 31, 23, 59, 0, -8, 0)
- datetimezone(2011, 12, 31, 23, 59, 59.9999999, -7, 0)
- datetimezone(2011, 12, 31, 9, 15, 36, -7, 0)
- datetimezone(2011, 5, 17, 23, 59, 59.9999999, -7, 0)
- datetimezone(2011, 5, 17, 5, 59, 59.9999999, -7, 0)
- datetimezone(2011, 5, 21, 23, 59, 59.9999999, -7, 0)
- datetimezone(2011, 5, 31, 23, 59, 59.9999999, -7, 0)
- datetimezone(2011, 8, 16, 23, 34, 37.745, 0, 0)
- datetimezone(2012, 1, 1, 0, 0, 0, -8, 0)
- datetimezone(2012, 1, 1, 0, 1, 0, -8, 0)
- datetimezone(2012, 1, 1, 0, 2, 0, -8, 0)
- datetimezone(2012, 1, 1, 0, 3, 0, -8, 0)
- datetimezone(2012, 1, 1, 0, 4, 0, -8, 0)
- datetimezone(2012, 7, 24, 14, 50, 52.9842245, -7, 0)
- datetimezone(2013,02,26, 09,15,00, 09,00)
- datetimezone(2020, 10, 30, 01, 30, 00, -8, 00)
- datetimezone(2024, 4, 10, 6, 30, 0, -7, 0)
- datetimezone(2024, 6, 15, 13, 45, 30, 0, 0)
- datetimezone(2025, 7, 23, 
10, 30, 0, 4, 0)
- datetimezone(2025, 7, 24, 12, 0, 0, 7, 0)
- day (#duration(1, 0, 0, 0)
- ddd(.hh:mm(:ss(.ff)
- default (or current)
- digit (0-9)
- digits (0-
9)
- distinct (i.e. no duplicates)
- duration(
    days as number,
    hours as number,
    minutes as number,
    seconds as number
)
- duration( 30,08,00,00)
- duration(-1,0,0,0)
- duration(-16,00,00,00)
- duration(0, 
0, 0, 0.2)
- duration(0, 
0, 1, 0)
- duration(0, -6, -30, 0)
- duration(0, 0, 
0, 0.2)
- duration(0, 0, 0, 
0.2)
- duration(0, 0, 0, -5.5)
- duration(0, 0, 0, 1)
- duration(0, 0, 0, 1.75)
- duration(0, 0, 0, 2)
- duration(0, 0, 0, 5.5)
- duration(0, 0, 1, 0)
- duration(0, 0, 2, 0)
- duration(0, 0, 29, 30)
- duration(0, 0, 5, -30)
- duration(0, 0, 5, 30)
- duration(0, 0, 54, 40)
- duration(0, 1, 0, 0)
- duration(0, 12, 0, 0)
- duration(0, 18, 0, 0)
- duration(0, 2, 0, 0)
- duration(0, 22, 30, 0)
- duration(0, 23, 59, 59)
- duration(0, 24, 0, 0)
- duration(0, 3, 0, 0)
- duration(0, 3, 30, 0)
- duration(0, 4, 0, 0)
- duration(0, 5, 0, 0)
- duration(0,-1,-30,0)
- duration(0,0,0,30.45)
- duration(0,0,2,0)
- duration(0,04,30,00)
- duration(0,1,30,0)
- duration(0,1,30,45.3)
- duration(0,8,0,0)
- duration(00,08,00,00)
- duration(1, 0, 0, 0)
- duration(1, 12, 0, 0)
- duration(1, 2, 0, 0)
- duration(1, 2, 29, 29.55)
- duration(1, 5, 30, 0)
- duration(1,0,0,0)
- duration(1,2,30,0)
- duration(16,00,00,00)
- duration(2, 12, 36, 0)
- duration(2, 2, 31, 0.4)
- duration(2, 3, 0, 0)
- duration(2, 5, 30, 0)
- duration(2, 5, 30, 45)
- duration(2, 5, 55, 20)
- duration(2, 5, 55, 20.242)
- duration(2, 5, 55, 20.3456700)
- duration(2,0,0,0)
- duration(2,1,0,15.1)
- duration(30,08,0,0)
- duration(30,5,0,0)
- duration(4, 2, 0, 30.2)
- duration(521,22,46,41)
- duration(<days>, <hours>, <minutes>,
<seconds>)
- duration(<days>, <hours>, <minutes>, <seconds>)
- e (2.7182...)
- elevation (Z)
- ellipsis
( ... )
- empty
(has no fields)
- empty (by having nothing between the
semicolons)
- empty (has no fields)
- environment ( B )
- environments (desktop vs. online)
- equivalent (for any type T )
- error
(x, y)
- evaluated (computed)
- exceeded (default is false)
- exponential ("E")
- expression
(x)
- expression (  argument-list
 )
- expression ( 1 + 1 )
- expression ( 2 + 2 )
- expression ( 2 > 1 )
- expression ( 4 )
- expression (1 + 1)
- expression (2 + 2)
- expression (2 > 1)
- expression (4)
- expression (in this case 2
+ 2 )
- expression (in this case 2 + 2)
- expression (informally known as a "try expression")
- expressions ( a  and b )
- expressions (Go to
Expressions, values, and let expression)
- expressions (as well as let expressions)
- f(42)
- f(b)
- fact (num-1)
- fact(5)
- fail (default is 2048)
- feed (U+000A)
- field (when using a
monospaced font)
- field(s)
- fields (selected by y1 , y2 , ... )
- following (in that both evaluate to equal
values)
- forms (d.h:m:s)
- function (  parameter-specification-list
 )
- function (X as number)
- function (optional x as nullable text)
- function (optional x as text)
- function (x as number, optional y as text)
- function (x as number, y as text)
- function (y as number, optional z as text)
- functions ( Value.Add , Value.Subtract , Value.Multiply , Value.Divide )
- general ("G")
- handled
("15", "3,423.10", "5.0E-10")
- headers (i.e. column names)
- headers (that is, as
column names)
- hex (255)
- hexadecimal ("X")
- hold (for any type T )
- hour
(#duration(0, 1, 0, 0)
- hours (maximum 23 hours)
- identifier
(SRID)
- identifier (GUID)
- identifier (SRID)
- if (y = null)
- infinity ( #infinity )
- infinity ( -#infinity )
- initial (if present)
- inner (more deeply nested)
- input (it will
never be called with the default value)
- instead ( '\'  displays \ )
- instead (except in the case of
GetExpression )
- instead (except in the case of GetExpression )
- interpreted (for example, "en-US")
- intrinsic (native)
- is (ConcurrentRequest * RequestSize)
- juin (fr-FR)
- juni (da-DK)
- key1  (for table1 )
- key2  (for table2 )
- keys (if
any)
- known (either because it is floating or not defined)
- language (informally
known as "M")
- length (up to MaxLength )
- level (or root)
- list (any two items, in any order)
- list ({1, 2, 5})
- list ({1, {1.1, 1.2}})
- list ({2, 3, 4})
- list ({3, 4})
- list( list )
- listFormat(binaryData)
- load (which is always done)
- locale (Windows, MacOS)
- locally (on Power Query Desktop)
- location ( each Table.RowCount(_)
- logical (that is, true  or false )
- logical (true/false)
- long (eight hex digits)
- lundi (fr-FR)
- measure (M)
- measure (cell property)
- meta (Value.Metadata(x)
- meta ([ Rating = 5 ] & [ Tags = {"Classical"} ])
- metadata (rather than
merge metadata into possibly existing metadata)
- minute (#duration(0, 0, 1, 0)
- minutes (maximum
59 minutes)
- mm(:ss(.ff)
- month
("M", "m")
- month ("M", "m")
- month ("Y")
- month ("Y", "y")
- name (not its value)
- name (not the value)
- names (default is false)
- names (default is true)
- nan  (NaN—Not a Number)
- noon (#time(12, 0, 0)
- normalization (such as group expansion)
- not (true and true)
- not (x <> y)
- null
(24)
- null
(25)
- nullable ( Type.ForList({type number})
- nullable (Type.NonNullable(type T)
- number
(NaN)
- number  (exponential function)
- number (0, 1 or 2)
- number (14 or 15)
- number (3 or 4)
- number (from 0 to 6)
- number (n)
- number (using RoundingMode.ToEven, also known as "banker's rounding")
- numeric ("N")
- objects (for
example, dimensions and measures)
- objects (for example, dimensions and
measures)
- occur (up to the level where they are handled by a try expression)
- of ()
- offset(s)
- offsets (although this adjustment
can be brittle, for example, due to daylight savings time or regional settings)
- one(s)
- online (UTC)
- online (on Power Query Online)
- operations (for example, to download a section of a file)
- operator ( & )
- operator ( + )
- operator ( +x )
- operator ( -x )
- operator ( @ )
- operator ( [] )
- operator ( not )
- operator ( x & y )
- operator ( x * y )
- operator ( x + y )
- operator ( x - y )
- operator ( x / y )
- operator ( x meta y )
- operator ( {} )
- operator (&)
- operator (+)
- operator ([ ])
- operator ({ })
- operators ( + , - , * , / )
- operators (In addition to Common operators)
- option (if available)
- or ( Culture = "" )
- order ( {each 1 / _, Order.Descending} )
- other (linked)
- others (such as (type [a = text])
- parameter ( value )
- parameter (_)
- parameters (by name)
- parts (hour, minute, second)
- parts (year, month, day)
- parts (year, month, day, hour,
minute, second)
- pattern (long
time)
- pattern (short
time)
- percent ("%")
- percent ("P")
- placeholder ( # )
- placeholders (0 or #)
- places (Rounding down)
- places (Rounding up)
- point ("F")
- points (2)
- position
(end - countOrCondition )
- position (go to Example 3 - Get a row from a table by index position)
- position (or match)
- position(s)
- precision (if necessary)
- prices ("each
List.Sum([price])
- primitive (or nullable primitive)
- production (https://login.salesforce.com
)
- provided
(for example, "en-US")
- provided (for
example, "en-US")
- provided (for example,
"en-US")
- provided (for example, "en-
US")
- provided (for example, "en-US")
- queries (for example, to create T-SQL statements from M queries)
- quote ( "" )
- quoteStyle  (and includeLineSeparators  and encoding  are null )
- quoteStyle  (and includeLineSeparators  is null )
- record  (the empty open record type)
- recordFormat(binaryData)
- requested (by lookup or index operators)
- return
(first occurrence by default)
- return (U+000D)
- returned (Not a number)
- row(s)
- rows (i.e. the table
is empty)
- rows (no duplicates)
- rows (starting at the bottom)
- rows (starting at the top)
- runs (desktop vs. online)
- seconds (3.33 ms)
- seconds (maximum 59.9999999 seconds)
- semicolon (;)
- separator (U+2028)
- separator (U+2029)
- server (default is null)
- sets (of any length)
- short (four hex digits)
- sign (%)
- sign (+)
- sign (-)
- signature (x as any)
- signature (x as any, y as any)
- sortable
("s")
- sortable ("s")
- sortable ("u")
- source
(for example, nvarchar  for SQL Server)
- source (for example, 42  or newid()
- sources (known
as folding)
- sources (such as SQL Server)
- specified (or current document locale)
- specifier (C)
- specifier (D)
- specifier (E)
- specifier (F)
- specifier (G)
- specifier (N)
- specifier (P)
- specifier (X)
- specifier (and the "yyyy'-'MM'-
'dd'T'HH':'mm':'ss'.'fffffffxxx" custom format)
- specifier (plus any number of additional "H" specifiers)
- specifier (plus any number of additional "d" specifiers)
- specifier (plus any number of additional "h" specifiers)
- specifier (plus any number of additional "m" specifiers)
- specifier (plus any number of additional "s" specifiers)
- specifier (plus any number of additional "t" specifiers)
- specifier (plus any number of additional "y" specifiers)
- specifiers (plus any number of additional "g" specifiers)
- standard (ISO 8601)
- state (such as the current time or the results of a query
against a database that evolves over time)
- string ("")
- string (default is false)
- string (that is, to use the "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z",
":", or "/" custom format specifier by itself)
- strings (that is, format strings that don't contain scientific
notation format characters)
- symbol (...)
- system (for example, "en-US")
- t
(26)
- table  (as specified by
count )
- table  (or the resulting view in the case of GetExpression )
- table (Table.FromRecords({[a = 1, b = 2], [a = 3, b = 4]})
- table (list of records)
- table (type table [Account Code = text, Posted Date = date, Sales = number],
{
    {"US-2004", #date(2023, 1, 20)
- table ({ [ key = "x", attribute =
"a", value = 1 ], [ key = "x", attribute = "c", value = 3 ], [ key = "y", attribute =
"a", value = 2 ], [ key = "y", attribute = "b", value = 4 ] })
- table ({[ key = "x", a = 1, b = null, c = 3 ], [ key
= "y", a = 2, b = 4, c = null ]})
- table ({[a = "A", b = "a"], [a = "B", b =
"a"], [a = "A", b = "b"]})
- table ({[a = 1, b = 2],
[a = 3, b = 4]})
- table ({[a = 1, b = 2], [a
= 3, b = 4]})
- table ({[a = 1, b = 2], [a = 3, b = 4], [a = 1, b =
6]})
- table ({[a = 1, b = 2], [a = 3, b = 4]})
- table ({[a = 2,
b = 4], [a = 6, b = 8], [a = 2, b = 4], [a = 1, b = 4]} .
Usage
Power Query M
Output
{0, 1, 2}
Equation criteria
Example 2
Table.PositionOfAny(
    Table.FromRecords({
        [a = 2, b = 4],
        [a = 6, b = 8],
        [a = 2, b = 4],
        [a = 1, b = 4]
    })
- table ({[a = 2,
b = 4], [a = 6, b = 8], [a = 2, b = 4], [a = 1, b = 4]})
- table ({[a = 2, b = 4],
[a = 6, b = 8]})
- table ({[a = 2, b = 4], [a
= 6, b = 8], [a = 2, b = 4], [a = 1, b = 4]})
- table ({[a = 2, b = 4], [a = 6,
b = 8], [a = 2, b = 4], [a = 1, b = 4]})
- table ({[a = 2, b = 4], [a = 6, b =
8]})
- table ({[a = 2, b = 4], [a = 6, b = 8], [a = 2, b = 4], [a = 1, b = 4]})
- table ({[a = [aa = 1, bb = 2, cc = 3], b = 2]})
- table ({[saleID = 1, price = 20], [saleID = 2, price = 10]})
- table ({[t = {[a=1, b=2, c=3], [a=2,b=4,c=6]}, b = 2]})
- table ({})
- table(
        type table [Column1 = text, Column2 = text],
        {{"a", "b"}, {"c", "d,e,f"}}
    )
- table(
        {"OrderID", "CustomerID", "Item", "Price"},
        {
            {1, 1, "Fishing rod", 100.00},
            {2, 1, "1 lb. worms", 5.00}
        }
    )
- table(
    type table [Digit = number, Name = text],  
    {{1,"one"}, {2,"two"}, {3,"three"}} 
    )
- table(
    type table [Merged = text],
    {{"a,b"}, {"c,""d,e,f"""}}
)
- table(
    type table [Name = text, Score = number],
    {{"Betty", 90.3}, {"Carl", 89.5}}
)
- table(
    type table [OrderID = number, CustomerID = number, Item = text, Price = 
number],
        {
            {1, 1, "Fishing rod", 100.00},
            {2, 1, "1 lb. worms", 5.00}
         }
    )
- table(
    type table [OrderID = number, CustomerID = number, Item = text, Price = 
number],
        {
            {1, 1, "Fishing rod", 100.00},
            {2, 1, "1 lb. worms", 5.00}
        }
    )
- table( {"A", "B"}, { {1, 2}, {3, 4} } )
- table(2, {{"Betty", 90.3}, {"Carl", 89.5}})
- table(columns as any, rows as any)
- table(null, {{"Betty", 90.3}, {"Carl", 89.5}})
- table(type table [Account Code = text, Posted Date = date, Sales = 
number],
    {
        {"US-2004", #date(2023,1,20)
- table(type table [Account Code = text, Posted Date = date, Sales = number],
{
    {"CA-8843", #date(2023,7,18)
- table(type table [Account Code = text, Posted Date = date, Sales = number],
{
    {"US-2004", #date(2023, 1, 20)
- table(type table [Account Code = text, Posted Date = text, Sales = 
number],
    {
        {"US-2004", "20 Januar 2023", 580},
        {"CA-8843", "18 Juli, 2023", 280},
        {"PA-1274", "12 Januar, 2022", 90},
        {"PA-4323", "14 April 2023", 187},
        {"US-1200", "14 Dezember, 2022", 350},
        {"PTY-507", "4 Juni, 2023", 110}
    })
- table(type table [Account Code = text, Posted Date = text, Sales = 
number],
    {
        {"US-2004", "20 gen. 2023", 580},
        {"CA-8843", "18 lug. 2024", 280},
        {"PA-1274", "12 gen. 2023", 90},
Output
Power Query M
How culture affects text formatting
Standard date and time format strings
Custom date and time format strings
        {"PA-4323", "14 apr. 2023", 187},
        {"US-1200", "14 dic. 2023", 350},
        {"PTY-507", "4 giu. 2024", 110}
    })
- table(type table [CUSTOMER = text, FRUIT = text],
    {
        {"Tulga", "Squash"}, 
        {"suSanna", "Pumpkin"}, 
        {"LESLIE", "ApPlE"}, 
        {"Willis", "pear"}, 
        {"Dilbar", "orange"}, 
        {"ClaudiA", "APPLE"}, 
        {"afonso", "Pear"}, 
        {"SErgio", "pear"}
    })
- table(type table [CUSTOMER = text, FRUIT = text], 
    {
        {"Tulga", "Squash"}, 
        {"suSanna", "Pumpkin"}, 
        {"LESLIE", "ApPlE"}, 
        {"Willis", "PEAR"}, 
        {"Dilbar", "orange"}, 
        {"ClaudiA", "APPLE"}, 
        {"afonso", "Pear"}, 
        {"SErgio", "peAR"}
        })
- table(type table [CUSTOMER = text, FRUIT = text], 
    {
        {"Tulga", "Squash"}, 
        {"suSanna", "Pumpkin"}, 
        {"LESLIE", "ApPlE"}, 
        {"Willis", "pear"}, 
        {"Dilbar", "orange"}, 
        {"ClaudiA", "APPLE"}, 
        {"afonso", "Pear"}, 
        {"SErgio", "pear"}
    })
- table(type table [CUSTOMER = text, FRUIT = text], 
    {
        {"Tulga", "Squash"}, 
        {"suSanna", "Pumpkin"}, 
        {"LESLIE", "ApPlE"}, 
        {"Willis", "pear"}, 
        {"Dilbar", "orange"}, 
        {"ClaudiA", "APPLE"}, 
This code produces the following output:
The following example demonstrates how to change all items in both of the table columns to
proper case.
Power Query M
        {"afonso", "Pear"}, 
        {"SErgio", "pear"}
    })
- table(type table [Company ID = text, Country = text, Date = date],
    {
        {"JS-464", "USA", #date(2024, 3, 24)
- table(type table [Company ID = text, Country = text, Date = text],
    {
        {"JS-464", "USA", "24/03/2024"},
        {"LT-331", "France", "05/10/2024"},
        {"XE-100", "USA", "21/05/2024"},
        {"RT-430", "Germany", "18/01/2024"},
        {"LS-005", "France", "31/12/2023"},
        {"UW-220", "Germany", "25/02/2024"}
    })
- table(type table [Company ID = text, Country = text, Date = text],
{
    {"LT-331", "France", "05/10/2024"},
    {"LS-005", "France", "31/12/2023"}
})
- table(type table [Date = date, Customer ID = text, Value = number],
    {
        {#date(2024, 3, 12)
- table(type table [Date = text, Customer ID = text, Value = Percentage.Type],
{
    {"12.03.2024", "134282", .24368},
    {"30.05.2024", "44343", .03556},
    {"14.12.2023", "22", .3834}
})
- table(type table [First Name = text, Last Name = text, Email Address = text],
{
    {"Douglas", "Elis", "DougEli@contoso.com"},
    {"Ana", "Jorayew", "AnaJor@contoso.com"},
    {"Rada", "Mihaylova", "RadaMih@contoso.com"}
})
- table(type table [First Name = text, Last Name = text],
    {
        {"Douglas", "Elis"},
        {"Ana", "Jorayew"},
        {"Rada", "Mihaylova"}
    })
- table(type table [Fruit = text], {{"blueberries"}, 
        {"Blue berries are simply the best"}, {"strawberries"}, {"Strawberries = 
<3"}, 
This code produces the following output:
Lists and tables can both be sorted using either List.Sort or Table.Sort, respectively. However,
sorting text depends on the case of the associated items in the list or table to determine the
actual sort order (either ascending or descending)
- table(type table [Home Sale = text, Sales Date = date, Sales Status 
= text],
    {
        {"1620 Ferris Way", #date(2024, 8, 22)
- table(type table [Home Sale = text, Sales Date = date, Sales Status = text],
    {
        {"1620 Ferris Way", #date(2024, 8, 22)
- table(type table [Name = text, Account Name = text, Interest = number],
    {
        {"Bob", "847263-US", 2.841},
        {"Leslie", "4648-FR", 3.8392},
        {"Ringo", "2046790-DE", 12.66}
    })
- table(type table [Name = text, Account Name = text, Interest = number],
    {
        {"Bob", "US-847263", 2.841},
        {"Leslie", "FR-4648", 3.8392},
        {"Ringo", "DE-2046790", 12.66}
    })
- table(type table [Name = text, Account Name= text, Interest = 
number],
    {
        {"Bob", "@****847263-US", 2.8410},
        {"Leslie", "@******4648-FR", 3.8392},
        {"Ringo", "@*****24679-DE", 12.6600}
    })
- table(type table [Name = text, Account Name= text, Interest = 
number],
    {
        {"Bob", "US-847263****@", 2.8410},
        {"Leslie", "FR-4648****@**", 3.8392},
        {"Ringo", "DE-2046790@***", 12.6600}
    })
- table(type table [Name = text, Score = number], {{"Betty", 90.3}, {"Carl", 
89.5}})
- table(type table [a = number, b = number],
    {
        {1, 2},
        {3, 4}
    })
- table(type table [a = text, b = number],
{
    {"1", 2},
    {"3", 4}
})
- table(type table rowType, {{"Betty", 90.3}, {"Carl", 89.5}})
- table(type table[CUSTOMER = text, FRUIT = text],
    {
        {"Tulga", "Squash"}, 
        {"suSanna", "Pumpkin"}, 
        {"LESLIE", "ApPlE"}, 
        {"Willis", "pear"}, 
        {"Dilbar", "orange"}, 
        {"ClaudiA", "APPLE"}, 
        {"afonso", "Pear"}, 
        {"SErgio", "pear"}
    })
- table(type table[Country = text, Date = date, Value = Int64.Type],
    {
        {"USA", #date(2023, 8, 1)
- table(type table[CustomerID = number, First Name = text, Last Name = text, Phone 
= text],
{
    {1, "Bob", "White", "123-4567"},
    {2, "Jim", "Smith", "987-6543"},
    {3, "Paul", "-No Entry-", "543-7890"},
Split the name column into first name and last name, then rename the new columns. Because
there might be more values than the number of available columns, make the last name column
a list that includes all values after the first name.
Usage
Power Query M
Output
Power Query M
    {4, "Cristina", "Best", "232-1550"}
})
- table(type table[CustomerID = number, First Name = text, Last Name = text, Phone 
= text],
{
    {1, "Bob", "White", "123-4567"},
    {2, "Jim", "Smith", "987-6543"},
    {3, "Paul", null, "543-7890"},
    {4, "Cristina", "Best", "232-1550"}
})
- table(type table[CustomerID = number, First Name = text, Last Name = text, Phone 
= text],
{
    {1, "Bob", {"White"}, "123-4567"},
    {2, "Jim", {"Smith"}, "987-6543"},
    {3, "Paul", {"Green"}, "543-7890"},
    {4, "Cristina", {"J.", "Best"}, "232-1550"}
})
- table(type table[CustomerID = number, Name = text, Phone = text],
    {
        {1, "Bob White", "123-4567"},
        {2, "Jim Smith", "987-6543"},
        {3, "Paul Green", "543-7890"},
        {4, "Cristina J. Best", "232-1550"}
    })
- table(type table[CustomerID = number, Name = text, Phone = text],
    {
        {1, "Bob White", "123-4567"},
        {2, "Jim Smith", "987-6543"},
        {3, "Paul", "543-7890"},
        {4, "Cristina Best", "232-1550"}
    })
- table(type table[CustomerID = number, Name = text, Phone = text],
Output
Power Query M
Split the name column into first name and last name, then rename the new columns.
Usage
Power Query M
    {
        {1, "Bob White", "123-4567"},
        {2, "Jim Smith", "987-6543"},
        {3, "Paul", "543-7890"},
        {4, "Cristina Best", "232-1550"}
    })
- table(type table[CustomerID = number, Name.1 = text, Name.2 = text, Phone = 
text],
{
    {1, "Bob", "White", "123-4567"},
    {2, "Jim", "Smith", "987-6543"},
    {3, "Paul", null, "543-7890"},
    {4, "Cristina", "Best", "232-1550"}
})
- table(type table[StartTime = datetime, Seconds = Int64.Type],
    {
        {#datetime(2025, 7, 25, 8, 0, 0)
- table({"A","B"}, {{1,2}})
- table({"A","B"},{{0,1},{2,1}})
- table({"A","B"},{{1,2}})
- table({"B","A"},{{2,1}})
- table({"B","C"}, {{3,4}})
- table({"Column1", "Column2"}, {{"Betty", 90.3}, {"Carl", 89.5}})
- table({"Foo"}, {{"Bar"}})
- table({"Link"}, {{"/test.html"}})
- table({"Name", "Kind", "Data"}, ...)
- table({"Name", "Score"}, {{"Betty", 90.3}, {"Carl", 89.5}})
- table({"Name", "Title"}, {{"Jo", "Manager"}})
- table({"X","Y"},{{0,1},{1,0}})
- table({"X","Y"},{{1,2}})
- table({"a", "b", "c"}, {{1, 2, 3}, {4, 5, 6}})
- table({"a", "b", "c"}, {{7, 8, 9}})
- table({"x", "x^2"}, {{1,1}, {2,4}, {3,9}})
- table({}, {})
- target  (for example, a T-SQL statement)
- text (for example,
"en-US")
- text (for example, "en-US")
- textFormat(binaryData)
- the (first)
- time
("T")
- time
("t")
- time
(DST)
- time ("F")
- time ("G")
- time ("T")
- time ("f")
- time ("g")
- time ("t")
- time (no date portion)
- time(
    hour as number,
    minute as number,
    second as number
)
- time(01, 30, 25)
- time(01,30,00)
- time(06, 45, 12)
- time(08,00,00)
- time(09,15,00)
- time(09,17,00)
- time(10, 00, 00)
- time(10, 12, 00)
- time(10, 12, 31)
- time(11, 30, 30)
- time(11, 56, 2)
- time(12, 0, 0)
- time(12,23,0)
- time(12,25,0)
- time(13, 0, 0)
- time(14, 0, 0)
- time(15, 0, 0)
- time(18, 10, 48)
- time(8, 30, 0)
- time(8,0,0)
- time(hour, minute, second)
- timezone (assuming PST)
- to ( => )
- to (=>)
- to ({[saleID = 1, item = "Shirt"], [saleID = 2, item = "Hat"]})
- transform (optional)
- transformFormat(binaryData)
- transformOperations  (where the
format is { column name, transformation } or { column name, transformation, new column type
})
- transformation(s)
- tree (AST)
- trip
("O", "o")
- trip ("O", "o")
- true
    (x = y)
- true
(1 meta [ a = 1 ])
- true 
(1 meta [ a = 1 ])
- type  (or the same type, if it is already closed)
- type  (or the same type, if it is already opened)
- type ( Int64.Type , Double.Type , and so on)
- type (but all table values have a row type that is
compatible with type table 's row type)
- type (called the "item type")
- type (derived from the intrinsic
type function )
- type (derived from the intrinsic type
table )
- type (for example,
subtracting a date  value from a datetime  value)
- type (i.e.
a non-custom type)
- type (including fractional digits)
- type (or the same type, if it is already closed)
- types ( Byte.Type , Decimal.Type , Int8.Type ,
Int16.Type , Int64.Type , and Single.Type )
- types ( Double.Type  and Int32.Type )
- types ( function , table , any , anynonnull
and none )
- types (but none  itself)
- types (for example,
"en-US")
- types (for example, "en-
US")
- units (days, hours, minutes, seconds)
- units (in this case,
thousands)
- useHeaders  (and delayTypes  is null)
- used ({ {old1, new1}, {old2, new2} })
- using ((state, current)
- value
(BinaryFormat.Byte)
- value 
(x, y)
- value ( "" )
- value ( #nan )
- value ( 4600 )
- value ("")
- value (-1 if not found)
- value (0)
- value (4326)
- value (for example, "en-US")
- value (not to
evaluate the function-body)
- value (optional)
- value (the return value)
- value (true or false)
- value(s)
- values
(2)
- values ( binary , date , datetime ,
datetimezone , duration , list , logical , null , number , record , text , time , type )
- values ( true  and false )
- values (as
opposed to function expressions)
- values (default is false)
- values (default is true)
- values (including record fields)
- values (length 0)
- values (length >
0)
- values (records,
lists, tables, and so on)
- values (refer to RoundingMode.Type for possible values)
- values (such as (type text)
- values (the argument
values)
- values (the body of the function)
- values (the parameters to
the function)
- variants (such as
DateTimeZone.FixedUtcNow )
- view (via
Table.View)
- view (via Binary.View)
- view (via Table.View)
- volatility (whether the value changes when called multiple times in the
same query)
- week (for example, Day.Sunday )
- written (for
example, UTF-8 BOM: 0xEF 0xBB 0xBF )
- x (inner)
- x (outer)
- x(...)
- y
 (x, y)
- y 
(x, y)
- zero (for example, 2008)
- zone (seven hours behind UTC)
- μμ (el-GR)
- Пн (ru-RU)
- понедельник (ru-
RU)
- م (ar-EG)
- 午 (ja-JP)
- 午後 (ja-JP)

***

# END OF THE CHEATSHEET
***
***
Made with ❤️ [Naveen Jujaray](https://www.linkedin.com/in/naveenjujaray/)
***
***