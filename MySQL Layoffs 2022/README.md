# Layoffs Case Study

## Introduction
For this project I did not know what exactly I wanted to do with this information or what I wanted to learn. I wanted to explore and handle the data to see what insights I could get from it.

## Part 1: Cleaning
Data cleaning consisted of: creating a second table identical to the first, find and remove duplicate rows, standardizing data, populate missing data, and removing unnecessary columns. The data cleaning was standard and not very unique which is why I thought it best to not cover it in great detail. If you'd like to see the queries they can be found [here.](https://github.com/CarterR21/Portfolio/blob/main/MySQL%20Layoffs%202022/Exploratory%20Data%20Analysis.sql)

## Part 2: EDA
***
### 1. What were the worst layoffs as a total and percentage?
***
````sql
SELECT MAX(total_laid_off), MAX(percentage_laid_off)
FROM layoffs_staging2;
````
Answer:

![image](https://github.com/user-attachments/assets/b54f5e82-fefd-4d57-8388-97d5cccf0ea6)

Deduction: Here I was curious to see what the extremes were in this data set. We can see a total of 12000 people were let go from a single company, as well as at least one company went under due to the percentage laid off being 100%

### 2. Which companies that went under had the most funds?
***
````sql
SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/a427df3c-6116-46d2-9437-b5af77dd3e17)

Deduction: Curious to see how the amount of funds raised affected comapanies we can see that the companies with medium to small amounts of funding went under much more often than highly funded companies did but not exclusively. An example of a heavily funded company that went under is Britishvolt (a battery manufacturer) which raised over 2 billion in funding and still went out of business. Also note that a large number of companies that went under were based in the United States.

### 3. Which companies had the most total laid off?
***
````sql
SELECT company, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY company
ORDER BY 2 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/7a0635c6-52f7-45bf-ba31-847e609b9801)

Deduction: The top of this list is dominated by companies with numerous amounts so while they are top of total, there is no guarantee that they will have the highest percentages.

### 4. Which industries had the most layoffs?
***
````sql
SELECT industry, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY industry
ORDER BY 2 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/1171db0b-e51a-4db8-91af-e422a82c63df)

Deduction: The most layoffs were in the consumer industry, with the least being in manufacturing. This is likely because of COVID that heavily reduced the ability for consumerism and it was mostly the critical infastructure that had to stay open which allowed for the employees to keep their jobs. Of note: consumer, retail, and transportation having the highest layoffs are clear indicators of this.

### 5. Which countries had the most layoffs?
***
````sql
SELECT country, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY country
ORDER BY 2 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/3aa195f3-3928-4a19-849a-b80f488b9142)

Deduction: The highest layoffs by country is the United States, this could be due to a number of occurances but most likely it is due to the dataset being saturated by United States companies which disproportionatly shows a higher amount of United States layoffs over other countries.

### 6. What is the timespan of this data?
***
````sql
SELECT YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY YEAR(`date`)
ORDER BY 1 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/ba2b564b-1db8-4db0-9c9a-f698565d56d1)

Deduction: Finding the time in which this data is related to is important so we know of world events and can find out what might affect layoffs. An example would be COVID, where layoffs after became a pandemic and again after it was over and companies over hired so they needed to cut back down. 

### 7. Which year had the most layoffs?
***
````sql
SELECT YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY YEAR(`date`)
ORDER BY 1 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/9271724a-ad45-43ff-ae3e-ec5714013b35)

Deduction: There were massive spikes in layoffs in 2020 and 2022, 2020 is likely due to COVID while 2022 is a bit more complex, as companies stated that some layoffs are due to preperation for a recession and speculations that investors had a role to play as well.

### 8. What company stage has the most layoffs?
***
````sql
SELECT stage, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY stage
ORDER BY 2 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/b2a180f7-5545-485b-b87e-9f0fe165cc39)

Deduction: Post-IPO had the msot layoffs and this is expected, the most turbulant time for a company is right after going public as they are adjusting to the change of constant influences they have not exprienced. As a public company they are also more influenced by external forces that may cause for layoffs to be more common.

### 9. How many layoffs by month with a rolling total?
***
````sql
WITH Rolling_Total AS
(
SELECT SUBSTRING(`date`,1,7) AS `MOnth`, SUM(total_laid_off) AS total_off
FROM layoffs_staging2
WHERE SUBSTRING(`date`,1,7) IS NOT NULL
GROUP BY `MONTH`
ORDER BY 1 ASC
)
SELECT `MONTH`, total_off, SUM(total_off) OVER(ORDER BY `MONTH`) AS rolling_total
FROM rolling_total;
````
Answer:

![image](https://github.com/user-attachments/assets/19d7d0fb-8af0-43f2-925e-4e62b71db08b)

Deduction: The biggest spikes of layoffs by month were mid 2020, which is likely due to the COVID pandemic that forced companies to layoff numerous people, and late 2022 to early 2023. This second spree of layoffs coincides with the increased interest rates that were occuring at this time.

### 10. What is the most layoffs by a company in a year?
***
````sql
SELECT company, YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY company, YEAR(`date`)
ORDER BY 3 DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/678dae46-c39a-4c4f-bd82-561175c4ea50)

Deduction: Google holds the record for this in 2023 with 12000 layoffs. This massive wave of layoffs is a more indepth look into the previous question where we can see the companies highest amount of layoffs to see what companies attributed the most to the outcome.

### 11. What are the top company layoffs each year?
***
````sql
WITH company_year (company, years, total_laid_off) AS
(
SELECT company, YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY company, YEAR(`date`)
), company_year_rank AS
(
SELECT *, DENSE_RANK() OVER (PARTITION BY years ORDER BY total_laid_off DESC) AS ranking
FROM COMPANY_YEAR
WHERE years IS NOT NULL
)
SELECT *
FROM company_year_rank
WHERE ranking <= 5;
````
Answer:

![image](https://github.com/user-attachments/assets/751d6091-efe1-4af7-8b3b-5b50afff6a54)

Deduction: 2020-2021 has companies that are in the retail or consumer sectors more than other companies, this is likely due to the drop in travel and ability to buy during COVID. However 2022-2023 is dominated by tech companies, likely due to the reasons stated in question 9.

### 12. What percent of each company was laid of on average
***
````sql
CREATE TEMPORARY TABLE layoffs_staging3
SELECT * FROM layoffs_staging2;

ALTER TABLE layoffs_staging3
ADD total_employees varchar(255);

DELETE
FROM layoffs_staging3
WHERE total_laid_off is null or percentage_laid_off is null;

UPDATE layoffs_staging3
SET total_employees = ROUND(total_laid_off / percentage_laid_off)
WHERE NOT percentage_laid_off = 0;

SELECT company, ROUND(SUM(total_laid_off)/SUM(total_employees),2) AS total_laid_off_by_company
FROM layoffs_staging3
GROUP BY company
ORDER BY total_laid_off_by_company DESC;
````
Answer:

![image](https://github.com/user-attachments/assets/8efc205e-5ac1-4928-838e-983869b6cd68)

Deduction: This querey was a bit more complex than other queries as it required a new table to combine the companies that had seperate rows. The end result shows what the average layoffs a company had over the span of this dataset, from 100% all the way down to .03% with companies that were able to retain more people. These low percent layoff companies tend to be large companies with a large amount of employees and start ups that had few employees but were well funded.

