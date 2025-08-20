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

### **Section.Section**

**Syntax**

```m
Section.Section(name as text) as section
```

**Example**

```m
Section.Section("MySection")
// Creates a new section
```


***

### **Section.Members**

**Syntax**

```m
Section.Members(section as section) as record
```

**Example**

```m
Section.Members(#sections[MySection])
```


***

### \#sections

**Syntax + Example**

```m
#sections
// Returns all sections in environment
```


***

### \#shared

**Syntax + Example**

```m
#shared
// Returns all shared functions in environment
```


***

### **Value.Metadata**

**Syntax**

```m
Value.Metadata(value as any) as record
```

**Example**

```m
Value.Metadata(123)
// Output: metadata record if exists
```


***

### **Value.AddMetadata**

**Syntax**

```m
Value.AddMetadata(value as any, metadata as record) as any
```

**Example**

```m
Value.AddMetadata(100, [Source="User"])
// Output: 100 with metadata
```


***

### **Table.View**

**Syntax**

```m
Table.View(name as text, handlers as record) as table
```

**Example**

```m
Table.View("MyView", [GetType = ()=> type table [A=number], GetRows=()=> {{1},{2}}])
```


***

### **Binary.Compress**

**Syntax**

```m
Binary.Compress(binary as binary, compressionType as number) as binary
```

**Example**

```m
Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate)
```


***

### **Binary.Decompress**

**Syntax**

```m
Binary.Decompress(binary as binary, compressionType as number) as binary
```

**Example**

```m
Binary.Decompress(Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate), Compression.Deflate)
```


***

### **Diagnostics.Trace**

**Syntax**

```m
Diagnostics.Trace(level as number, message as text, details as any) as any
```

**Example**

```m
Diagnostics.Trace(1, "Step running", [Detail="Log Info"])
```


***

### **Diagnostics.ActivityId**

**Syntax**

```m
Diagnostics.ActivityId() as text
```

**Example**

```m
Diagnostics.ActivityId()
// Returns a unique trace id
```


***
<section id="-accessing-data-functions"><h2>📂 Accessing Data Functions</h2></section>


***

### **Excel.Workbook**

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
// Returns a table of sheets and tables inside workbook
```


***

### **Excel.CurrentWorkbook**

**Syntax**

```m
Excel.CurrentWorkbook() as table
```

**Example**

```m
Excel.CurrentWorkbook(){[Name="Sales"]}[Content]
```


***

### **Excel.TableDefinedNames**

**Syntax**

```m
Excel.TableDefinedNames(workbook as any) as table
```

**Example**

```m
Excel.TableDefinedNames(File.Contents("C:\Data\Report.xlsx"))
```


***

### **Excel.SheetNames**

**Syntax**

```m
Excel.SheetNames(workbook as any) as list
```

**Example**

```m
Excel.SheetNames(File.Contents("C:\Data\Test.xlsx"))
```


***

### **Excel.CurrentWorkbook.Contents()**

**Syntax**

```m
Excel.CurrentWorkbook.Contents()
```

**Example**

```m
Excel.CurrentWorkbook.Contents()
```


***

### **Csv.Document**

**Syntax**

```m
Csv.Document(binary as binary, optional options as record) as table
```

**Example**

```m
Csv.Document(File.Contents("C:\Data\sales.csv"), [Delimiter=",", Columns=5, Encoding=1252])
```


***

### **Csv.PromoteHeaders**

**Syntax**

```m
Csv.PromoteHeaders(table as table, optional options as record) as table
```

**Example**

```m
Csv.PromoteHeaders(Table.FromRecords({[Col1="A", Col2="B"]}))
```


***

### **Csv.FromRows**

**Syntax**

```m
Csv.FromRows(rows as list, optional options as record) as text
```

**Example**

```m
Csv.FromRows({{"A","B"},{"C","D"}}, [Delimiter=","])
// Output text: "A,B↵C,D"
```


***

### **Json.Document**

**Syntax**

```m
Json.Document(source as any, optional encoding as any) as any
```

**Example**

```m
Json.Document(File.Contents("C:\Data\data.json"))
```


***

### **Json.FromValue**

**Syntax**

```m
Json.FromValue(value as any) as binary
```

**Example**

```m
Json.FromValue([Name="John", Age=30])
```


***

### **Xml.Document**

**Syntax**

```m
Xml.Document(source as any) as table
```

**Example**

```m
Xml.Document(File.Contents("C:\Data\data.xml"))
```


***

### **Xml.Tables**

**Syntax**

```m
Xml.Tables(source as any) as table
```

**Example**

```m
Xml.Tables(File.Contents("C:\Data\data.xml"))
```


***

### **Xml.Table**

**Syntax**

```m
Xml.Table(source as any, optional options as record) as table
```

**Example**

```m
Xml.Table("<root><x>1</x><x>2</x></root>")
```


***

### **Web.Contents**

**Syntax**

```m
Web.Contents(url as text, optional options as record) as binary
```

**Example**

```m
Web.Contents("https://api.example.com/data")
```


***

### **Web.Page**

**Syntax**

```m
Web.Page(html as any) as table
```

**Example**

```m
Web.Page(Web.Contents("https://example.com"))
```


***

### **Web.BrowserContents**

**Syntax**

```m
Web.BrowserContents(url as text) as binary
```

**Example**

```m
Web.BrowserContents("https://example.com")
```


***

### **OData.Feed**

**Syntax**

```m
OData.Feed(url as any, optional options as record) as table
```

**Example**

```m
OData.Feed("https://services.odata.org/V4/Northwind/Northwind.svc")
```


***

### **ODataV2.Feed / ODataV3.Feed / ODataV4.Feed**

Same as `OData.Feed`, but version-specific.

***

### **Odbc.DataSource**

**Syntax**

```m
Odbc.DataSource(connection as any, optional options as record) as table
```

**Example**

```m
Odbc.DataSource("dsn=mydb")
```


***

### **Odbc.Query**

**Syntax**

```m
Odbc.Query(connection as any, query as text, optional options as record) as table
```

**Example**

```m
Odbc.Query("dsn=mydb", "SELECT * FROM Sales")
```


***

### **Odbc.InferOptions**

**Syntax**

```m
Odbc.InferOptions(connection as any) as record
```


***

### **OleDb.DataSource**

**Syntax**

```m
OleDb.DataSource(provider as text, optional options as record) as table
```


***

### **OleDb.Query**

**Syntax**

```m
OleDb.Query(provider as text, query as text) as table
```


***

### **Sql.Database**

**Syntax**

```m
Sql.Database(server as text, database as text, optional options as record) as table
```

**Example**

```m
Sql.Database("serverName", "SalesDB")
```


***

### **Sql.Databases**

**Syntax**

```m
Sql.Databases(server as text, optional options as record) as table
```


***

### **Sql.Execute**

**Syntax**

```m
Sql.Execute(server as text, database as text, query as text) as table
```


***

### **Sql.Query**

**Syntax**

```m
Sql.Query(server as text, query as text, optional options as record) as table
```
***

### **AnalysisServices.Database**

**Syntax**

```m
AnalysisServices.Database(server as text, database as text, optional options as record) as table
```

**Placeholder**

```m
AnalysisServices.Database("MyServer", "ModelDB")
```

**Example**

```m
AnalysisServices.Database("asazure://region.asazure.windows.net/Server1", "SalesModel")
```


***

### **AnalysisServices.Databases**

**Syntax**

```m
AnalysisServices.Databases(server as text, optional options as record) as table
```

**Example**

```m
AnalysisServices.Databases("Server1")
```


***

### **ActiveDirectory.Domains**

**Syntax**

```m
ActiveDirectory.Domains(optional options as record) as table
```

**Example**

```m
ActiveDirectory.Domains()
```


***

### **ActiveDirectory.Domain**

**Syntax**

```m
ActiveDirectory.Domain(domain as text, optional options as record) as table
```

**Example**

```m
ActiveDirectory.Domain("contoso.com")
```


***

### **Exchange.Contents**

**Syntax**

```m
Exchange.Contents(url as text, optional options as record) as table
```

**Example**

```m
Exchange.Contents("https://outlook.office365.com/EWS/Exchange.asmx")
```


***

### **Exchange.Contacts**

**Syntax**

```m
Exchange.Contacts(url as text, optional options as record) as table
```

**Example**

```m
Exchange.Contacts("https://outlook.office365.com/EWS/Exchange.asmx")
```


***

### **SharePoint.Contents**

**Syntax**

```m
SharePoint.Contents(siteUrl as text, optional options as record) as table
```

**Example**

```m
SharePoint.Contents("https://contoso.sharepoint.com/sites/Finance")
```


***

### **SharePoint.Files**

**Syntax**

```m
SharePoint.Files(siteUrl as text, optional options as record) as table
```

**Example**

```m
SharePoint.Files("https://contoso.sharepoint.com/sites/Finance")
```


***

### **SharePoint.Tables**

**Syntax**

```m
SharePoint.Tables(siteUrl as text, optional options as record) as table
```


***

### **SharePoint.Lists**

**Syntax**

```m
SharePoint.Lists(siteUrl as text, optional options as record) as table
```


***

### **SharePoint.ContentsWithPath**

**Syntax**

```m
SharePoint.ContentsWithPath(siteUrl as text, path as text) as table
```


***

### **Folder.Files**

**Syntax**

```m
Folder.Files(path as text) as table
```

**Example**

```m
Folder.Files("C:\Data")
```


***

### **Folder.Contents**

**Syntax**

```m
Folder.Contents(path as text) as table
```

**Example**

```m
Folder.Contents("C:\Data")
```


***

### **File.Contents**

**Syntax**

```m
File.Contents(path as text) as binary
```

**Example**

```m
File.Contents("C:\Data\sales.csv")
```


***

### **Hdfs.Contents**

**Syntax**

```m
Hdfs.Contents(path as text) as table
```

**Example**

```m
Hdfs.Contents("/user/data")
```


***

### **Hadoop.FileSystem**

**Syntax**

```m
Hadoop.FileSystem(contents as any) as table
```


***

### **Python.Execute**

**Syntax**

```m
Python.Execute(script as text, optional inputs as record) as table
```

**Example**

```m
Python.Execute("import pandas as pd; df = pd.DataFrame({'A':[1,2]})")
```


***

### **RScript.Evaluate**

**Syntax**

```m
RScript.Evaluate(script as text, optional inputs as record) as table
```

**Example**

```m
RScript.Evaluate("data.frame(A=c(1,2), B=c(3,4))")
```


***
### **AzureStorage.BlobContents**

**Syntax**

```m
AzureStorage.BlobContents(url as text) as binary
```


***

### **AzureStorage.Contents**

**Syntax**

```m
AzureStorage.Contents(account as text) as table
```


***

### **AzureTables.Contents**

**Syntax**

```m
AzureTables.Contents(account as text) as table
```


***

### **AzureTable.Storage**

**Syntax**

```m
AzureTable.Storage(account as text, table as text) as table
```


***

### **AzureSQL.Database**

**Syntax**

```m
AzureSQL.Database(server as text, database as text, optional options as record) as table
```


***

### **AzureDataLake.Contents**

**Syntax**

```m
AzureDataLake.Contents(account as text, optional options as record) as table
```


***

### **AzureDataLake.Files**

**Syntax**

```m
AzureDataLake.Files(account as text, optional options as record) as table
```


***

### **AzureDataExplorer.Contents**

**Syntax**

```m
AzureDataExplorer.Contents(cluster as text, optional options as record) as table
```


***

### **AzureCostManagement.Tables**

**Syntax**

```m
AzureCostManagement.Tables(scope as text, optional options as record) as table
```


***

### **AzureDevOps.AccountContents**

**Syntax**

```m
AzureDevOps.AccountContents(organization as text, optional options as record) as table
```


***

### **AzureDevOps.Contents**

**Syntax**

```m
AzureDevOps.Contents(organization as text, optional options as record) as table
```


***

### **MySql.Database**

**Syntax**

```m
MySql.Database(server as text, database as text, optional options as record) as table
```


***

### **PostgreSQL.Database**

**Syntax**

```m
PostgreSQL.Database(server as text, database as text, optional options as record) as table
```


***

### **Teradata.Database**

**Syntax**

```m
Teradata.Database(server as text, optional options as record) as table
```


***

### **Snowflake.Databases**

**Syntax**

```m
Snowflake.Databases(account as text, optional options as record) as table
```


***

### **Snowflake.Database**

**Syntax**

```m
Snowflake.Database(account as text, database as text, optional options as record) as table
```


***

### **GoogleBigQuery.Database**

**Syntax**

```m
GoogleBigQuery.Database(optional options as record) as table
```


***

### **GoogleSheets.Contents**

**Syntax**

```m
GoogleSheets.Contents(url as text, optional options as record) as table
```


***

### **PowerBI.Dataflows**

**Syntax**

```m
PowerBI.Dataflows(optional options as record) as table
```


***

### **PowerPlatform.Dataflows**

**Syntax**

```m
PowerPlatform.Dataflows(optional options as record) as table
```


***

### **PowerBI.Datamarts**

**Syntax**

```m
PowerBI.Datamarts(optional options as record) as table
```


***

### **Salesforce.Data / Salesforce.Objects / Salesforce.Reports / Salesforce.Query**

- `Salesforce.Data()` – returns Salesforce data
- `Salesforce.Objects()` – returns list of objects
- `Salesforce.Reports()` – returns list of reports
- `Salesforce.Query(soql as text)` – runs a SOQL query

***

### **Dynamics365BusinessCentral.Contents**

**Syntax**

```m
Dynamics365BusinessCentral.Contents(url as text, optional options as record) as table
```


***

### **Dynamics365.Contents**

**Syntax**

```m
Dynamics365.Contents(url as text, optional options as record) as table
```


***

### **CommonDataService.Database**

**Syntax**

```m
CommonDataService.Database(url as text, optional options as record) as table
```


***

### **Dataverse.Contents**

**Syntax**

```m
Dataverse.Contents(url as text, optional options as record) as table
```


***
<section id="-binary-functions"><h2>📂 Binary Functions</h2></section>


***

### **Binary.Buffer**

**Syntax**

```m
Binary.Buffer(binary as binary) as binary
```

**Placeholder**

```m
Binary.Buffer(File.Contents("C:\img.png"))
```

**Example**

```m
Binary.Buffer(File.Contents("C:\Data\image.png"))
// Forces full file into memory
```


***

### **Binary.Combine**

**Syntax**

```m
Binary.Combine(binaries as list) as binary
```

**Example**

```m
Binary.Combine({Text.ToBinary("Hello"), Text.ToBinary("World")})
// Output binary representing "HelloWorld"
```


***

### **Binary.From**

**Syntax**

```m
Binary.From(value as any, optional options as record) as binary
```

**Example**

```m
Binary.From(123)
// Returns binary representation of number
```


***

### **Binary.FromText**

**Syntax**

```m
Binary.FromText(text as text, optional encoding as number) as binary
```

**Example**

```m
Binary.FromText("SGVsbG8=", BinaryEncoding.Base64)
// Decodes base64 string to binary
```


***

### **Binary.ToText**

**Syntax**

```m
Binary.ToText(binary as binary, optional encoding as number) as text
```

**Example**

```m
Binary.ToText(Text.ToBinary("Power"), BinaryEncoding.Base64)
// "UG93ZXI="
```


***

### **Binary.Length**

**Syntax**

```m
Binary.Length(binary as binary) as number
```

**Example**

```m
Binary.Length(Text.ToBinary("Test"))
// Output: 4
```


***

### **Binary.Range**

**Syntax**

```m
Binary.Range(binary as binary, offset as number, count as number) as binary
```

**Example**

```m
Binary.Range(Text.ToBinary("abcdef"), 2, 3)
// "cde"
```


***

### **Binary.Split**

**Syntax**

```m
Binary.Split(binary as binary, size as number) as list
```

**Example**

```m
Binary.Split(Text.ToBinary("abcdef"), 2)
// Output: { "ab","cd","ef" }
```


***

### **Binary.ToList**

**Syntax**

```m
Binary.ToList(binary as binary) as list
```

**Example**

```m
Binary.ToList(Text.ToBinary("AB"))
// {65,66}
```


***

### **Binary.Compress**

**Syntax**

```m
Binary.Compress(binary as binary, compressionType as number) as binary
```

**Example**

```m
Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate)
```


***

### **Binary.Decompress**

**Syntax**

```m
Binary.Decompress(binary as binary, compressionType as number) as binary
```

**Example**

```m
Binary.Decompress(Binary.Compress(Text.ToBinary("Hello"), Compression.Deflate), Compression.Deflate)
```


***
<section id="-binaryformat-functions"><h2>📂 BinaryFormat Functions</h2></section>

These describe **how to read/write binary streams**.

***

### **BinaryFormat.Binary**

```m
BinaryFormat.Binary(length as number)
```

**Example**

```m
BinaryFormat.Binary(5)
// Reads 5 bytes
```


***

### **BinaryFormat.Byte**

```m
BinaryFormat.Byte
```

**Example**

```m
BinaryFormat.Byte
// Reads 1 unsigned byte
```


***

### **BinaryFormat.SignedInteger8**

```m
BinaryFormat.SignedInteger8
```


### **BinaryFormat.UnsignedInteger8**

```m
BinaryFormat.UnsignedInteger8
```


***

### **BinaryFormat.SignedInteger16**

```m
BinaryFormat.SignedInteger16
```


### **BinaryFormat.UnsignedInteger16**

```m
BinaryFormat.UnsignedInteger16
```


***

### **BinaryFormat.SignedInteger32 / 64, UnsignedInteger32 / 64**

**Example**

```m
BinaryFormat.SignedInteger32
```


***

### **BinaryFormat.Single / Double**

```m
BinaryFormat.Single
BinaryFormat.Double
```


***

### **BinaryFormat.Text**

```m
BinaryFormat.Text(encoding as number)
```

**Example**

```m
BinaryFormat.Text(BinaryEncoding.Utf8)
```


***

### **BinaryFormat.Null**

```m
BinaryFormat.Null
```


***

### **BinaryFormat.Choice**

```m
BinaryFormat.Choice(selector as function, choices as list)
```


***

### **BinaryFormat.ChoiceRestart**

```m
BinaryFormat.ChoiceRestart(selector as function, choices as list)
```


***

### **BinaryFormat.List**

```m
BinaryFormat.List(elementFormat as function, count as any)
```


***

### **BinaryFormat.Record**

```m
BinaryFormat.Record(fields as record)
```


***

### **BinaryFormat.Length**

```m
BinaryFormat.Length(format as function, length as number)
```


***

### **BinaryFormat.ByteOrder**

```m
BinaryFormat.ByteOrder(format as function, byteOrder as number)
```


***

### **BinaryFormat.Group**

```m
BinaryFormat.Group(format as function)
```


***

### **BinaryFormat.Repeat**

```m
BinaryFormat.Repeat(format as function, count as number)
```


***
<section id="-combiner-functions"><h2>📂 Combiner Functions</h2></section>


***

### **Combiner.CombineTextByDelimiter**

```m
Combiner.CombineTextByDelimiter(delimiter as text, optional quoteStyle as any)
```

**Example**

```m
Combiner.CombineTextByDelimiter(",")({"A","B","C"})
// "A,B,C"
```


***

### **Combiner.CombineTextByEachDelimiter**

```m
Combiner.CombineTextByEachDelimiter(delimiters as list, quoteStyle as any, escape as any)
```


***

### **Combiner.CombineTextByLengths**

```m
Combiner.CombineTextByLengths(lengths as list)
```


***
<section id="-comparer-functions"><h2>📂 Comparer Functions</h2></section>


***

### **Comparer.Equals**

```m
Comparer.Equals(a as any, b as any) as logical
```

**Example**

```m
Comparer.Equals("A","a")
// false (case sensitive)
```


***

### **Comparer.FromCulture**

```m
Comparer.FromCulture(culture as text, ignoreCase as logical)
```

**Example**

```m
Comparer.FromCulture("en-US", true)
```


***

### **Comparer.Ordinal**

```m
Comparer.Ordinal
```


### **Comparer.OrdinalIgnoreCase**

```m
Comparer.OrdinalIgnoreCase
```


***
<section id="-lines-functions"><h2>📂 Lines Functions</h2></section>


***

### **Lines.FromBinary**

```m
Lines.FromBinary(binary as binary, optional encoding as any) as list
```

**Example**

```m
Lines.FromBinary(File.Contents("C:\Data\data.txt"))
```


***

### **Lines.ToBinary**

```m
Lines.ToBinary(lines as list, optional encoding as any)
```

**Example**

```m
Lines.ToBinary({"Line1","Line2"})
```


***

### **Lines.FromText**

```m
Lines.FromText(text as text, optional lineSeparator as any)
```

**Example**

```m
Lines.FromText("A;B;C",";")
// {"A","B","C"}
```


***

### **Lines.ToText**

```m
Lines.ToText(lines as list, optional lineSeparator as any)
```

**Example**

```m
Lines.ToText({"A","B","C"}, "|")
// "A|B|C"
```


***
<section id="-replacer-functions"><h2>📂 Replacer Functions</h2></section>


***

### **Replacer.ReplaceText**

```m
Replacer.ReplaceText(old as text, new as text)
```


### **Replacer.ReplaceValue**

```m
Replacer.ReplaceValue(old as any, new as any)
```

**Example**

```m
Table.ReplaceValue(#table({"A"},{{"Hello"}}),
    "Hello","World", Replacer.ReplaceText, {"A"})
// Output: {{"World"}}
```


***
<section id="-splitter-functions"><h2>📂 Splitter Functions</h2></section>


***

### **Splitter.SplitTextByDelimiter**

```m
Splitter.SplitTextByDelimiter(delimiter as text, optional quoteStyle as any, optional startAt as any)
```

**Example**

```m
Splitter.SplitTextByDelimiter(",")("A,B,C")
// {"A","B","C"}
```


***

### **Splitter.SplitTextByEachDelimiter**

```m
Splitter.SplitTextByEachDelimiter(delimiters as list, optional quoteStyle as any, optional startAt as any, optional comparer as any)
```


***

### **Splitter.SplitTextByWhitespace**

```m
Splitter.SplitTextByWhitespace()
```


***

### **Splitter.SplitTextByCharacterTransition**

```m
Splitter.SplitTextByCharacterTransition(accept as function, reject as function)
```


***

### **Splitter.SplitTextByLengths**

```m
Splitter.SplitTextByLengths(lengths as list)
```

**Example**

```m
Splitter.SplitTextByLengths({2,3})("ABCDE")
// {"AB","CDE"}
```


***

### **Splitter.SplitTextByPositions**

```m
Splitter.SplitTextByPositions(positions as list)
```


***

### **Splitter.SplitTextByRanges**

```m
Splitter.SplitTextByRanges(ranges as list)
```


***
<section id="-uri-functions"><h2>📂 Uri Functions</h2></section>


***

### **Uri.Parts**

```m
Uri.Parts(uri as text) as record
```

**Example**

```m
Uri.Parts("https://example.com/page?x=1")
// [Scheme="https", Host="example.com", Path="/page", Query=[x="1"]]
```


***

### **Uri.BuildQueryString**

```m
Uri.BuildQueryString(record as record) as text
```

**Example**

```m
Uri.BuildQueryString([x=1, y=2])
// "x=1&y=2"
```


***

### **Uri.EscapeDataString**

```m
Uri.EscapeDataString(text as text) as text
```

**Example**

```m
Uri.EscapeDataString("a b")
// "a%20b"
```


***

### **Uri.UnescapeDataString**

```m
Uri.UnescapeDataString(text as text) as text
```

**Example**

```m
Uri.UnescapeDataString("a%20b")
// "a b"
```


***
<section id="-value-functions"><h2>📂 Value Functions</h2></section>


***

### **Value.Type**

```m
Value.Type(value as any) as type
```

**Example**

```m
Value.Type("Hello")
// type text
```


***

### **Value.ReplaceType**

```m
Value.ReplaceType(value as any, type as type) as any
```

**Example**

```m
Value.ReplaceType(123, type text)
// Treats 123 as type text
```


***

### **Value.Metadata**

```m
Value.Metadata(value as any) as record
```

**Example**

```m
Value.Metadata(123)
```


***

### **Value.AddMetadata**

```m
Value.AddMetadata(value as any, metadata as record) as any
```

**Example**

```m
Value.AddMetadata(42, [Source="User"])
// 42 (with metadata)
```


***

### **Value.Is**

```m
Value.Is(value as any, type as type) as logical
```

**Example**

```m
Value.Is(123, type number)
// true
```


***

### **Value.As**

```m
Value.As(value as any, type as type) as any
```

**Example**

```m
Value.As(123, type number)
// 123
```


***

### **Value.FromText**

```m
Value.FromText(text as text, optional culture as text) as any
```

**Example**

```m
Value.FromText("123")
// 123
```


***

### **Value.ToText**

```m
Value.ToText(value as any, optional format as any, optional culture as text) as text
```

**Example**

```m
Value.ToText(123, "D4")
// "0123"
```


***

### **Value.Compare**

```m
Value.Compare(a as any, b as any, optional comparer as any) as number
```

**Example**

```m
Value.Compare(1,2)
// -1
```


***

### **Value.Equals**

```m
Value.Equals(a as any, b as any, optional precision as any) as logical
```

**Example**

```m
Value.Equals(3.1415, 3.1415)
// true
```


***

### **Value.NullableEquals**

```m
Value.NullableEquals(a as any, b as any) as logical
```

**Example**

```m
Value.NullableEquals(null, null)
// true
```


***

### **Value.ExpandRecord**

```m
Value.ExpandRecord(record as record) as list
```

**Example**

```m
Value.ExpandRecord([a=1,b=2])
// {1,2}
```


***

### **Value.ReplaceError**

```m
Value.ReplaceError(value as any, replacement as any) as any
```

**Example**

```m
Value.ReplaceError(try 1/0 otherwise null, -1)
// -1
```


***

***
<section id="-expression--error--diagnostics"><h2>📂 Expression &amp; Error &amp; Diagnostics</h2></section>


***

### **Expression.Evaluate**

```m
Expression.Evaluate(text as text, optional environment as record)
```

**Example**

```m
Expression.Evaluate("2+3")
// 5
```


***

### **Expression.Identifier**

```m
Expression.Identifier(name as text)
```


***

### **Expression.Constant**

```m
Expression.Constant(value as any)
```


***

### **Error.Record**

```m
Error.Record(reason as text, message as text, detail as any) as record
```

**Example**

```m
Error.Record("Error", "Message", "Details")
```


***

### **Error.Raise**

```m
Error.Raise(reason as text, message as text, optional detail as any) as none
```


***

### **Diagnostics.Trace**

```m
Diagnostics.Trace(level as number, message as text, details as any) as any
```


***

### **Diagnostics.ActivityId**

```m
Diagnostics.ActivityId()
```


***

***
<section id="-table-helper-functions"><h2>📂 Table Helper Functions</h2></section>


***

### **Table.SelectColumns**

```m
Table.SelectColumns(table as table, columns as any, optional missingField as any)
```

**Example**

```m
Table.SelectColumns(#table({"A","B"}, {{1,2},{3,4}}), {"A"})
// Only A column
```


***

### **Table.RemoveColumns**

```m
Table.RemoveColumns(table as table, columns as list, optional missingField as any)
```


***

### **Table.RenameColumns**

```m
Table.RenameColumns(table as table, renames as list, optional missingField as any)
```


***

### **Table.ReorderColumns**

```m
Table.ReorderColumns(table as table, columns as list, optional missingField as any)
```


***

### **Table.TransformColumns**

```m
Table.TransformColumns(table as table, transformations as list, optional defaultTransformation as any, optional missingField as any)
```


***

### **Table.TransformColumnTypes**

```m
Table.TransformColumnTypes(table as table, typeTransformations as list, optional culture as text, optional missingField as any)
```


***

### **Table.SplitColumn**

```m
Table.SplitColumn(table as table, column as text, splitter as function, optional newColumnNames as list, optional default as any, optional extraValues as any)
```


***

### **Table.AddColumn**

```m
Table.AddColumn(table as table, newColumnName as text, columnGenerator as function, optional columnType as any)
```


***

### **Table.AddIndexColumn**

```m
Table.AddIndexColumn(table as table, newColumnName as text, optional initialValue as number, optional increment as number, optional columnType as any)
```


***

***
<section id="-text-helper-functions"><h2>📂 Text Helper Functions</h2></section>


***

### **Text.Contains**

```m
Text.Contains(text as text, substring as text, optional comparer as any) as logical
```


### **Text.StartsWith**

```m
Text.StartsWith(text as text, substring as text, optional comparer as any)
```


### **Text.EndsWith**

```m
Text.EndsWith(text as text, substring as text, optional comparer as any)
```


### **Text.Split**

```m
Text.Split(text as text, delimiter as text, optional quoteStyle as any)
```


### **Text.SplitAny**

```m
Text.SplitAny(text as text, separators as any)
```


### **Text.SplitByLengths**

```m
Text.SplitByLengths(text as text, lengths as list)
```


### **Text.SplitByPositions**

```m
Text.SplitByPositions(text as text, positions as list)
```


### **Text.ReplaceEach**

```m
Text.ReplaceEach(text as text, replacements as list)
```


***

***
<section id="-number-helper-functions"><h2>📂 Number Helper Functions</h2></section>


***

### **Number.Round**

```m
Number.Round(number as nullable number, optional digits as nullable number, optional roundingMode as any)
```


### **Number.Divide**

```m
Number.Divide(number as nullable number, divisor as nullable number, optional precision as any)
```


### **Number.ToText**

```m
Number.ToText(number as nullable number, optional format as any, optional culture as text)
```


### **Number.FromText**

```m
Number.FromText(text as text, optional culture as text)
```


***

***
<section id="-datetime-overloads"><h2>📂 Date/Time Overloads</h2></section>


***

### **Date.ToText**

```m
Date.ToText(date as date, optional format as any, optional culture as text)
```


### **Time.ToText**

```m
Time.ToText(time as time, optional format as any, optional culture as text)
```


### **DateTime.ToText**

```m
DateTime.ToText(datetime as datetime, optional format as any, optional culture as text)
```


### **DateTime.AddZone**

```m
DateTime.AddZone(datetime as datetime, offset as number) as datetimezone
```


### **DateTimeZone.SwitchZone**

```m
DateTimeZone.SwitchZone(datetimezone as datetimezone, offset as number) as datetimezone
```


### **DateTimeZone.ToLocal**

```m
DateTimeZone.ToLocal(datetimezone as datetimezone) as datetime
```


### **DateTimeZone.RemoveZone**

```m
DateTimeZone.RemoveZone(datetimezone as datetimezone) as datetime
```


***

# END OF THE CHEATSHEET
***
***
Made with ❤️ [Naveen Jujaray](https://www.linkedin.com/in/naveenjujaray/)
***
***