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


#### Chapter 8 in SQFMM: Inner Joins

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

The most common use for an INNER JOIN is to link tables so that you can fetch columns from different tables that are related.

##### Embedding Joins withins Joins

Although you can solve many problems by linking only two tables, you often to link more than two tables.  The best way to do this is to 
check the relationships.  You many nteed to follow a path through several relationships. From SQFMM: " If you find your query using 
many JOINS is taking a long time to execute on a large db, you might get it to run faster by changing the sequence of the joins in your 
sql statement."

Here's a request: Show me the names of all my recipes and the names of all the ingredients for each of those recipes.

```
SELECT R.RecipeTitle AS 'Recipe Name', I.IngredientName AS 'Ingredient Name'
FROM (Recipes R 
INNER JOIN Recipe_Ingredients RI
ON R.RecipeID = RI.RecipeID ) 
INNER JOIN Ingredients I
ON RI.IngredientID = I.IngredientID
```

So in this case, even though we don't need any columns from Recipe_Ingredients table we need it in the query because 
Recipes and Ingredients are related through the Recipe_Ingredients table.  

##### SQFMM Inner Join Problems to Solve

SQFMM includes problems to solve--work through these!!

