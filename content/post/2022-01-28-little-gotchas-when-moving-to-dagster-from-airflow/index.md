---
title: Little Gotchas when Moving to Dagster from Airflow
author: Roel M. Hogervorst
date: '2022-01-28'
slug: little-gotchas-when-moving-to-dagster-from-airflow
categories:
  - other
tags:
  - airflow
  - dagster
  - schedulers
  - python
  - data-engineering
---

I've been experimenting with [dagster](https://dagster.io/), an open source scheduler for 
data workflows. The product looks really slick and I enjoy working with it.
Previously I've worked with Airflow but for this job I believe dagster is the
better choice.

I believe it is possible to more or less transform airflow DAGs (directed acyclic graphs, or compution actions in order) into Dagster Jobs. 

So what are the gotchas?

Airflow has a focus on executing the actions in order. The focus of dagster is 
a pipeline of data transformations. 
Dagster explicitly defines  the inputs and outputs of every operation, so you can
connect the data you yield from step 1 and use it in step 2. In Airflow you can provide
the location of your data in step 1, and retrieve that location in step 2, but it is not
so explicit. 
So if you want to execute a set of independent SQL queries, Airflow is the simpler choice. If you want to load data from a database, 
transform it with pandas and write it to S3 you might consider if dagster isn't better. 

For this $work assignment we have many data intensive flows of data from one system
to another and therefore dagster is a better choice. 
However we do have SQL scripts that need to be run in separate steps in order, 
but they are not idempotent and they don't move data. So what do you do then?

In dagster you can make explicit that your operation has no output but does
depend on other operations. In dagster we define in and outputs of operations (@ops) inside the decorator. 

```python
from dagster import In, Nothing, job, op
from repository.queries import query1, query2
@op
def create_table_1():
    query = read_query_file(query1)
    get_database_connection().execute(query)


@op(ins={"start": In(Nothing)})
def create_table_2():
    query = read_query_file(query2)
    get_database_connection().execute(query)

@job
def nothing_dependency():
    create_table_2(start=create_table_1())
```

So I think that this is an appropriate way to move from loose SQL scripts to 
running these scripts with a proper scheduler. 

However if you are actually filling tables or partitions you want to upgrade 
this by yielding Asset Materializations, that is; telling Dagster you've created
something in a remote location. That way you can even trigger other jobs that 
only need to run on a new partition, in Airflow you had to cobble them all
together inside one DAG. In dagster you can keep the downstream jobs seperate.

* [dagster, jobs, order-based-dependencies-nothing-dependencies](https://docs.dagster.io/concepts/ops-jobs-graphs/jobs-graphs#order-based-dependencies-nothing-dependencies)
