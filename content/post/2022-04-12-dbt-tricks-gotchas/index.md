---
title: dbt Tricks & Gotchas
author: Roel M. Hogervorst
date: '2022-04-12'
slug: dbt-tricks-gotchas
categories:
  - lessons-learned
tags:
  - dbt
  - sql
---

I've been working with dbt lately and I love that project and all it enables.
But there are some things  I figured out only after trying it out.

* if you build a custom test it needs to live in one of 2 places: `macros/` (Because it is a macro) or `tests/generic/` 

```
├── analyses/
├── dbt_packages/
├── logs/
├── macros/    <- put custom tests here or
├── models/
├── seeds/
├── snapshots/
├── target/
└── tests/      <- or put them in tests/generic/
├── GUIDE.md
├── README.md
├── dbt_project.yml
├── packages.yml
├── profiles.yml
```

* custom tests are quite easily build based on the basis of existing ones.
Here is one I wrote

```sql
-- make sure the column value is between two values inclusive.

{% test column_between_values_incl(model, column_name, low, high) %}

    select *
    from {{ model }}
    where {{ column_name }} > {{ high }}
    and {{ column_name }} > {{ low }}

{% endtest %}
```

And you can use this one in the schema.yml 

```yaml
version: 2

models:
  - name: stg_daily_values
    description: >
        Contains the values on a day that do not change
    columns:
      - name: wind_dir_degree
        description: Wind direction, degrees (meteorological) (0-260)(int)
        tests:
          - column_between_values_incl:
              low: 0
              high: 360
```

* You can annotate models, source tables and many things more with tags. But where do you do this?  

Sources can be tagged in the schema.yml (that live close to the files).
But you can also tag models, but that lives in config

a schema.yml
```yaml
sources:
    tables:
      - name: raw_current_weather
        tags:
            - raw
models:
  - name: stg_daily_values
    description: >
        Contains the values on a day that do not change
    config:
      tags: 'blob'
```

I think it is better to define all the tags in the dbt_project.yml,
but I'm not sure how to tag a source in dbt_project.yml. 

```yaml
models:
  work_dbt:
    openweathermap:
      +materialized: view
      +tags: weather
      +schema: openweathermap
      staging:
        stg_daily_values:
          +tags: "daily"

```
The model stg_daily_values in openweathermap has 2 tags: one from the upper definition openweathermap (weather) and one from the lower level

