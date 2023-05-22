# SQL-DATA-EXPLORATION-USING-COVID-19-DATA.



---LOOKING AT SELECTED COLUMNS

SELECT LOCATION, Date, Total_Cases, New_Cases, Total_Deaths, Population
FROM CovidDeaths$
ORDER BY 3,4

--LOOKING AT THE TOTAL CASES VS TOTAL DEATHS
SELECT Location, Date, Total_cases, Total_Deaths, (total_Deaths/Total_Cases)*100 AS Deathpercent
FROM CovidDeaths$
WHERE location LIKE '%state%'
ORDER BY 1,2

--LOOKING TOTAL CASES VS POPULATION

SELECT Location, Date, Total_cases,Population, (Total_cases/population)*100 AS percentagepopulationAffected
FROM CovidDeaths$
WHERE Location LIKE '%state%'
ORDER BY 1, 2

---Looking at Countries With Highest infection rate compared to Population
SELECT Location, population, MAX(Total_cases) As HighestInfectionCount,
MAX(Total_cases/population)*100 AS percentagePopulationInfected
FROM CovidDeaths$
GROUP BY Location, Population
ORDER BY percentagePopulationInfected DESC


---Showing Countries with the highest Death count Per population,converted Total Deaths
--- From varchar to int

SELECT Location, population, MAX(Cast(Total_Deaths AS Int)) AS TotalDeathCount
FROM CovidDeaths$
Group By Location, Population
ORDER By TotaldeathCount

--Lets Break Things Down By continent
SELECT Continent, Max(Cast(Total_deaths AS int)) AS TotalDeathCount
FROM CovidDeaths$
WHERE Continent is not NULl
Group By Continent
ORDER BY TotaldeathCount DESC
