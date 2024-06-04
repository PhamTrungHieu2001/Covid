# SQL Query Results

## 1. EXPLORE THE DATA FROM 2 TABLES
```sql
SELECT iso_code, continent, location, date, population, total_cases, new_cases, total_deaths, new_deaths
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NULL)
ORDER BY location, date

SELECT iso_code, continent, location, date, new_tests, total_tests, total_vaccinations, new_vaccinations
FROM     PortfolioProject.dbo.CovidVaccinations
ORDER BY location, date

## 2. NUMBER OF DEATHS AND CASES ON THE FINAL DAY OF EACH COUNTRY
```sql
SELECT location, MAX(total_deaths) AS final_deaths, MAX(total_cases) AS final_cases, MAX(total_deaths) / MAX(total_cases) * 100 AS final_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location
ORDER BY location

## 3. TOTAL CASES AND TOTAL DEATHS IN A SPECIFIC COUNTRY EVERY DAY
```sql
SELECT location, date, total_cases, total_deaths, total_deaths / total_cases * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date

## 4. A SPECIFIC COUNTRY'S DAILY INFECTION RATE (= TOTAL CASES / POPULATION)
```sql
SELECT location, date, total_cases, population, total_cases / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date

	
-- 5. COUNTRIES WITH THE HIGHEST INFECTION RATE (= TOTAL CASES / POPULATION)
SELECT location, population, MAX(total_cases) AS final_cases, MAX(total_cases) / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location, population
ORDER BY infection_rate DESC, location

	
-- 6. COUNTRIES WITH THE HIGHEST NUMBER OF DEATHS PER POPULATION
SELECT location, population, MAX(CAST(total_deaths AS int)) AS final_deaths, MAX(total_deaths) / population * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY location, population
ORDER BY final_deaths DESC, death_rate DESC

	
-- 7. CONTINENTS WITH THE HIGHEST NUMBER OF DEATHS
SELECT continent, MAX(CAST(total_deaths AS int)) AS final_deaths
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY continent
ORDER BY final_deaths DESC

	
-- 8. TOTAL NUMBER OF CASES, TOTAL NUMBER OF DEATHS, AND DEATH RATE IN THE WORLD
SELECT SUM(new_cases) AS global_cases, SUM(CAST(new_deaths AS int)) AS global_deaths, SUM(CAST(new_deaths AS int)) / SUM(new_cases) * 100 AS global_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)

	
-- 9. VACCINATION RATE AROUND THE WORLD EVERY DAY
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
