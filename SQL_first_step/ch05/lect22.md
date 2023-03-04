# 목차

1. [GROUP BY로 그룹화](#1-GROUP-BY로-그룹화)
2. [HAVING 구로 조건 지정](#2-HAVING-구로-조건-지정)
3. [복수열의 그룹화](#3-복수열의-그룹화)
4. [결괏값 정렬](#4-결괏값-정렬~)

## 1) GROUP BY로 그룹화
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  GROUP BY 열명
  ```
- 지정된 열에서 같은 값을 가진 행들을 하나의 그룹으로 그룹화 한다.
- 복수로 지정할 수 있다.

예시 1)

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |

코드
```SQL
  SELECT name
  FROM sample51
  GROUP BY name;
```

결과

| name |
|------|
| A    |
| B    |
| C    |
| NULL |

- DISTINCT와 같은 결과가 나온다.
- SELECT 구에서 name 열을 지정했기 때문에 그룹화된 name 열의 데이터가 반환된다.

예시 2)

- GROUP BY 구와 집계함수를 조합한다.

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |

코드
```SQL
  SELECT name, COUNT(name), SUM(quantity)
  FROM sample51
  GROUP BY name;
```

결과

| name | COUNT(name) | SUM(quantity) |
|------|-------------|---------------|
| NULL | 1           | NULL          |
| A    | 0           | 3             |
| B    | 2           | 10            |
| C    | 1           | 3             |

- name 열에는 GROUP BY name에 의해 나뉜 NULL, A, B, C가 있다.
- COUNT(name) 열에는 각 그룹의 행의 개수가 반환된다.
- SUM(quantity) 열에는 각 그룹의 quantity의 합이 반환된다.

## 2) HAVING 구로 조건 지정
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  GROUP BY 열명
  HAVING 조건문
  ```
  
- WHERE 구에는 집계함수를 사용할 수 없기 때문에 HAVING 구로 검색 조건을 지정한다.
- HAVING 구는 GROUP BY 구의 뒤에 작성한다.
- 조건식이 참인 그룹만 반환된다
- SELECT 구보다 먼저 실행되므로 HAVING 구에서는 SELECT 구에서 지정한 별명을 사용할 수 없다.
- 검색 순서는 다음과 같다.
1. WHERE 구로 검색 -> 2. 검색한 뒤 그룹화 -> 3. HAVING 구로 검색 -> SELECT 구 실행

예시 1)

테이블
```SQL
  SELECT name, COUNT(name)
  FROM sample51
  GROUP BY name;
```
| name | COUNT(name) |
|------|-------------|
| NULL | NULL        |
| A    | 2           |
| B    | 1           |
| C    | 1           |


- HAVING 구로 걸러내기

코드
```SQL
  SELECT name, COUNT(name)
  FROM sample51
  GROUP BY name
  HAVING COUNT(name) = 1;
```

결과

| name | COUNT(name) |
|------|-------------|
| B    | 1           |
| C    | 1           |

실행 순서
1. name 으로 그룹화
2. COUNT(name) = 1 조건을 만족하는 행 반환

## 3) 복수열의 그룹화

- GROUP BY에서 지정한 열 이외의 열은 집계함수를 사용하지 않는 채 SELECT 구에서 사용할 수 없다.

  잘못된 예시)
  ```SQL
    SELECT no, name, quantity
    FROM sample51
    GROUP BY name;
  ```
  올바른 예시 1)
  - 집계함수를 사용하면 집합은 하나의 값으로 계산되므로 문제가 발생하지 않는다.
    ```SQL
      SELECT MIN(no), name, SUM(quantity)
      FROM sample51
      GROUP BY name;
    ```

  올바른 예시 2)
  - GROUP BY에 지정한 열이라면 SELECT 구에서 사용할 수 있다. 
    ```SQL
      SELECT MIN(no), name, SUM(quantity)
      FROM  sample51
      GROUP BY name;
    ```

## 4) 결괏값 정렬

- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  GROUP BY 열명
  ORDER BY 조건문
  ```

- GROUP BY는 데이터를 정렬해주지 않는다.
- ORDER BY를 사용하여 조건에 맞게 정렬할 수 있다.
- ASC(오름차순)이 기본값이며, DESC(내림차순)을 지정할 수 있다.

예시 1)

테이블

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |

- 집계한 결과 정렬하기

코드
```SQL
  SELECT name, COUNT(name), SUM(quantity)
  FROM sample51
  GROUP BY name
  ORDER BY SUM(quantity) DESC;
```

결과

| name | COUNT(name) | SUM(quantity) |
|------|-------------|---------------|
| B    | 1           | 10            |
| C    | 1           | 3             |
| A    | 2           | 3             |
| NULL | 0           | NULL          |

- quantity를 오름차순으로 정렬한 결과를 반환한다.