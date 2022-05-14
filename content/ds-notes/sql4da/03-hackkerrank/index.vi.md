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
- **FORMAT(number, 'Fm'|'Nm')**: Định dạng số gồm m chữ số phần thập phân.


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
```
{{< /admonition >}}

## 4. Aggregation

## 5. Basic Join

## 6. Advanced Join

## 7. Alternative Queries



## 8. Certificate

Sau khi luyện tập xong, các bạn có thể làm thử bài test để lấy chứng chỉ của [HackerRank](https://www.hackerrank.com/skills-verification). Còn đây là kết quả của mình:

{{< figure src="./hackerrank-basic.png" width=80% >}}

{{< figure src="./hackerrank-intermediate.png" width=80% >}}

