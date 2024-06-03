# COVID-19 Cases Analysis

## Project Overview

This project focuses on analyzing COVID-19 cases across various countries from January 2020 to April 2021 using SQL. The goal is to provide insights into the spread of the virus, the impact on different regions, and trends over time.

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
| iso_code     | NVARCHAR(255) | ISO code of the country |
| continent     | NVARCHAR(255) | Continent of the country |
| location     | NVARCHAR(255) | Name of the country |
| date     | DATETIME | Date of the report |
| population     | FLOAT | Population of the country |
| total_cases     | FLOAT | Total number of cases |
| new_cases     | FLOAT | Number of new cases |
| total_deaths     | NVARCHAR(255) | Total number of deaths |
| new_deaths     | NVARCHAR(255) | Number of new deaths |

### Table: `CovidVaccinations`

| Column       | Type    | Description                      |
|--------------|---------|----------------------------------|
| iso_code     | NVARCHAR(255) | ISO code of the country |
| continent     | NVARCHAR(255) | Continent of the country |
| location     | NVARCHAR(255) | Name of the country |
| date     | DATETIME | Date of the report |
| total_vaccinations| NVARCHAR(255) | Total number of vaccinations |
| new_vaccinations| NVARCHAR(255) | Number of new vaccinations |

## Contributing

If you'd like to contribute to this project, please fork the repository and use a feature branch. Pull requests are welcome.




