# MY SQL 문법 정리

## 1. SELECT 

#### 1. 필요한 column만 호출 

```sql
SELECT target column
FROM DB.TABLE;
```

#### 2. 개수

```sql
SELECT COUNT(sth)
FROM DB.TABLE;
```

#### 3. 집계 (sum)

```sql
SELECT SUM(amount),
COUNT(number)
FROM DB.TABLE;
```

#### 4. *(asterisk)는 모든 결과 조회

```sql
SELECT *
FROM DB.TABLE;
```

#### 5. 만약 column을 출력하고 싶다면?

```sql
SELECT column1, column2
FROM DB.TABLE;
```

#### 6. AS

* 특정 column이름 변경

```sql
SELECT column1 AS sth
FROM DB.TABLE;
```

```sql
SELECT COUNT(PRODUCTCODE) AS N_PRODUCTS
COUNT(PRODUCTCODE) N_PRODUCTS
FROM DB.PRODUCTS;
```

#### 7. DISTINCT

* 중복을 제외하고 데이터 조회

```sql
SELECT DISTINCT STH
FROM DB.TABLE;
```



# 2. WEHRE

#### 1. 조건추가

```sql
SELECT STH
FROM DB.TABLE
WHERE STH = 'STH';
```

```sql
SELECT PRODUCTNAME
FROM DB.PRODUCT
WHERE COUNTRY = 'USA';
```

#### 2. BETWEEN

* 특정 column의 값이 시작점 - 끝점인 데이터만 출력할 수 있는 조건 생성

```sql
SELECT *
FROM DB.TABLE
WHERE COLUMN BETWEEN START_POINT AND END_POINT;
```

```sql
SELECT PRODUCTNAME
FROM DB.PRODUCT
WHERE YEAR BETWEEN 2019 AND 2021;
```

#### 3. 대소관계

|  연산자  |   설명    |
| :------: | :-------: |
|    =     | 동일하다  |
|    >     |   초과    |
|    >=    |   이상    |
|    <     |   미만    |
|    <=    |   이하    |
| <> or != | 같지 않다 |

```sql
SELECT PRODUCTNAME
FROM DB.PRODUCT
WHERE YEAR =< 2021;
```

#### 4. IN

* 여러 조건 만족하는 리스트 출력

```sql
SELECT COLUMN
FROM DB.TABLE
WHERE COLUMN IN (VALUE1, VALUE2);
```

```sql
SELECT PRODUCTNAME
FROM DB.PRODUCT
WHERE COUNTRY IN ('USA','UK');
```

#### 5. NOT IN

* 특정값들을 제외한 결과 출력

```sql
SELECT PRODUCTNAME
FROM DB.PRODUCT
WHERE COUNTRY NOT IN ('USA','UK');
```

#### 6. IS NULL / IS NOT NULL

* NULL 출력 / NULL값 제외하고 출력

```sql
SELECT PRODUCT
FROM DB.PRODUCT
WHERE REPORTSTO IS NULL;
```

```sql
SELECT PRODUCT
FROM DB.PRODUCT
WHERE REPORTSTO IS NOT NULL;
```

#### 7. LIKE

* 특정 단어가 들어간 데이터 조회

```sql
SELECT *
FROM DB.CUSTOMER
WHERE ADDRESS LIKE '%ST%';
```

```sql
SELECT *
FROM DB.CUSTOMER
WHERE ADDRESS LIKE '%_T%'
```

# 3. GROUP BY

* column의 값을 그룹화 해 각 값들의 평균 값, 개수 등을 구할 때 사용

```sql
SELECT COUNTRY, CITY,
COUNT(CUSTOMERNUMBER) N_CUSTOMERS
FROM DB.CUSTOMERS
GROUP BY COUNTRY, CITY # 국가별, 도시별 고객의 수 (count)
```

|  함수   |    의미     |
| :-----: | :---------: |
|  AVG()  |    평균     |
| COUNT() | 개수 구하기 |
|  SUM()  |    합계     |

#### cf. CASE WHEN 



```sql
SELECT SUM(CASE WHEN COUNTRY = 'USA' THEN 1 ELSE 0) N_USA,# USA 거주자의 수 
SUM(CASE WHEN COUNTRY = 'USA' THEN 1 ELSE 0 END)/COUNT(*) USA_PROPORTION # USA 거주자의 비중
FROM DB.CUSTOMERS;
```

# 4. JOIN

* 여러가지 테이블을 하나로 결합 

#### 1. LEFT JOIN (LEFT OUTER JOIN)

* 특정 테이블 정보를 기준으로 타 테이블을 결합 

```sql
SELECT A.ORDERNUMBER, B.COUNTRY
FROM DB.ORDERS A
LEFT JOIN DB.CUSTOMERS B
ON A.CUSTOMERNUMBER = B.CUSTOMERNUMBER
WHERE B.COUNTRY = 'USA' # 거주지가 USA인
```

#### 2. INNER JOIN

* 2가지 테이블에 공통으로 존재하는 정보만 출력 

```sql
SELECT *
FROM TABLE_A
INNER JOIN TABLE_B
ON TABLE_A.COLUMN1 = TABLE_B.COLUMN 2
```

#### 3. FULL JOIN

* 첫번째 테이블 또는 두번째 테이블과 매칭되는 레코드 모두 출력
* 그렇기 때문에 결과는  매우 큰 데이터 세트 

```sql
SELECT *
FROM TABLE_A
FULL JOIN TABLE_B
ON TABLE_A.COLUMN1 = TABLE_B.COLUMN 2
```

# 5. CASE WHEN

* 조건에 따른 값을 다르게 출력하고 싶을 때

```sql
SELECT CASE WHEN CONDITION 1 THEN RESULT 1
WHEN CONDITION 2 THEN RESULT 2
ELSE RESULT 3 END
FROM DB.TABLE;
```

```sql
SELECT COUNTRY CASE WHEN COUNTRY IN ('USA','CANADA') THEN 'NORTH AMERICA'
ELSE 'OTHERS' END AS region
FROM DB.CUSTOMERS
```

# 6. SUBQUERY

* 쿼리 안의 쿼리

```sql
SELECT ORDERNUMBER
FROM DB.ORDERS
WHERE CUSTOMERNUMBER IN (SELECT CUSTOMERNUMBER FROM DB.CUSTOMERS WHERE CITY = 'NYC');
```

```sql
SELECT CUSTOMERNUMBER
FROM (SELECT CUSTOMERNUMBER FROM DB.CUSTOMER WHERE CITY = 'NYC')A;
```

```sql
SELECT ORDERNUMBER
FROM DB.ORDERS
WHERE CUSTOMER IN (SELECT CUSTOMERNUMBER FROM DB.CUSTOMERS
                  WHERE COUNTRY = 'USA')
```

