## table model

a new class for each table in the database 

## domain model

```
class Accounts{

void withdraw(accountNum, amt){
...
}

}
```



## transaction script

```
class stategy{
...
}

class withdraw : public Straegy{

}

```

> # Layers

## Service Layer


## Presentation Layer


## Data Source Layer

- Row Data Gateway - Each row of the table is an object. There can be many objects for many rows.
  
- Table Data Gateway - One object is the gateway or access to the whole table in the database.
Eg: In mongodb, Object students = db.collection("students")

Students object points to the student db

- Record Set - The dsata structure which represents the result of the query.

-  Active Record SEt

  The data source and domain layer merged Eachinstamce of th3e class is the row in the table.

  ```
class students{

getName();
getId();
getMarks();nt

```

- Data Mapper Pattern

```
  Class User{
  string naem;
  string id;
   



  }
 ```


# Behavioral Patterns

- Unit of work - When u want to do only one database call thus u bundle a number of api calls in one call. Thus latency is low.

- identity mapper - 

- Lazy Loading


# Structural Patterns

- Identity field
- Single Table inheritance -
- Concrete Table inheritance
- Class table inheritance
