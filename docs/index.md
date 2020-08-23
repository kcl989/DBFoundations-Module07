<p style="text-align: right;"> Krystina Letendre </p> 
<p style="text-align: right;"> August 23, 2020 </p>
<p style="text-align: right;"> IT FDN 130 A </p>

# Assignment 7
Link to GitHub: https://github.com/kcl989/DBFoundations-Module07

## Introduction
Module 7 - Functions continued to build on the previous module and delved deeper in the subject of Functions.  For the assignment, we started by incorporating built-in functions into SELECT statements, then moved to creating VIEWS with functions, finally culminating in writing a user-defined function.  The user-defined function is a very powerful tool, allowing parameters to be passed to the function, which are then used to return a scalar value or an entire table.

## Short Answer
1. Explain when you would use a SQL UDF.
SQL UDF, or SQL user-defined functions, are custom functions the user can create.  They can be used as an alternative to VIEW, by passing in a parameter.  A main benefit of creating UDF’s is you can call the function instead of retyping the logic every time you want to use it.  Some of the examples used in the assignment this week include creating a KPI from inventory data (see code below).  The query itself was fairly complex, but by defining it as a function, the query is simplified to the users by just passing in a parameter without needing to recreate the logic of the query.  The function just needs to be defined once.  Further, if the KPI definition changes, the function can be altered in one location, rather than fixing code in every location it is used. 
```
-- How can you CREATE one more VIEW 
-- called vProductInventoriesWithPreviousMonthCountsWithKPIs
-- to show a list of Product names, Inventory Dates, Inventory Count, the Previous Month 
-- Count and a KPI that displays an increased count as 1, 
-- the same count as 0, and a decreased count as -1? Order the results by the Product, Date, and Count!

-- <Put Your Code Here> --
GO 
CREATE VIEW vProductInventoriesWithPreviousMonthCountsWithKPIs
AS
	SELECT TOP 100000 ProductName
		,([FormattedDate])
		,[InventoryCount]
		,[PreviousMonthCount]
		,[QtyChangeKPI] = CASE 
		   WHEN [InventoryCount] > [PreviousMonthCount] THEN 1
		   WHEN [InventoryCount] = [PreviousMonthCount] THEN 0
		   WHEN [InventoryCount] < [PreviousMonthCount] THEN -1
		   END 
	FROM vProductInventoriesWithPreviousMonthCounts
	ORDER BY ProductName, Month([FormattedDate]), [InventoryCount];
GO
```

2. Explain the differences between Scalar, Inline, and Multi-Statement Functions.
Scalar functions return a single value as an expression.  For example, you could make a scalar function that adds two parameters it received -- the result is a single summation value.  In contrast, both inline and multi-statement functions are table-valued functions, meaning they both return a table.  An inline function is the result of a single SELECT statement.  A multi-statement function is the result of multiple SELECT statements or queries (columns need to be defined, etc.).  

## Summary
This module helped provide practical examples for functions, along with demos and assignment questions to apply this newly introduced topic.  In some cases, Views and Functions can accomplish the same task, in which case Views are oftentimes preferred due to their simplicity and ease-of-understanding.  In this module, we created a UDF to return a table of values that meet the criteria of a specific KPI value.  This is a good example of how functions can be a useful tool in industry.
