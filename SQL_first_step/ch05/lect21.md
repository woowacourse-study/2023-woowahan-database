# 목차

1. [SUM으로 합계 구하기](#1-sum으로-합계-구하기)
2. [AVG로 평균내기](#2-avg로-평균내기)
3. [MIN/MAX로 최솟값/최댓값 구하기](#3-minmax로-최솟값최댓값-구하기)

# 5강 - 집계와 서브쿼리

## 1) SUM으로 합계 구하기
- SYNTAX
  ```SQL
    SUM(집합)
  ```

- 주어진 집합의 합계를 구해 반환한다.
- 합계를 구할 수 있는 집합은 수치형 뿐이다. (문자열형, 날짜시간형 불가)

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
  SELECT SUM(quantity) FROM sample51;
```

결과

| COUNT(*) |
|----------|
| 16       |

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


<br/>

## 2) AVG로 평균내기
- SYNTAX
  ```SQL
    AVG(집합)
  ```

- 주어진 집합의 평균을 구해 반환한다.
- SUM(열 명) / COUNT(열 명)으로 대체할 수 있다.

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
  SELECT AVG(quantity) FROM sample51;
```

결과

| COUNT(*) |
|----------|
| 4.0000   |

<br/>

## 3) MIN/MAX로 최솟값/최댓값 구하기
- SYNTAX
  ```SQL
    MIN(집합)
    MAX(집합)
  ```

- 주어진 집합의 최솟값/최댓값을 구해 반환한다.
- **문자열형과 날짜시간형에도 사용 가능하다.**


| no  | name | quantity |
|-----|------|----------|
| 1   | A    | 1        |
| 2   | A    | 2        |
| 3   | B    | 10       |
| 4   | C    | 3        |
| 5   | NULL | NULL     |


코드 (수치형)
```SQL
  SELECT MIN(quantity), MAX(quantity) FROM sample51;
```

결과

| MIN(quantity) | MAX(*quantity) |
|---------------|----------------|
| 1             | 10             |

---
코드 (문자열형)
```SQL
  SELECT MIN(name), MAX(name) FROM sample51;
```

결과

| MIN(name) | MAX(*name) |
|-----------|------------|
| A         | C          |

<br/>
