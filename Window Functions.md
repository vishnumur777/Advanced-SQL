
- Window functions are used to do certain operation on a specific set of rows based on column selection.

- Which means operations are performed after separation of subset of rows.



## For Example

Let us consider a table which contains employees data which named as 'emp'.

| id | name | salary | department |
| -- | ---  | ------- | --------- |
| 1 | John Doe | 10000 | Sales |
| 2 | Jane Doe | 15000 | IT |
| 3 | Mary Smith |  20000 | Sales |
| 4 | Peter Jones | 25000 | IT |
| 5 | Susan Williams | 30000 | Accounts |


## *Note : For applying window function in SQL, 'OVER' Keyword is applied.*

- Query looks like this

### SELECT 'A' OVER 'B' FROM TABLE_NAME;

where,
- A =  Aggregate Function
- B = PARTIION OVER 'column_name' (OR) ORDER BY 'column_name' (OR) ROW or RANGE clause.

#### From the above table,

we can write query as

### SELECT id,name,salary,department,SUM(salary) OVER (PARTITION BY department ORDER BY id DESC) AS running_total FROM emp;

which we get table as,

![[Pasted image 20230707225305.png]]

________________________________________________________________


# Analysing the query

when I run by removing some aggregate functions , I can able to understand something on this

- When I run,

#a1

### SELECT id,name,salary,department,SUM(salary) OVER (PARTITION BY department) AS running_total FROM emp;


we get table as,

![[Pasted image 20230707225909.png]]

From this I can understand that by looking on `running_total` column, it just forms a `subset` which is based on department (IT, sales and Accounts) and `summed up together` , and applied on all the columns which are applicable to it.

#### For example,

 -  If we consider id = 2 and 4 , they work from IT department , If I summed up the total of both salaries in the department we get 40,000 ( 15,000 + 25,000 ).
 
 -  same applied for sales department as well 30,000 (10,000+20,000).

------------------------------------------------------

From the #a1 query,

#a2

### SELECT id,name,salary,department,SUM(salary) OVER (PARTITION BY department ORDER BY id) AS running_total FROM emp;

we get table as,

![[Pasted image 20230707232907.png]]

- Now by looking at `running_total` column, at id = 2 , we can see no change happened by looking on salary,
-  But, by looking at next row, the 25,000 get summed up along with 15,000 to get 40,000.

---------------------------------------------

Now we add descending order and see the changes to it,

we get the entire query as output.

![[Pasted image 20230707225305.png]]



# Note: Window funtions works based on aggregate operations on group of rows but produce results on for each row.



______________________________________________________________________

# Aggregate Function used in Window functions

window functions can be used according to syntax are classified into 2 types based on syntax

#### SELECT A OVER (B) FROM TABLE_NAME;

WHERE 

- A => selection function
- b => define a window

## 1. selection function

- selection function are the aggregate functions used in SQL for window functions.

- these are classified into 3 types,

    - Aggregate functions
    - Ranking functions
    - Analytic functions


#### i) Aggregate functions

- Same functions that you can use with the group by statement.

- SUM
- AVG
- MIN
- MAX, etc.,

- used to compute statistics within group.

![[Pasted image 20230708220521.png]]


#### ii) Ranking Functions

- Calculate the rank of each row within each group
- commonly used ranking Functions

	- ROW NUMBER - number all row sequentially
	- RANK - provides same numberic value or row with its same value.
	- DENSE_RANK - provides rank with no gaps within its values
	- NTILE - provide percentile.

- Used for selection of N top row in the group.

![[Pasted image 20230708220932.png]]


#### iii) Analytical Functions

- Access values of multiple row in a window.
- compare multiple rows and calculate the differences between rows.

Example 

   - lead - K values present after the current row.
   - lag - K values present before the current row.

where K is offset

##### Rules

- need to specify the column name as well as offset
- Offset cannot be a negative value.
- can set the default value to be used if a previous/following row does not exist.

![[Pasted image 20230708221905.png]]


![[Pasted image 20230708221938.png]]


--------------------------------------------------------------------------

# Done!!!

-----------------------------

