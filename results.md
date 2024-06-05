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
**CovidDeaths**
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

**CovidVaccinations**
| iso_code | continent | location   | date       | new_tests | total_tests | total_vaccinations | new_vaccinations |
|----------|-----------|------------|------------|-----------|-------------|--------------------|------------------|
| AFG      | Asia      | Afghanistan | 2020-02-24 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-02-25 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-02-26 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-02-27 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-02-28 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-02-29 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-03-01 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-03-02 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-03-03 | NULL      | NULL        | NULL               | NULL             |
| AFG      | Asia      | Afghanistan | 2020-03-04 | NULL      | NULL        | NULL               | NULL             |


## 2. Number of deaths and cases until the final day of each country
```sql
SELECT location, MAX(total_deaths) AS final_deaths, MAX(total_cases) AS final_cases, MAX(total_deaths) / MAX(total_cases) * 100 AS final_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location
ORDER BY location
```
| location              | final_deaths | final_cases | final_death_rate     |
|-----------------------|--------------|-------------|----------------------|
| Afghanistan           | 996          | 59745       | 1.66708511172483     |
| Africa                | 99814        | 4557699     | 2.19000859863716     |
| Albania               | 989          | 131085      | 0.754472288972804    |
| Algeria               | 996          | 122108      | 0.815671372883022    |
| Andorra               | 98           | 13232       | 0.740628778718259    |
| Angola                | 96           | 26652       | 0.360198108959928    |
| Anguilla              | NULL         | NULL        | NULL                 |
| Antigua and Barbuda   | 9            | 1232        | 0.73051948051948     |
| Argentina             | 992          | 2977363     | 0.0333180737451228   |
| Armenia               | 995          | 216064      | 0.460511700236967    |

## 3. Total cases and total deaths in a specific country every day
```sql
SELECT location, date, total_cases, total_deaths, total_deaths / total_cases * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date
```
| location | date       | total_cases | total_deaths | death_rate |
|----------|------------|-------------|--------------|------------|
| Vietnam  | 2020-01-23 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-24 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-25 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-26 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-27 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-28 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-29 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-30 | 2           | NULL         | NULL       |
| Vietnam  | 2020-01-31 | 2           | NULL         | NULL       |
| Vietnam  | 2020-02-01 | 6           | NULL         | NULL       |

## 4.  A specific country's daily infection rate (= total cases / population)
```sql
SELECT location, date, total_cases, population, total_cases / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (location = 'Vietnam')
ORDER BY date
```
| location | date       | total_cases | population | infection_rate       |
|----------|------------|-------------|------------|----------------------|
| Vietnam  | 2020-01-23 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-24 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-25 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-26 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-27 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-28 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-29 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-30 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-01-31 | 2           | 97338583   | 2.05468370132325E-06 |
| Vietnam  | 2020-02-01 | 6           | 97338583   | 6.16405110396974E-06 |

## 5. Countries with the highest infection rate (= total cases / population)
```sql
SELECT location, population, MAX(total_cases) AS final_cases, MAX(total_cases) / population * 100 AS infection_rate
FROM     PortfolioProject.dbo.CovidDeaths
GROUP BY location, population
ORDER BY infection_rate DESC, location
```
| location     | population | final_cases | infection_rate      |
|--------------|------------|-------------|---------------------|
| Andorra      | 77265      | 13232       | 17.1254772536077    |
| Montenegro   | 628062     | 97389       | 15.5062716738156    |
| Czechia      | 10708982   | 1630758     | 15.2279460363273    |
| San Marino   | 33938      | 5066        | 14.9272202251164    |
| Slovenia     | 2078932    | 240292      | 11.5584348117206    |
| Luxembourg   | 625976     | 67205       | 10.7360346083556    |
| Bahrain      | 1701583    | 176934      | 10.3981997939566    |
| Serbia       | 6804596    | 689557      | 10.1336949320724    |
| United States| 331002647  | 32346971    | 9.77242064169958    |
| Israel       | 8655541    | 838481      | 9.68721654718059    |
	
## 6. Countries with the highest number of deaths per population
```sql
SELECT location, population, MAX(CAST(total_deaths AS int)) AS final_deaths, MAX(total_deaths) / population * 100 AS death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY location, population
ORDER BY final_deaths DESC, death_rate DESC
```
| location        | population | final_deaths | death_rate            |
|-----------------|------------|--------------|-----------------------|
| United States   | 331002647  | 576232       | 0.0300816325496031    |
| Brazil          | 212559409  | 403781       | 0.0468443154167784    |
| Mexico          | 128932753  | 216907       | 0.0771937290441631    |
| India           | 1380004385 | 211853       | 0.00722990456294818   |
| United Kingdom  | 67886004   | 127775       | 0.145424673987292     |
| Italy           | 60461828   | 120807       | 0.165038013736535     |
| Russia          | 145934460  | 108290       | 0.0683868635276411    |
| France          | 68147687   | 104675       | 0.14664620972389      |
| Germany         | 83783945   | 83097        | 0.0119092028908402    |
| Spain           | 46754783   | 78216        | 0.0200770902946978    |
	
## 7. Continents with the highest number of deaths
```sql
SELECT continent, MAX(CAST(total_deaths AS int)) AS final_deaths
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
GROUP BY continent
ORDER BY final_deaths DESC
```
| continent      | final_deaths |
|----------------|--------------|
| North America  | 576232       |
| South America  | 403781       |
| Asia           | 211853       |
| Europe         | 127775       |
| Africa         | 54350        |
| Oceania        | 910          |
	
## 8. Total number of cases, deaths, and death rate in the world
```sql
SELECT SUM(new_cases) AS global_cases, SUM(CAST(new_deaths AS int)) AS global_deaths, SUM(CAST(new_deaths AS int)) / SUM(new_cases) * 100 AS global_death_rate
FROM     PortfolioProject.dbo.CovidDeaths
WHERE  (continent IS NOT NULL)
```
| global_cases | global_deaths | global_death_rate |
|--------------|---------------|-------------------|
| 150574977    | 3180206       | 2.11204149810363  |
	
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
| location | date       | population | new_vaccinations | total_vaccinations | vaccination_rate     |
|----------|------------|------------|------------------|--------------------|----------------------|
| Albania  | 2021-01-13 | 2877800    | 60               | 60                 | 0.00208492598512753  |
| Albania  | 2021-01-14 | 2877800    | 78               | 138                | 0.00479532976579331  |
| Albania  | 2021-01-15 | 2877800    | 42               | 180                | 0.00625477795538258  |
| Albania  | 2021-01-16 | 2877800    | 61               | 241                | 0.0083744527069289   |
| Albania  | 2021-01-17 | 2877800    | 36               | 277                | 0.00962540829800542  |
| Albania  | 2021-01-18 | 2877800    | 42               | 319                | 0.0110848564875947   |
| Albania  | 2021-01-19 | 2877800    | 36               | 355                | 0.0123358120786712   |
| Albania  | 2021-01-20 | 2877800    | 36               | 391                | 0.0135867676697477   |
| Albania  | 2021-01-21 | 2877800    | 30               | 421                | 0.0146292306623115   |
| Albania  | 2021-01-22 | 2877800    | NULL             | 421                | 0.0146292306623115   |
