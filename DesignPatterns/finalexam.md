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

- Record Set - 

## Domain Layer
