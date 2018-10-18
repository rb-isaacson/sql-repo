# sql-repo

Notes from the book SQL Queries for Mere Mortals(SQFMM) and the [dofactory sql tutorial](https://www.dofactory.com/sql/tutorial)

## Joins

A join allows you to creat a logical table.  For example, you can use a join to link customers to their orders by matching 
the CustomerID in the Customers table to the CustomerID in the Orders table.

### Summary of different types of joins

* INNER JOIN: Select records that have matching values in both tables.
* LEFT OUTER JOIN: Select records from the left most table with matching right table records.
* RIGHT OUTER JOIN: Select records from the right most table with matching left table records.
* FULL OUTER JOIN: Select all records that match either left or right table records.


### Inner Joins

The inner join returns rows in a Students that have a matching value in a Courses table. It will not return Students who 
don't have any courses or any courses without students.  Another way to say this is:

An INNER JOIN returns only those rows where the linking values match in both of the tables or in result sets.

If you don't explicitly state the type of JOIN you want, then the default is INNER.  

The recommendation from SQFMM is to always explicitly state the type of JOIN so that the nature of your request is clear.

Here's an example request:  Show me the recipe title, preparation and recipe class description of all recipes.

```
SELECT       Recipes.RecipeTitle, Recipes.Preparation, Recipe_Classes.RecipeClassDescription
FROM         Recipes 
INNER JOIN   Recipe_Classes 
ON           Recipes.RecipeClassID = Recipe_Classes.RecipeClassID
```

You can also use alias names for the tables.  (SQFMM also refers to them as correlation names).  Here's what that would look like
using the above query when we use alias names for the tables.

```
SELECT       R.RecipeTitle, R.Preparation, RC.RecipeClassDescription
FROM         Recipes AS R
INNER JOIN   Recipe_Classes AS RC 
ON           R.RecipeClassID = RC.RecipeClassID
```
