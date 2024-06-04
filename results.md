# SQL Query Results
_The following tables only show the first 10 rows of the actual result._

## 1. Explore the data from 2 tables
```sql
SELECT iso_code, continent, location, date, population, total_cases, new_cases, total_deaths, new_deaths
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NULL)
ORDER BY location, date

SELECT iso_code, continent, location, date, new_tests, total_tests, total_vaccinations, new_vaccinations
FROM     PortfolioProject.dbo.CovidVaccinations
ORDER BY location, date
```
| iso_code | continent | location | date       | population | total_cases | new_cases | total_deaths | new_deaths |
|----------|-----------|----------|------------|------------|-------------|-----------|--------------|------------|
| BGR      | Europe    | Bulgaria | 2020-10-22 | 6,948,445  | 34,930      | 1,595     | 1,064        | 16         |
| BGR      | Europe    | Bulgaria | 2020-10-23 | 6,948,445  | 36,519      | 1,589     | 1,077        | 13         |
| BGR      | Europe    | Bulgaria | 2020-10-24 | 6,948,445  | 37,562      | 1,043     | 1,084        | 7          |
| BGR      | Europe    | Bulgaria | 2020-10-25 | 6,948,445  | 37,889      | 327       | 1,094        | 10         |
| BGR      | Europe    | Bulgaria | 2020-10-26 | 6,948,445  | 40,132      | 2,243     | 1,136        | 42         |
| BGR      | Europe    | Bulgaria | 2020-10-27 | 6,948,445  | 42,701      | 2,569     | 1,161        | 25         |
| BGR      | Europe    | Bulgaria | 2020-10-28 | 6,948,445  | 45,461      | 2,760     | 1,197        | 36         |
| BGR      | Europe    | Bulgaria | 2020-10-29 | 6,948,445  | 48,150      | 2,689     | 1,225        | 28         |
| BGR      | Europe    | Bulgaria | 2020-10-30 | 6,948,445  | 51,041      | 2,891     | 1,254        | 29         |
| BGR      | Europe    | Bulgaria | 2020-10-31 | 6,948,445  | 52,844      | 1,803     | 1,279        | 25         |




## 2. Number of deaths and cases on the final day of each country
```sql
SELECT location, MAX(total_deaths) AS final_deaths, MAX(total_cases) AS final_cases, MAX(total_deaths) / MAX(total_cases) * 100 AS final_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location
ORDER BY location
```


## 3. Total cases and total deaths in a specific country every day
```sql
SELECT location, date, total_cases, total_deaths, total_deaths / total_cases * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date
```

## 4.  A specific country's daily infection rate (= total cases / population)
```sql
SELECT location, date, total_cases, population, total_cases / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date
```

## 5. Countries with the highest infection rate (= total cases / population)
```sql
SELECT location, population, MAX(total_cases) AS final_cases, MAX(total_cases) / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location, population
ORDER BY infection_rate DESC, location
```
	
## 6. Countries with the highest number of deaths per population
```sql
SELECT location, population, MAX(CAST(total_deaths AS int)) AS final_deaths, MAX(total_deaths) / population * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY location, population
ORDER BY final_deaths DESC, death_rate DESC
```
	
## 7. Continents with the highest number of deaths
```sql
SELECT continent, MAX(CAST(total_deaths AS int)) AS final_deaths
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY continent
ORDER BY final_deaths DESC
```
	
## 8. Total number of cases, deaths, and death rate in the world
```sql
SELECT SUM(new_cases) AS global_cases, SUM(CAST(new_deaths AS int)) AS global_deaths, SUM(CAST(new_deaths AS int)) / SUM(new_cases) * 100 AS global_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
```
	
## 9. Vaccination rate around the world every day
```sql
WITH VaccinationPopulation
AS (
	SELECT d.continent, d.location, d.date, d.population, v.new_vaccinations, sum(CONVERT(int, new_vaccinations)) OVER 
		(partition by d.location ORDER BY  d.date) total_vaccinations
	FROM PortfolioProject.dbo.CovidDeaths d
	JOIN PortfolioProject.dbo.CovidVaccinations v 
		ON d.location = v.location
		AND d.date = v.date
	WHERE d.continent is NOT null
)

SELECT location, date, population, new_vaccinations, total_vaccinations, total_vaccinations / population * 100 AS vaccination_rate
FROM     VaccinationPopulation
WHERE  (total_vaccinations IS NOT NULL)
ORDER BY location, date
```
