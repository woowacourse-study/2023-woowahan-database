# 목차

1. [EXISTS](#1-EXISTS)
2. [NOT EXISTS](#2-NOT-EXISTS)
3. [상관 서브쿼리](#3-상관-서브쿼리)
4. [IN](#4-IN)

## 1) EXISTS
- SYNTAX
  ```SQL
  EXISTS (SELECT 명령)
  ```
- 데이터가 존재하는지 아닌지 판별하기 위한 조건을 지정할 때 EXISTS 술어를 사용할 수 있다.
- EXISTS 술어에 서브쿼리를 지정하면 서브쿼리가 행을 반환할 경우 참을 돌려준다.

예시 1)

테이블 sample551

| no  | a    |
|-----|------|
| 1   | NULL |
| 2   | NULL |
| 3   | NULL |
| 4   | NULL |
| 5   | NULL |

테이블 sample552

| no 2 |
|------|
| 3    |
| 5    |

- EXISTS를 사용해 '있음'으로 갱신하기

코드
```SQL
  UPDATE sample551 SET a = '있음'
  WHERE EXISTS (SELECT * FROM sample 552 WHERE no2 = no);
  
  SELECT * FROM sample551;
```

결과

| no  | a    |
|-----|------|
| 1   | NULL |
| 2   | NULL |
| 3   | 있음   |
| 4   | NULL |
| 5   | 있음   |


## 2) NOT EXISTS
- SYNTAX
  ```SQL
  NOT EXISTS (SELECT 명령)
  ```
- NOT EXISTS 술어에 서브쿼리를 지정하면 행이 존재하지 않는 경우 서브쿼리가 행을 반환할 때 참을 돌려준다.

예시 1)

테이블 sample551

| no  | a    |
|-----|------|
| 1   | NULL |
| 2   | NULL |
| 3   | NULL |
| 4   | NULL |
| 5   | NULL |

테이블 sample552

| no 2 |
|------|
| 3    |
| 5    |

- NOT EXISTS를 사용해 '없음'으로 갱신하기

코드
```SQL
  UPDATE sample551 SET a = '없음'
  WHERE NOT EXISTS (SELECT * FROM sample 552 WHERE no2 = no);
  
  SELECT * FROM sample551;
```

결과

| no  | a   |
|-----|-----|
| 1   | 없음  |
| 2   | 없음  |
| 3   | 있음  |
| 4   | 없음  |
| 5   | 있음  |

## 3) 상관 서브쿼리

#### 상관 서브쿼리란?

다음 쿼리를 살펴보자.

```SQL
  UPDATE sample551 SET a = '있음'
  WHERE EXISTS (SELECT * FROM sample552 WHERE no2 = no);
```
- UPDATE 명령은 부모가 되고, WHERE 구에 괄호로 묶은 서브쿼리는 자식이 된다.
- 자식인 서브쿼리에서는 sample552 테이블의 no2값이 부모쿼리의 테이블인 sample551의 no 열과 일치하는지 검색한다.
- 이처럼 부모 명령과 자식인 서브쿼리가 특정 관계를 가지는 것을 '상관 서브쿼리'라고 한다.
- 이때 상관 서브쿼리의 자식 서브쿼리는 부모 명령과 독립적이지 않으므로, 부모 명령 없이 독립적으로 실행될 수 없다.

#### 상관 서브쿼리에 해당하지 않는 경우

다음과 같이 서브쿼리가 부모 명령과 독립적으로 실행될 수 있는 경우는 '상관 서브쿼리'라고 할 수 없다.
    ```SQL
      DELETE 
      FROM sample54 WHERE a = (SELECT MIN(a) FROM sample54);
    ```
<br/>
<br/>
<br/>
#### 테이블명 붙이기

- 부모 명령과 자식 서브쿼리에서 사용하는 열의 명이 같다면 'WHERE no = no'와 같이 어느 테이블의 no 열인지 구분하기 어렵다.
- 이때 테이블명을 붙여 테이블을 구분해줄 수 있다.

예시)
```SQL
  UPDATE sample551 SET a = '있음'
  WHERE EXISTS (SELECT * FROM sample552 WHERE sample552.no = sample551.no);
```

- 이와 같이 테이블명을 명시할 경우 문제 없이 실행할 수 있다.


## 6) IN
- SYNTAX
  ```SQL
  열명 IN (집합)
  ```
- 스칼라 값을 비교할 때는 '=' 연산자를 사용하지만 집합을 비교할 때는 IN을 사용한다.
- IN의 왼쪽에 지정된 열이 오른쪽에 지정된 집합 안에 존재하면 참을 반환한다.

예시 1)

테이블 sample551

| no  | a    |
|-----|------|
| 1   | NULL |
| 2   | NULL |
| 3   | NULL |
| 4   | NULL |
| 5   | NULL |

테이블 sample552

| no 2 |
|------|
| 3    |
| 5    |

- IN을 사용해 조건식 기술

코드
```SQL
  SELECT *
  FROM sample551
  WHERE no IN (3, 5);
```

결과

| no  | a   |
|-----|-----|
| 3   | 있음  |
| 5   | 있음  |


예시 2)

테이블 sample551

| no  | a    |
|-----|------|
| 1   | NULL |
| 2   | NULL |
| 3   | NULL |
| 4   | NULL |
| 5   | NULL |

테이블 sample552

| no 2 |
|------|
| 3    |
| 5    |

- IN의 오른쪽을 서브쿼리로 지정하기

코드
```SQL
  SELECT *
  FROM sample551
  WHERE no IN (SELECT no2 FROM sample552);
```

결과

| no  | a   |
|-----|-----|
| 3   | 있음  |
| 5   | 있음  |
