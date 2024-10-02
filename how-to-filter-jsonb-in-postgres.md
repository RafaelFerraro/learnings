### How to filter jsonb fields in postgres?

Let's suppose we have a table called persons with a jsonb column named external_data_provider.

Persons
| id   | name | external_data_provider            |
| ---  | ---  | ---                               |
|1     |Rafael|{id: "123", status: "ok"}          |
|2     |Felipe|{id: "345", status: "missing_docs"}|

To filter all records with status missing_docs, we may do the following:
```
select * from persons where external_data_provider->>'status' = 'missing_docs'
```

The structure then is:
```
select * from {{table}} where {{field}}->>'{{key}}' = {{value}}
```

Persons
| id   | name | external_data_provider            |
| ---  | ---  | ---                               |
|1     |Rafael|{id: "123", status: "ok", job_details: {salary: 130000}}          |
|2     |Felipe|{id: "345", status: "missing_docs", job_details: {salary: 90000}}|

When the field has an object inside another object? For example, how can we filter the ones where current salary is above 100k? We can do this:

```
select * from persons where external_data_provider->job_details->>salary >= 100000
```

```
select * from {{table}} where {{field}}->{{object-key}}->>{{key}} >= 100000
```
