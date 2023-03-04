# 목차

1. [COUNT로 행 개수 구하기](#1-count로-행-개수-구하기) <br/>
2. [집계함수와 NULL값 구하기](#2-집계함수와-null값-구하기) <br/>
3. [DISTINCT로 중복 제거](#3-distinct로-중복-제거)
4. [집계함수에서 DISTINCT](#4-집계함수에서-distinct)

# 5강 - 집계와 서브쿼리

## 1) COUNT로 행 개수 구하기
- SYNTAX
  ```SQL
    COUNT(집합)
  ```

- 주어진 집합의 '개수'를 구해 반환한다.

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
  SELECT COUNT(*) FROM sample51;
```

결과
  
| COUNT(*)  |
|-----------|
| 5         |

- sample51 테이블 행의 개수를 반환한다.

**예시 2)**

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |

코드
```SQL
  SELECT COUNT(*) FROM sample51 WHERE name = 'A';
```

결과

| COUNT(*) |
|----------|
| 2        |

- sample51 테이블 중 이름이 'A'인 행의 개수를 반환한다.
- SELECT 구에 COUNT를 사용할 경우 결과값으로 하나의 행을 반환한다.

<br/>

## 2) 집계함수와 NULL값 구하기

- COUNT 함수에서 NULL값은 무시된다.

**예시)**

[sample51 테이블]

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |

코드
```SQL
  SELECT COUNT(no), COUNT(name) FROM sample51;
```

결과

| COUNT(no) | COUNT(name) |
|-----------|-------------|
| 5         | 4           |

- no 열은 NULL값이 존재하지 않아 5가 반환된다.
- name 열은 NULL값이 무시되어 4가 반환된다.

<br/>


## 3) DISTINCT로 중복 제거

- 중복을 제거하기 위해 DISTINCT를 사용한다.
- 중복을 제거하지 않으려면 ALL을 사용한다. (ALL은 기본값)

**예시)**

[sample51 테이블]

| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |

코드
```SQL
  SELECT DISTINCT name FROM sample51;
```

결과

| name |
|------|
| A    |
| B    |
| C    |
| NULL |

- name에서 중복되는 A는 제거되어 반환된다.

<br/>

## 4) 집계함수에서 DISTINCT

- SELECT 구나 WHERE 구에서는 중복을 제거하는 함수가 없다.
- DISTINCT로 집합에서 중복을 제거한 뒤 COUNT로 개수를 구할 수 있다.

**예시)**

코드
```SQL
  SELECT COUNT(ALL name), COUNT(DISTINCT name) FROM sample51;
```

결과

| COUNT(no) | COUNT(name) |
|-----------|-------------|
| 4         | 3           |


<br/>

