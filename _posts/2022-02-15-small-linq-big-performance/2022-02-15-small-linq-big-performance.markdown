---
layout:	post
title:	"Small LINQ Big Performance"
date:	2022-02-15
---

Avoid writing LINQs that generate queries invoking the function **Convert()**, it might cause a performance issue.

In one of my web application projects, there was a performance issue on an endpoint making queries to a database. The queries were written by LINQ EF Core 6.

The LINQ statement was simply a query of a collection of records with a simple Where conditional statement.

Unfortunately, a small misthinking led to a big performance decrement.

Given a database with a simple table having a column named “guid” with data type GUID.

I have a string collection of GUID values, I want to find all records matching with my GUID collection.

Let’s begin to write a LINQ.

#### LINQ Bad Way

```
List<string> stringGUIDCollection = 
    DB.Context.Where(x => 
        stringGUIDCollection.Contains(x.guid.ToString())
    );
```
**guid** must be converted to string because the method **Contains() **requires an argument of a string type.

The given LINQ will be translated to a query below

```
SELECT *  
FROM <Table>  
WHERE Convert(nvarchar(max), guid) in ('xxx-yyy...','zzz-mmm...',...)
````
The function Convert() here slows down the query a lot. Hmm… Why?

I didn’t know exactly what MS SQL worked under the hood, my findings were based on my comparison with another query producing the exact same expected output.

**LINQ Better Way**

```
List<string> stringGUIDCollection = ...

List<guid> guidCollection = stringGUIDCollection.Select(s => Guid.Parse(s));
 
DB.Context.Where(x => guidCollection.Contains(x.guid));
 ```
Here I do the job of converting GUID strings to GUID objects and passing them to the LINQ.

The given LINQ will be translated to a query below

```
SELECT *  
FROM <Table>  
WHERE guid in ('xxx-yyy...','zzz-mmm...',...)
```
In terms of time-consuming, this query is much faster than the one invoking the function Convert() above.

No big discovery but I am aware of this sort of issue from now on, so you do!