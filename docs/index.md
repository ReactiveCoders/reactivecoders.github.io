---
layout: doc
title: Documentation
permalink: /docs/
---
* Will be replace by toc
{:toc}

#Who
Main target = enterprise
Process owner = finance department

#Logical implementation path

- standard reports
- ad hoc query
- multi-dimensional data
- planning/what if scenario

#Problem definition
- lots of small applications or large Excel file with valuable company specific details
- difficult to distribute/collect information/have latest document version
- Excel limit have been reach. When your spreadsheet is more than 100MB you have a problem.
There are a lot of valuable application with unreliable/wrong implementation.

I guess this is also due to IT specialization. No sysadmin, DB developer, Object oriented/functional language developer looks like a solution.
Like all complex problems is somewhere between domain.

#Solution

- try to harden existing implementation by adopting some existing IT experience/tools

Of interest for us:

- data warehouse/star schema. I see this two being the same : this is a set of practice, not a technology !!
- in-memory storage : Redis, Spark, VoltDB
- specialize store: multi-dimensional store, column store DB : Druid
- document management systems : Alfresco
- ETL : Pentaho Datastage, Storm
    Here I need to mention some input source a queue like : Kafka
- Large data storage : Hadoop HDFS
