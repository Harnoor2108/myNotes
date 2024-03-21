## Data Source Patterns

> ## Architectural Patterns

1. Rowdata gateway - When each row is returned as an object. Organised but a lot of objects floating around.
2. table data gateway - All the rows are merged into a single object
3. Record set - a bunch of parallel arrays, data pulled out of database
4. Active Record - Combine data source and domain logic into one object. Used effeciently with data model and transaction scripts nu tnot with complex data models.
5. Data mapper - separated data access from domain logic. Complex pattern. Completely independent from each other. Useful in providing losose coupling.


> ## Behavioural Patterns

Controls when to read and write to the database
Slowest transaction - Reading and writing to the dtabase
  
  1.  Unit of Work - Lists changes to objects before forwarding to database and allows commits.
  2.  Identity map - Ensures each objct is loaded from the databse only once. Checks if the object is already loaded then get the same object else go to the database and find the object. The object is not persistant.
  3.  Lazy Loading - Does not get the data till it is mandatory
   
