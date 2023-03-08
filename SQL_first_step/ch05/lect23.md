# 목차

1. [DELETE의 WHERE 구에서 서브쿼리 사용하기](#1-DELETE의-WHERE-구에-서브쿼리-사용하기)
2. [스칼라 값](#2-스칼라-값)
3. [SELECT 구에서 서브쿼리 사용하기](#3-SELECT-구에서-서브쿼리-사용하기)
4. [SET 구에서 서브쿼리 사용하기](#4-SET-구에서-서브쿼리-사용하기)
5. [FROM 구에서 서브쿼리 사용하기](#5-FROM-구에서-서브쿼리-사용하기)
6. [INSERT 명령과 서브쿼리](#6-INSERT-명령과-서브쿼리)

## 1) DELETE의 WHERE 구에서 서브쿼리 사용하기
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  WHERE 열명 = (SELECT 조건문을 적용한 집합)
  ```
- 특정 조건에 해당하는 열을 걸러내고 싶을 때 사용할 수 있다.
- SELECT를 실행하기 전 괄호로 둘러싼 서브쿼리를 먼저 실행한 후 SELECT를 실행한다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- 최솟값을 가지는 행 삭제하기

코드
```SQL
DELTE FROM sample54
WHERE a = (SELECT MIN(a) FROM sample54);
```

결과

| name | a   |
|------|-----|
| A    | 100 |
| B    | 900 |
| C    | 80  |

- WHERE 절의 서브쿼리에서 반환되는 값은 20이다.
- a = 20을 만족하는 행을 지운 테이블을 반환한다.


## 2) 스칼라 값

- SELECT 명령이 하나의 값만 반환하는 것을 '스칼라 값을 반환한다'고 한다.
- 스칼라 값을 반환하는 서브쿼리는 서브쿼리로 사용하기 쉽다. (서브쿼리 = 연산자로 쉽게 비교할 수 있기 때문)
- 서브쿼리가 반환하는 값에는 일반적으로 네 가지 패턴이 있다.

패턴 1) 하나의 값을 반환하는 패턴
- 코드
    ```SQL
    SELECT MIN(a)
    FROM sample54;
    ```
  
- 결과

    | MIN(a) |
    |--------|
    | 80     |


패턴 2)  복수의 행이 반환되지만 열은 하나인 패턴

- 코드
    ```SQL
    SELECT no
    FROM sample54;
    ```

- 결과

    | no |
    |----|
    | 1  |
    | 2  |
    | 3  |

패턴 3) 하나의 행이 반환되지만 열이 복수인 패턴

- 코드
    ```SQL
    SELECT MIN(a), MAX(no)
    FROM sample54;
    ```

- 결과

  | MIN(no) | MAX(no) |
  |---------|---------|
  | 80      | 4       |

패턴 4) 복수의 행, 복수의 열이 반환되는 패턴

- 코드
    ```SQL
    SELECT no, a
    FROM sample54;
    ```

- 결과

    | no  | a   | 
    |-----|-----|
    | 1   | 100 |
    | 2   | 900 |
    | 4   | 80  |


## 3) SELECT 구에서 서브쿼리 사용하기
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  GROUP BY 열명
  ```
- SELECT 구에서 서브쿼리를 사용하기 위해서는 스칼라 서브쿼리를 사용해야 한다.


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

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- SELECT 구에서 서브쿼리 사용하기

코드
```SQL
  SELECT
    (SELECT COUNT(*) FROM sample51) AS sq1,
    (SELECT COUNT(*) FROM sample54) AS sq2,
    
```

결과

| sq1 | sq2 |
|-----|-----|
| 5   | 3   |


## 4) SET 구에서 서브쿼리 사용하기
- SYNTAX
```SQL
  UPDATE 테이블명
  SET 열명 = (서브쿼리)
```
- UPDATE나 SET 구에서도 서브쿼리를 사용할 수 있다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

코드
```SQL
  UPDATE sample54
  SET a = (SELECT MAX(a) FROM sample54);
```

결과

| name | a   |
|------|-----|
| A    | 900 |
| B    | 900 |
| C    | 900 |

## 5) FROM 구에서 서브쿼리 사용하기
- SYNTAX
```SQL
  UPDATE 테이블명
  SET 열명 = (서브쿼리)
```
- FROM 구에서도 서브쿼리를 사용할 수 있다.
- FROM 구에서 사용하는 서브쿼리는 반드시 스칼라 값을 반환하지 않아도 된다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

코드
```SQL
  SELECT *
  FROM (SELECT * FROM sample54) sq;
```

결과

| no  | a   |
|-----|-----|
| 1   | 100 |
| 2   | 900 |
| 4   | 900 |# 목차

1. [DELETE의 WHERE 구에서 서브쿼리 사용하기]
2. [스칼라 값]
3. [SELECT 구에서 서브쿼리 사용하기]
4. [SET 구에서 서브쿼리 사용하기]
5. [FROM 구에서 서브쿼리 사용하기]
6. [INSERT 명령과 서브쿼리]

## 1) DELETE의 WHERE 구에서 서브쿼리 사용하기
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  WHERE 열명 = (SELECT 조건문을 적용한 집합)
  ```
- 특정 조건에 해당하는 열을 걸러내고 싶을 때 사용할 수 있다.
- SELECT를 실행하기 전 괄호로 둘러싼 서브쿼리를 먼저 실행한 후 SELECT를 실행한다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- 최솟값을 가지는 행 삭제하기

코드
```SQL
DELTE FROM sample54
WHERE a = (SELECT MIN(a) FROM sample54);
```

결과

| name | a   |
|------|-----|
| A    | 100 |
| B    | 900 |
| C    | 80  |

- WHERE 절의 서브쿼리에서 반환되는 값은 20이다.
- a = 20을 만족하는 행을 지운 테이블을 반환한다.


## 2) 스칼라 값

- SELECT 명령이 하나의 값만 반환하는 것을 '스칼라 값을 반환한다'고 한다.
- 스칼라 값을 반환하는 서브쿼리는 서브쿼리로 사용하기 쉽다. (서브쿼리 = 연산자로 쉽게 비교할 수 있기 때문)
- 서브쿼리가 반환하는 값에는 일반적으로 네 가지 패턴이 있다.

패턴 1) 하나의 값을 반환하는 패턴
- 코드
    ```SQL
    SELECT MIN(a)
    FROM sample54;
    ```

- 결과

  | MIN(a) |
      |--------|
  | 80     |


패턴 2)  복수의 행이 반환되지만 열은 하나인 패턴

- 코드
    ```SQL
    SELECT no
    FROM sample54;
    ```

- 결과

  | no |
      |----|
  | 1  |
  | 2  |
  | 3  |

패턴 3) 하나의 행이 반환되지만 열이 복수인 패턴

- 코드
    ```SQL
    SELECT MIN(a), MAX(no)
    FROM sample54;
    ```

- 결과

  | MIN(no) | MAX(no) |
    |---------|---------|
  | 80      | 4       |

패턴 4) 복수의 행, 복수의 열이 반환되는 패턴

- 코드
    ```SQL
    SELECT no, a
    FROM sample54;
    ```

- 결과

  | no  | a   | 
      |-----|-----|
  | 1   | 100 |
  | 2   | 900 |
  | 4   | 80  |


## 3) SELECT 구에서 서브쿼리 사용하기
- SYNTAX
  ```SQL
  SELECT 열명
  FROM 테이블명
  GROUP BY 열명
  ```
- SELECT 구에서 서브쿼리를 사용하기 위해서는 스칼라 서브쿼리를 사용해야 한다.


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

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- SELECT 구에서 서브쿼리 사용하기

코드
```SQL
  SELECT
    (SELECT COUNT(*) FROM sample51) AS sq1,
    (SELECT COUNT(*) FROM sample54) AS sq2,
    
```

결과

| sq1 | sq2 |
|-----|-----|
| 5   | 3   |


## 4) SET 구에서 서브쿼리 사용하기
- SYNTAX
```SQL
  UPDATE 테이블명
  SET 열명 = (서브쿼리)
```
- UPDATE나 SET 구에서도 서브쿼리를 사용할 수 있다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

코드
```SQL
  UPDATE sample54
  SET a = (SELECT MAX(a) FROM sample54);
```

결과

| name | a   |
|------|-----|
| A    | 900 |
| B    | 900 |
| C    | 900 |

## 5) FROM 구에서 서브쿼리 사용하기
- SYNTAX
```SQL
  UPDATE 테이블명
  SET 열명 = (서브쿼리)
```
- FROM 구에서도 서브쿼리를 사용할 수 있다.
- FROM 구에서 사용하는 서브쿼리는 반드시 스칼라 값을 반환하지 않아도 된다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

코드
```SQL
  SELECT *
  FROM (SELECT * FROM sample54) sq;
```

결과

| no  | a   |
|-----|-----|
| 1   | 100 |
| 2   | 900 |
| 4   | 80  |

- SELECT 명령 안에 SELECT가 들어있는 것처럼 보이는 구조를 '네스티드(nested) 구조'라고 한다.
- 서브쿼리의 결과에도 별명을 붙일 수 있다.

예시 2)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- ROWNUM으로 행 개수를 제한할 수 있지만 정렬 후 상위 몇 건을 추출하는 것은 불가능하다.
- 이런 경우 FROM구에서 서브쿼리를 사용한다.

코드
```SQL
  SELECT *
  FROM (SELECT * FROM sample54 ORDER BY a DESC) sq)
  WHERE ROWNUM <= 2;
```

결과

| no  | a   |
|-----|-----|
| 2   | 900 |
| 1   | 100 |

## 6) INSERT 명령과 서브쿼리
- SYNTAX
```SQL
  INSERT INTO 테이블명 VALUES (
    (SELECT 집계함수(열명) FROM sample51),
    (SELECT 집계함수(열명) FROM sample54)
  );
```
- INSERT 명령에서 VALUES 구의 일부로 서브쿼리를 사용할 수 있다.
- INSERT 명령에서 VALUES 구 대신 SELECT 명령을 사용할 수 있다.
- 이때 서브쿼리는 스칼라 서브쿼리로 지정해야 한다.
- 서브쿼리의 반환 자료형은 INSERT 하는 열의 자료형과 일치해야 한다.

예시 1)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- VALUES 구에서 서브쿼리 사용하기

코드
```SQL
  INSERT INTO sample54 VALUES (
    (SELECT COUNT(*) FROM sample51),
    (SELECT COUNT(*) FROM sample54)
  );
  SELECT * FROM sample54;
```

결과

| a   | b   |
|-----|-----|
| 5   | 3   |

예시 2)

테이블 sample54

| no  | a    |
|-----|------|
| 1   | 100  |
| 2   | 900  |
| 3   | 20   |
| 4   | 80   |

- SELECT 결과를 INSERT 하기

코드
```SQL
  INSERT INTO sample54 SELECT 1, 2;
  SELECT * FROM sample54;
```

결과

| a   | b   |
|-----|-----|
| 5   | 3   |
| 1   | 2   |

예시 3)

- 테이블 복사하기

코드
```SQL
  INSERT INTO sample54 SELECT * FROM sample 51;
```

