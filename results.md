# SQL Query Example

Below is an example SQL query that retrieves COVID-19 data for Bulgaria from a hypothetical database table named `covid_data`:

```sql
SELECT
    iso_code,
    continent,
    location,
    date,
    population,
    total_cases,
    new_cases,
    total_deaths,
    new_deaths
FROM
    covid_data
WHERE
    location = 'Bulgaria'
ORDER BY
    date;
