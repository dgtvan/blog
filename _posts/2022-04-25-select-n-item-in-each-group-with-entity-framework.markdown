---
layout:	post
title:	"Select N Item In Each Group With Entity Framework"
date:	2022-04-25
---

  I was working on a project using EF 3.1. It was a day that I was given a dataset and asked to select only a few rows in each grouped subset.

There was nothing to clarify, I went straight forward to write LINQ, it should be something below

DatabaseContext.Objects.Where(w => ...)  
 .GroupBy(object => object.Key)  
 .Select(group => new {  
 Something = group.OrderBy(orderby => ...)  
 }  
 ...and what I got was an exception saying “…[something] can not be translated…”.

It turned out that LINQ obviously is an immediate language and gradually, it will be translated into a SQL query language. That is why there are cases LINQ still does not work, it is understandable.

Back to my problem, I had never dealt with this problem before so I had to search a lot to find a solution and to expand my knowledge surrounding it.

Here is the table showing ways to solve the problem.

![]({{ site.baseurl }}/images/1C0R8lW1usDxfmaYv9-RgBQ_2.png)(*) [FromSqlRaw](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.relationalqueryableextensions.fromsqlraw?view=efcore-6.0) is away we use EF to execute raw SQL queries.

Here is a repository containing examples for each approach on each EF version.

<https://github.com/VanDng/SelectFirstInGroupWithEF>

Enjoy ~

  