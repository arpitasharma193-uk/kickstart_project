# kickstart_project

**created sql kickstart project to gets my hands on.**

**Tools Used: Excel, MySQL, Tableau**

**Questions I Wanted To Answer From the Dataset:**

**for beginners**

1. **List all Kickstarter projects launched in 2015**
 select * from ks_project
Where year(launched) = 2015
;

2. **Find all successful projects.**

select *
from ks_project
where state = 'successful';

3. **Count the number of projects in each category.**

   select count(name) as number_of_project, category
from ks_project
group by name, category;

4.  **Show projects where pledged amount exceeded the goal.**

select goal, pledged, name from ks_project
where goal < pledged ;

5. **Find the top 5 most funded projects (by pledged amount).**

select name, pledged
from ks_project
order by pledged desc
limit 5;

6. **Calculate success rate by category**

SELECT
    category,
    (COUNT(CASE WHEN state = 'success' THEN 1 END) / COUNT(*)) * 100 AS success_rate_percentage
FROM
    ks_project
GROUP BY
    category;

7.**Average pledged amount for successful vs failed projects.**

select avg(pledged) as avg_pledged, state
from ks_project
group by state;


8. **Find the month with the highest number of launches.**
   
SELECT MONTH(launched) AS month, COUNT(*) AS launches
FROM ks_project
GROUP BY MONTH(launched)
ORDER BY launches DESC
LIMIT 1;

10. **Find categories with the highest average funding success ratio (pledged ÷ goal)**

SELECT category,
       AVG(pledged / goal) AS avg_funding_ratio
FROM ks_project
GROUP BY category
ORDER BY avg_funding_ratio DESC;


10. **Find countries with the most successful projects.**

select country, state from ks_project
where state = 'successful'
group by country;

11.**Rank projects by pledged amount within each category.**

select name , category, pledged,
 rank() over ( partition by category order by pledged desc) as rn
  from ks_project;






