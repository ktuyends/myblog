---
title: "SQL Notes - HackerRank"
subtitle: ""
slug: sql-hackerrank
date: 2022-05-13
lastmod: 2022-05-13
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["SQL", "SQL for DA"]
categories: []
series: [SQL for Data Analysis]
series_weight: 3
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Giới thiệu HackerRank

Sau khi đã đi qua rất là nhiều kiến thức về SQL trong hai bài đầu tiên của [Series - SQL for Data Analysis](./databases-and-dbms/), thì cũng đã đến lúc chúng ta bắt tay vào thực hành với một số ví dụ đơn giản ở trang [HackerRank](https://www.hackerrank.com/domains/sql). 

Bài viết này là tổng hợp lời giải của mình về các câu hỏi ở HackerRank. Mình sẽ sử dụng hệ quản trị CSDL là SQL Server. 

Lưu ý là với mỗi DBMS, các hàm xử lý dữ liệu đôi khi không giống nhau. Một số hàm mình sử dụng:

- **LEN()**: Số lượng các ký tự của một chuỗi.
- **LEFT()**: Lấy ra một số lượng các ký tự nhất định tính từ bên trái.
- **RIGHT()**: Lấy ra một số lượng các ký tự nhất định tính từ bên phải.
- **CONCAT()**: Hàm nối các chuỗi ký tự.
- **COUNT()**: Hàm đếm số lượng các record không NULL.
- **FORMAT(number, 'Fm'|'Nm')**: Định dạng số gồm m chữ số phần thập phân, trả về kiểu string.
- **ROUND(number, n)**: Làm tròn đến n chữ số thập phân.
- **CEILING(), FLOOR()**: Làm tròn đến số nguyên gần nhất.
- **CAST(column AS datatype)**: Chuyển đổi kiểu dữ liệu. 
- **TOP 50 PERCENT**: Lấy ra `50%` records.


## 2. Basic Select

{{< admonition type=success title="1. Revising the Select Query I" open=false >}}
```sql
SELECT *
FROM CITY
WHERE COUNTRYCODE = 'USA'
AND POPULATION > 100000;
```
{{< /admonition >}}

{{< admonition type=success title="2. Revising the Select Query II" open=false >}}
```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'USA'
AND POPULATION > 120000;
```
{{< /admonition >}}

{{< admonition type=success title="3. Select All" open=false >}}
```sql
SELECT *
FROM CITY;
```
{{< /admonition >}}

{{< admonition type=success title="4. Select By ID" open=false >}}
```sql
SELECT *
FROM CITY
WHERE ID = 1661;
```
{{< /admonition >}}

{{< admonition type=success title="5. Japanese Cities' Attributes" open=false >}}
```sql
SELECT *
FROM CITY
WHERE CountryCode = 'JPN';
```
{{< /admonition >}}

{{< admonition type=success title="6. Japanese Cities' Names" open=false >}}
```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```
{{< /admonition >}}

{{< admonition type=success title="7. Weather Observation Station 1" open=false >}}
```sql
SELECT CITY, STATE
FROM STATION;
```
{{< /admonition >}}

{{< admonition type=success title="8. Weather Observation Station 3" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID % 2 = 0;
```
{{< /admonition >}}

{{< admonition type=success title="9. Weather Observation Station 4" open=false >}}
```sql
SELECT COUNT(CITY) - COUNT (DISTINCT CITY)
FROM STATION;
```
{{< /admonition >}}

{{< admonition type=success title="10. Weather Observation Station 5" open=false >}}
```sql
SELECT TOP 1 CITY, LEN(CITY)
FROM STATION
ORDER BY LEN(CITY), CITY;
UNION
SELECT TOP 1 CITY, LEN(CITY)
FROM STATION
ORDER BY LEN(CITY) DESC, CITY;
```
{{< /admonition >}}

{{< admonition type=success title="11. Weather Observation Station 6" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '[aeiou]%';
```
{{< /admonition >}}

{{< admonition type=success title="12. Weather Observation Station 7" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%[aeiou]';
```
{{< /admonition >}}

{{< admonition type=success title="13. Weather Observation Station 8" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '[aeiou]%[aeiou]';
```
{{< /admonition >}}

{{< admonition type=success title="14. Weather Observation Station 9" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '[aeiou]%';
```
{{< /admonition >}}

{{< admonition type=success title="15. Weather Observation Station 10" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '%[aeiou]';
```
{{< /admonition >}}

{{< admonition type=success title="16. Weather Observation Station 11" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '[aeiou]%[aeiou]';
```
{{< /admonition >}}

{{< admonition type=success title="17. Weather Observation Station 12" open=false >}}
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '[^aeiou]%[^aeiou]';
```
{{< /admonition >}}

{{< admonition type=success title="18. Higher Than 75 Marks" open=false >}}
```sql
SELECT NAME
FROM STUDENTS
WHERE MARKS > 75
ORDER BY RIGHT(NAME, 3), ID;
```
{{< /admonition >}}

{{< admonition type=success title="19. Employee Names" open=false >}}
```sql
SELECT NAME
FROM EMPLOYEE
ORDER BY NAME;
```
{{< /admonition >}}

{{< admonition type=success title="20. Employee Salaries" open=false >}}
```sql
SELECT NAME
FROM EMPLOYEE
WHERE SALARY > 2000 AND MONTHS < 10
ORDER BY EMPLOYEE_ID;
```
{{< /admonition >}}

## 3. Advanced Select

{{< admonition type=success title="21. Type of Triangle" open=false >}}
```sql
SELECT CASE             
            WHEN A + B > C AND B + C > A AND A + C > B THEN
                CASE 
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                    ELSE 'Scalene'
                END
            ELSE 'Not A Triangle'
        END
FROM TRIANGLES;
```
{{< /admonition >}}

{{< admonition type=success title="22. The PADS" open=false >}}
```sql
SELECT CONCAT(NAME, '(', LEFT(OCCUPATION, 1), ')')
FROM OCCUPATIONS
ORDER BY NAME;

SELECT CONCAT('There are a total of ', COUNT(OCCUPATION), ' ', LOWER(OCCUPATION), 's.')
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION), OCCUPATION;
```
{{< /admonition >}}

{{< admonition type=success title="23. Occupations" open=false >}}
```sql
SELECT Doctor
     , Professor
     , Singer
     , Actor
FROM (
SELECT 
    Row_Number() Over(Partition By Occupation Order by Name) AS row_no
  , Occupation
  , Name
FROM Occupations
) PivotData
PIVOT 
(
    Max(Name) For Occupation in ([Doctor], [Professor], [Singer], [Actor])
) PivotTable
```
{{< /admonition >}}

{{< admonition type=success title="24. Binary Tree Nodes" open=false >}}
```sql
SELECT CASE
    WHEN P IS NULL THEN CONCAT(N, ' Root')
    WHEN N IN (SELECT DISTINCT P FROM BST) THEN CONCAT(N, ' Inner')
    ELSE CONCAT(N, ' Leaf')
    END
FROM BST
ORDER BY N ASC;
```
{{< /admonition >}}

{{< admonition type=success title="25. New Companies" open=false >}}
```sql  
SELECT c.company_code
     , c.founder
     , COUNT(DISTINCT l.lead_manager_code)
     , COUNT(DISTINCT s.senior_manager_code)
     , COUNT(DISTINCT m.manager_code)
     , COUNT(DISTINCT e.employee_code) 
FROM Company c, Lead_Manager l, Senior_Manager s, Manager m, Employee e 
WHERE c.company_code = l.company_code 
    AND l.lead_manager_code=s.lead_manager_code 
    AND s.senior_manager_code=m.senior_manager_code 
    AND m.manager_code=e.manager_code 
GROUP BY c.company_code, c.founder
ORDER BY c.company_code;
```
{{< /admonition >}}

## 4. Aggregation

{{< admonition type=success title="26. Revising Aggregations - The Count Function" open=false >}}
```sql
SELECT COUNT(NAME)
FROM CITY
WHERE POPULATION > 100000;
```
{{< /admonition >}}

{{< admonition type=success title="27. Revising Aggregations - The Sum Function" open=false >}}
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'California';
```
{{< /admonition >}}

{{< admonition type=success title="28. Revising Aggregations - Averages" open=false >}}
```sql
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT = 'California';
```
{{< /admonition >}}

{{< admonition type=success title="29. Average Population" open=false >}}
```sql
SELECT ROUND(AVG(POPULATION), 0)
FROM CITY;  
```
{{< /admonition >}}

{{< admonition type=success title="30. Japan Population" open=false >}}
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```
{{< /admonition >}}

{{< admonition type=success title="31. Population Density Difference" open=false >}}
```sql
SELECT MAX(POPULATION) - MIN(POPULATION)
FROM CITY;
```
{{< /admonition >}}

{{< admonition type=success title="32. The Blunder" open=false >}}
```sql
SELECT CAST(CEILING(AVG(CAST(Salary AS Float)) - AVG(CAST(REPLACE(Salary, 0, '')AS Float))) AS INT)
FROM EMPLOYEES;
```
{{< /admonition >}}

{{< admonition type=success title="33. Top Earners" open=false >}}
```sql
SELECT TOP 1 MAX(MONTHS * SALARY), COUNT(*)
FROM EMPLOYEE
GROUP BY MONTHS * SALARY
ORDER BY MONTHS * SALARY DESC;
```
{{< /admonition >}}

{{< admonition type=success title="34. Weather Observation Station 2" open=false >}}
```sql
SELECT FORMAT(SUM(LAT_N), 'F2') AS lat, FORMAT(SUM(LONG_W), 'F2') AS lon
FROM STATION;
```
{{< /admonition >}}

{{< admonition type=success title="35. Weather Observation Station 13" open=false >}}
```sql
SELECT FORMAT(SUM(LAT_N), 'F4')
FROM STATION
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
```
{{< /admonition >}}

{{< admonition type=success title="36. Weather Observation Station 14" open=false >}}
```sql
SELECT FORMAT(MAX(LAT_N), 'F4')
FROM STATION
WHERE LAT_N < 137.2345;
```
{{< /admonition >}}

{{< admonition type=success title="37. Weather Observation Station 15" open=false >}}
```sql
SELECT FORMAT(LONG_W, 'F4')
FROM STATION
WHERE LAT_N = (SELECT MAX(LAT_N)
               FROM STATION
               WHERE LAT_N < 137.2345);
```
{{< /admonition >}}

{{< admonition type=success title="38. Weather Observation Station 16" open=false >}}
```sql
SELECT FORMAT(MIN(LAT_N), 'F4')
FROM STATION
WHERE LAT_N > 38.7780;
```
{{< /admonition >}}

{{< admonition type=success title="39. Weather Observation Station 17" open=false >}}
```sql
SELECT FORMAT(LONG_W, 'F4')
FROM STATION
WHERE LAT_N = (SELECT MIN(LAT_N)
               FROM STATION
               WHERE LAT_N > 38.7780);
```
{{< /admonition >}}

{{< admonition type=success title="40. Weather Observation Station 18" open=false >}}
```sql
SELECT FORMAT(MAX(LAT_N) - MIN(LAT_N) + MAX(LONG_W) - MIN(LONG_W), 'F4')
FROM STATION;
```
{{< /admonition >}}

{{< admonition type=success title="41. Weather Observation Station 19" open=false >}}
```sql
SELECT FORMAT(SQRT(POWER(MAX(LAT_N) - MIN(LAT_N) ,2) + POWER(MAX(LONG_W) - MIN(LONG_W) ,2)), 'F4')
FROM STATION;
```
{{< /admonition >}}

{{< admonition type=success title="42. Weather Observation Station 20" open=false >}}
```sql
SELECT FORMAT((
    (SELECT MAX(LAT_N)
    FROM (
        SELECT TOP 50 PERCENT LAT_N
        FROM STATION
        ORDER BY LAT_N
    ) AS BotHalf)
    +
    (SELECT MIN(LAT_N)
    FROM (
        SELECT TOP 50 PERCENT LAT_N
        FROM STATION
        ORDER BY LAT_N DESC
    ) AS TopHafl)
) / 2, 'F4') AS MEDIAN
```
{{< /admonition >}}


## 5. Basic Join

{{< admonition type=success title="43. Population Census" open=false >}}
```sql
SELECT SUM(CI.POPULATION)
FROM CITY CI 
JOIN COUNTRY CO ON CI.COUNTRYCODE = CO.CODE
WHERE CO.CONTINENT = 'ASIA';
```
{{< /admonition >}}


{{< admonition type=success title="44. African Cities" open=false >}}
```sql
SELECT CI.NAME
FROM CITY CI 
JOIN COUNTRY CO ON CI.COUNTRYCODE = CO.CODE
WHERE CO.CONTINENT = 'AFRICA';
```
{{< /admonition >}}

{{< admonition type=success title="45. Average Population of Each Continent" open=false >}}
```sql
SELECT CO.CONTINENT, FLOOR(AVG(CI.POPULATION))
FROM CITY CI 
JOIN COUNTRY CO ON CI.COUNTRYCODE = CO.CODE
GROUP BY CO.CONTINENT;
```
{{< /admonition >}}

{{< admonition type=success title="46. The Report" open=false >}}
```sql
SELECT CASE WHEN GR.GRADE >= 8 THEN ST.NAME
       ELSE NULL END AS NAME, GR.GRADE, ST.MARKS
FROM STUDENTS ST 
JOIN GRADES GR ON ST.MARKS >= GR.MIN_MARK
               AND ST.MARKS <= GR.MAX_MARK
ORDER BY GR.GRADE DESC, ST.NAME;
```
{{< /admonition >}}

{{< admonition type=success title="47. Top Competitors" open=false >}}
```sql
SELECT H.hacker_id, H.name
FROM Submissions S 
JOIN Challenges C ON S.challenge_id = C.challenge_id
JOIN Difficulty D ON C.difficulty_level = D.difficulty_level
JOIN Hackers H ON S.hacker_id = H.hacker_id
WHERE C.difficulty_level = D.difficulty_level AND S.Score = D.Score
GROUP BY H.hacker_id, H.name
HAVING COUNT(H.hacker_id) > 1
ORDER BY COUNT(H.hacker_id) DESC, H.hacker_id;
```
{{< /admonition >}}

{{< admonition type=success title="48. Ollivander's Inventory" open=false >}}

**Phân tích bài toán:**

_Mục tiêu:_ Lựa chọn những cây đũa phép thuật non-evil mà có cặp (power, age) có giá nhỏ nhất.

_Output:_ id, age (secondary order in DESC), coins_needed, power (primary order in DESC)   

Bảng Wands:

| Column | Type |
|:-:|-|
| id | integer |
| code | integer |
| coins_needed | integer |
| power | integer |

Bảng Wands_Property

| Column | Type |
|:-:|-|
| code | integer |
| age | integer |
| is_evil | integer (0 is not evil)|

```sql
--Bước 1: Xác định min coins
WITH Min_gold AS (
SELECT MIN(W.Coins_needed) OVER (PARTITION BY WP.age, W.power) AS min_coins
     , W.id
     , W.coins_needed
     , WP.age
     , W.power
FROM Wands W 
JOIN Wands_Property WP ON W.Code = WP.Code
WHERE WP.is_evil = 0)

-- Bước 2, xác định những coins_needed = min_coins
SELECT id
     , age
     , coins_needed
     , power
FROM Min_gold
WHERE coins_needed = min_coins
ORDER BY Power DESC, age DESC;
```
{{< /admonition >}}

{{< admonition type=success title="49. Challenges" open=false >}}
```sql
-- Tính tổng challanges cho từng người
WITH data
AS
(
SELECT c.hacker_id as id, h.name as name, count(c.hacker_id) as counter
FROM Hackers h
JOIN Challenges c ON c.hacker_id = h.hacker_id
GROUP BY c.hacker_id, h.name
)

-- Kết quả
SELECT id, name, counter
FROM data
WHERE counter = (SELECT max(counter) FROM data) 
OR counter in (SELECT counter 
               FROM data
               GROUP BY counter
               HAVING count(counter) = 1 )
ORDER BY counter desc, id
```
{{< /admonition >}}

{{< admonition type=success title="50. Contest Leaderboard" open=false >}}
```sql
-- Tạo bảng max score
WITH data AS 
(
SELECT H.hacker_id as id
     , H.name as name
     , S.challenge_id 
     , MAX(S.score) as max_score 
FROM Hackers H
JOIN Submissions S ON H.hacker_id = S.hacker_id
GROUP BY H.hacker_id, H.name, S.challenge_id
)

-- Kết quả
SELECT id, name, sum(max_score)
FROM data
GROUP BY id, name
HAVING sum(max_score) > 0
ORDER BY sum(max_score) DESC, id;
```
{{< /admonition >}}

## 6. Advanced Join

{{< admonition type=success title="51. SQL Project Planning" open=false >}}
```sql
WITH Project_stat_date AS 
(
SELECT Start_date,
       RANK() OVER (ORDER BY Start_date) AS Rank_start
FROM Projects
WHERE Start_date NOT IN (SELECT End_date From Projects)
), 

Project_end_date AS 
(
SELECT End_date,
       RANK() OVER (ORDER BY End_date) AS Rank_end
FROM Projects
WHERE End_date NOT IN (SELECT Start_date From Projects)
)

SELECT Start_date
     , End_date
FROM Project_stat_date SD, Project_end_date ED
WHERE Rank_start = Rank_end
ORDER BY DATEDIFF(day, Start_date, End_date), Start_date;
```
{{< /admonition >}}

{{< admonition type=success title="52. Placements" open=false >}}
```sql
-- student salary
WITH student_salary AS 
(
SELECT S.id AS id
     , S.name AS Name
     , P.salary As Salary
FROM Students S 
JOIN Packages P ON S.id = P.id
),

-- Friend salary
friends_salary AS 
(
SELECT F.id AS id
     , F.Friend_id AS Friend_id
     , P.salary AS Friend_salary
FROM Friends F 
JOIN Packages P ON F.Friend_id = P.id
)

-- Result
SELECT S.Name
FROM student_salary S
JOIN friends_salary F ON S.id = F.id
WHERE F.Friend_salary > S.Salary
ORDER BY F.Friend_salary
```
{{< /admonition >}}



{{< admonition type=success title="53. Symmetric Pairs" open=false >}}
```sql
SELECT F1.X, F1.Y
FROM Functions F1 
JOIN Functions F2 ON F1.X = F2.Y and F1.Y = F2.X
GROUP BY F1.X, F1.Y
HAVING F1.X < F1.Y OR COUNT(F1.X) > 1
ORDER BY F1.X
```
{{< /admonition >}}



{{< admonition type=success title="54. Interviews" open=false >}}
```sql
SELECT con.contest_id
     , con.hacker_id
     , con.name
     , SUM(total_submissions)
     , SUM(total_accepted_submissions)
     , SUM(total_views)
     , SUM(total_unique_views)
FROM contests con 
JOIN colleges col ON con.contest_id = col.contest_id 
JOIN challenges cha ON  col.college_id = cha.college_id 
LEFT JOIN
        (SELECT challenge_id
              , SUM(total_views) AS total_views
              , SUM(total_unique_views) AS total_unique_views
         FROM view_stats 
         GROUP BY challenge_id) vs ON cha.challenge_id = vs.challenge_id 
LEFT JOIN
       (SELECT challenge_id
             , SUM(total_submissions) AS total_submissions
             , SUM(total_accepted_submissions) AS total_accepted_submissions 
        FROM submission_stats 
        GROUP BY challenge_id) ss ON cha.challenge_id = ss.challenge_id
GROUP BY con.contest_id, con.hacker_id, con.name
HAVING SUM(total_submissions)!=0 OR 
       SUM(total_accepted_submissions)!=0 OR
       SUM(total_views)!=0 OR
       SUM(total_unique_views)!=0
ORDER BY contest_id;
```
{{< /admonition >}}


{{< admonition type=success title="55. 15 Days of Learning SQL" open=false >}}

**Phân tích yêu cầu bài toán:**

Với mỗi ngày _(sorted by the date)_:

- Tính tổng số hacker _(không tính trùng lặp)_ mà đã nộp bài thi mỗi ngày ít nhất một bài.
- Tìm ra tên hacker mà có `hacker_id` thấp nhất trong số những hacker nộp nhiều bài thi nhất. 


```sql
-- Đếm số Submission của mỗi hacker mỗi ngày
WITH SubCount AS
(
SELECT submission_date, hacker_id, COUNT(*) AS Total_sub
FROM Submissions
GROUP BY submission_date, hacker_id
)

-- Từ bảng trên, tìm hacker có max submission và min hacker_id
WITH MaxSubEachDay AS
(
SELECT submission_date
     , hacker_id
     , ROW_NUMBER() OVER (PARTITION BY submission_date 
                          ORDER BY Total_sub DESC, hacker_id) AS Rn
FROM SubCount
)

-- Đánh số hạng cho từng ngày
WITH Rankday AS 
(
SELECT submission_date
     , hacker_id
     , DENSE_RANK() OVER(ORDER BY submission_date) AS DayRn
FROM submissions
)

-- Tạo cột, nếu hôm trước mà xuất hiện hacker thì hôm sau = hôm trước + 1
WITH RankPrevDay AS 
(
SELECT RD.submission_date,
       RD.hacker_id,
       CASE WHEN RD.submission_date = '2016-03-01' THEN 1
            ELSE 1 + (SELECT COUNT(DISTINCT S.submission_date)                         
                      FROM Submissions S 
                      WHERE S.hacker_id = RD.hacker_id 
                        AND S.submission_date < RD.submission_date)
       END AS PrevDayRn,
       RD.DayRn
FROM Rankday RD
)

-- Hacker id cần tìm là những người có PrevDayRn = DayRn
WITH HackerSubEachDay AS 
(
SELECT submission_date
     , COUNT(DISTINCT hacker_id) total_hacker_each_day
FROM RankPrevDay
WHERE PrevDayRn = DayRn
GROUP BY submission_date
)

-- Tổng hợp kết quả
SELECT HS.submission_date
     , HS.total_hacker_each_day
     , M.hacker_id
     , H.name
FROM HackerSubEachDay HS
JOIN MaxSubEachDay M ON HS.submission_date = M.submission_date
JOIN Hackers H ON H.hacker_id = M.hacker_id
WHERE M.Rn = 1
```
{{< /admonition >}}


## 8. Certificate

Sau khi luyện tập xong, các bạn có thể làm thử bài test để lấy chứng chỉ của [HackerRank](https://www.hackerrank.com/skills-verification). Còn đây là kết quả của mình:

{{< figure src="./hackerrank-basic.png" width=80% >}}

{{< figure src="./hackerrank-intermediate.png" width=80% >}}

