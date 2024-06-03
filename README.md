# COVID-19 Cases Analysis

## Project Overview

This project focuses on analyzing COVID-19 cases across various countries using SQL. The goal is to provide insights into the spread of the virus, the impact on different regions, and trends over time.

## Data Source

The data used in this project is sourced from [Our World in Data](https://ourworldindata.org/covid-deaths) and includes daily reports of COVID-19 deaths and vaccinations globally.

## Project Structure

The project is structured as follows:

- **data/**: Contains the raw data files in Excel Workbook format.
- **Covid.sql**: Contains SQL scripts used for data processing and analysis.
- **results/**: Contains output results such as summary tables.

## Database Schema

The database schema consists of the following tables:

### Table: `CovidDeaths`

| Column       | Type    | Description                      |
|--------------|---------|----------------------------------|
| country_id   | INT     | Primary key                      |
| country_name | VARCHAR | Name of the country              |
| iso_code     | VARCHAR | ISO code of the country          |

### Table: `CovidVaccinations`

| Column       | Type    | Description                      |
|--------------|---------|----------------------------------|
| report_id    | INT     | Primary key                      |
| report_date  | DATE    | Date of the report               |
| country_id   | INT     | Foreign key referencing `countries` table |
| cases        | INT     | Number of confirmed cases        |
| recoveries   | INT     | Number of recoveries             |
| deaths       | INT     | Number of deaths                 |

## Contributing

If you'd like to contribute to this project, please fork the repository and use a feature branch. Pull requests are welcome.




