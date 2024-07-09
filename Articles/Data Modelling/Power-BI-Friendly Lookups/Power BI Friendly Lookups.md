# Power BI Lookups Best Practices

When working with Power BI lookups, there are several best practices to ensure efficient, accurate, and maintainable data models. It is important to ensure that our data models is not only minimised (small in size), but is also able to read and load data fast.

It is no longer news that the Star Schema is the `Holy Grail` of data modelling in Power BI, and that LookUp (Dimension) Tables are the key components thereof. However, if used wrongly, these have the tendency to brutally ruin the balance of the grail.

Ten things I keep in mind when designing LookUp Tables are as follows:

01. Understand Your Data
02. Data Types and Consistency
03. Understand Your Data Model
04. Efficient Data Loading
05. Manage Relationships
06. Use DAX Functions Wisely
07. Optimize Performance
08. Documentation and Naming Conventions
09. Regular Maintenance
10. Testing and Validation

<br>
I'll give brief descriptions below

### 01. Understand Your Data

<strong>Data Story:</strong> Understand each dataset in tyour model and the part they play in putting your data story together.
<strong>Nomenclature:</strong> Understand the naming convention/pattern of the columns of your datasets, ensure they are consistent always. 

### 02. Data Types and Consistency

Consistent Data Types: Ensure that the data types of columns used in relationships are consistent. Mismatched data types can lead to relationship issues and errors in lookups.
Avoid Implicit Data Conversions: Implicit conversions can slow down your model. Define data types explicitly in Power Query or your data source.

### 03. Understand Your Data Model

<strong>Know the Relationships:</strong> Understand the relationships between your tables (one-to-many, many-to-many, etc.), the fields that form these relationships, and ensure they are correctly defined in the data model. It is also important to know where to define an active relationship and where to define an inactive one.
<strong>Normalize Data:</strong> Properly normalised data models make lookups simpler and more efficient.

### 04. Efficient Data Loading

<strong>Filter Data at Source:</strong> Apply filters and transformations at the source or in Power Query to limit the data loaded into Power BI. This improves performance and reduces clutter.
<strong>Remove Unnecessary Columns:</strong> Only load columns that are needed for your analysis to optimize performance.

### 05. Manage Relationships

<strong>Create Relationships in Power BI:</strong> Define relationships explicitly in Power BI using the relationship view. Ensure the correct cardinality (one-to-many, many-to-one, etc.) is set.
<strong>Bidirectional Filtering:</strong> Use bidirectional filtering judiciously as it can impact performance and lead to ambiguous relationships. Default to single-directional filtering unless a specific use case necessitates bidirectional filters.

### 06. Use DAX Functions Wisely

<strong>RELATED and RELATEDTABLE:</strong> Use the RELATED function to pull data from a related table in a one-to-one or many-to-one relationship. Use RELATEDTABLE to work with many-to-many relationships.
<strong>LOOKUPVALUE:</strong> This function is useful for finding a single value from another table. However, be cautious with performance, especially on large datasets.

### 07. Optimize Performance

<strong>Index Columns:</strong> Ensure lookup columns (keys) are indexed in the source database to improve query performance.
<strong>Minimize Cross-Joins:</strong> Avoid cross-joins as they can lead to significant performance issues. Ensure relationships are correctly defined to prevent accidental cross-joins.
<strong>Use Measures Instead of Calculated Columns:</strong> Where possible, use measures rather than calculated columns for performance efficiency.

### 08. Documentation and Naming Conventions

<strong>Clear Naming Conventions:</strong> Use clear, descriptive names for tables and columns to make your model easier to understand and maintain.
<strong>Document Relationships and Logic:</strong> Maintain documentation on the relationships, business logic, and calculations used in your Power BI model.

### 09. Regular Maintenance

<strong>Review and Clean Up:</strong> Regularly review your data model to remove any unused tables, columns, or relationships.
<strong>Update as Needed:</strong> As your data or business requirements change, ensure your data model and lookups are updated accordingly.

### 10. Testing and Validation

<strong>Validate Relationships and Data:</strong> Regularly test your relationships and lookups to ensure they return correct and expected results.
<strong>Performance Testing:</strong> Perform load testing to identify and address any performance bottlenecks in your lookups and data model.

<br>

Creating a Power BI-Friendly lookup table involves several key principles to ensure it integrates well with your data model and performs efficiently. Here are the characteristics and best practices for designing such lookup tables:

### 01. Unique Key Columns

<strong>Primary Key:</strong> Each lookup table should have a primary key column that contains unique values. This key is used to establish relationships with fact tables.
<strong>Consistent Data Types:</strong> Ensure the primary key column has a consistent data type across all tables it relates to.

### 02. Descriptive Columns

<strong>Meaningful Names:</strong> Use clear and descriptive column names that indicate the content of the column. Avoid abbreviations that might be unclear.
<strong>Additional Descriptions:</strong> Include columns that provide additional descriptive information relevant to the key, which can be used for reporting purposes.

### 03. Normalisation

<strong>Eliminate Redundancy:</strong> Structure the lookup table to avoid redundancy. Ensure each piece of information is stored only once.
<strong>Separate Concerns:</strong> Split complex or multi-faceted data into separate tables to maintain a clean and efficient structure.

### 04. Proper Formatting and Data Types

<strong>Consistent Formatting:</strong> Ensure that columns are consistently formatted, especially for dates, strings, and numerical values.
<strong>Appropriate Data Types:</strong> Assign the correct data type to each column to optimize performance and accuracy.

### 05. Minimize Data Volume

<strong>Essential Columns Only:</strong> Include only the columns necessary for your analysis and reporting. Avoid loading extraneous data.
<strong>Filter Unneeded Rows:</strong> Apply filters to exclude irrelevant rows from the lookup table, reducing the amount of data processed.

### 06. Indexing

<strong>Indexed Keys:</strong> Ensure that the key columns are indexed in the source database to improve join and lookup performance in Power BI.

### 07. Data Quality

<strong>No Duplicates:</strong> Ensure there are no duplicate entries in the key column.
<strong>Data Integrity:</strong> Validate the data to ensure there are no missing or corrupt entries in the lookup table.

### 08. Documentation

Clear Descriptions: Document the purpose and contents of each lookup table and its columns. This aids in understanding and maintaining the data model.
Example Structure of a Power BI-Friendly Lookup Table
Assuming you have a lookup table for "Products," here is an example structure:


ProductID   |	ProductName |	Category    |	SubCategory |	Manufacturer    |	LaunchDate
------------|---------------|---------------|---------------|-------------------|---------------
1001	    |   Widget A	|    Widgets	|   Type 1	    |   Company X	    |   2020-01-15
1002	    |   Widget B	|    Widgets	|   Type 2	    |   Company Y	    |   2020-03-10
1003	    |   Gadget C	|    Gadgets	|   Type 1	    |   Company X	    |   2021-07-23
1004	    |   Gizmo D	    |    Gizmos	    |   Type 1	    |   Company Z	    |   2022-11-05


Key Considerations for the Example Table
- ProductID: Unique identifier for each product (Primary Key).
- ProductName: Descriptive name of the product.
- Category: General classification of the product.
- SubCategory: More detailed classification within the category.
- Manufacturer: Name of the company that manufactures the product.
- LaunchDate: The date the product was launched (proper date formatting).


# How normalised should a Power BI-Friendly LookUp Table be when compared to the actual fact table?

In Power BI, lookup tables, often referred to as dimension tables, should generally be more normalised compared to fact tables to optimize performance and maintainability. Here’s a detailed explanation based on industry best practices:

## Normalisation of Lookup Tables

### Normalisation Levels:

<strong>Dimension Tables:</strong> These tables are usually normalised to at least the second normal form (2NF). This means they store descriptive attributes in separate, logically grouped tables to reduce redundancy and ensure data integrity. For example, a "Product" dimension table might be normalised into separate tables for "ProductCategory" and "ProductSubcategory"​ (MS Learn)​​ (Stack Overflow)​.

<strong>Fact Tables:</strong> In contrast, fact tables are typically denormalized. They consolidate multiple keys and measures into a single table to speed up data retrieval and simplify queries. Fact tables store transactional or event data and usually contain foreign keys that reference dimension tables​ (Zebra BI)​.

<strong>Star Schema Preference:</strong> The preferred schema in Power BI is the star schema, where a central fact table is surrounded by dimension tables. This design simplifies queries and improves performance because it minimises the number of joins needed to retrieve data​ (MS Learn)​​ (Zebra BI)​.

### Advantages of Normalised Dimension Tables:

<strong>Efficiency:</strong> Normalised dimension tables reduce data redundancy and improve storage efficiency. This makes updates more manageable, as changes to an attribute only need to be made in one place.
<strong>Clarity and Maintenance:</strong> Normalisation helps keep the data model clean and organized, making it easier to understand and maintain. This is particularly important in complex models where attributes might otherwise be duplicated across multiple tables.

### Balancing Normalisation and Usability:

While normalization is beneficial, it’s crucial not to over-normalize to the point where it complicates the data model unnecessarily. In Power BI, it can be advantageous to slightly denormalize dimension tables if it simplifies the model and makes it more intuitive for end-users. For example, combining related attributes into a single table can sometimes improve usability without significantly impacting performance​ (MS Learn)​​ (SQL Spreads)​.

### Practical Example

<strong>Consider a sales data model:<strong>

<strong>Fact Table (Sales):</strong> Contains keys to related dimensions (e.g., DateKey, ProductKey, CustomerKey) and measures like SalesAmount, Quantity, etc.

<strong>Dimension Tables:
    - <strong>Products:</strong> Contains ProductID (Primary Key), ProductName, CategoryID, SubcategoryID, etc.
    - <strong>Categories:</strong> Contains CategoryID (Primary Key), CategoryName.
    - <strong>Subcategories:</strong> Contains SubcategoryID (Primary Key), SubcategoryName, CategoryID (Foreign Key).

In this setup, the "Products" table is normalised into separate "Categories" and "Subcategories" tables to avoid redundancy and improve data integrity. The fact table (Sales) is denormalized and includes keys to these dimension tables, which helps in efficient querying and reporting.

In summary:

A Power BI-Friendly lookup table should be normalized to at least 2NF to ensure efficiency and maintainability, while fact tables should be denormalized to facilitate fast data retrieval and simplify the analytical process. Striking the right balance between normalization and usability is key to creating an optimal data model in Power BI​ (MS Learn)​​ (Zebra BI)​.


### Credits
[(MS Learn)​​](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
[(Stack Overflow)](https://stackoverflow.com/questions/22703985/is-a-fact-table-in-normalized-or-de-normalized-form)
[(Zebra BI)​](https://zebrabi.com/guide/how-to-create-fact-and-dimension-tables-in-power-bi/)
[(SQL Spreads)](https://sqlspreads.com/blog/power-bi-fact-and-dimension-tables/)