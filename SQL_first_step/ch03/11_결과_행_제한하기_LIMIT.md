# 목차

1. [행수 제한](#1-행수-제한) <br/>
2. [오프셋 지정](#2-오프셋-지정) <br/>

<br/>

# 11강 - 결과 행 제한하기 - LIMIT

## 1) 행수

- SYNTAX

  ```
    SELECT 열명 FROM 테이블명 WHERE 조건식
    LIMIT 행수
  ```

  - 최대 행수를 수치로 지정해 클라이언트로 반환
  - ex) LIMIT 5 이면 쿼리 결과의 상위 5행만 출력한다.
  - <span style="color:gray"> 보통 쿼리의 가장 끝에 위치한다고 보면 된다.</span>
  - *MySQL과 PostgreSQL에서만 사용할 수 있는 문법이다!*

## 2) 오프셋 지정

- SYNTAX
  ```
    SELECT 열명 FROM 테이블명 WHERE 조건식
    LIMIT 행수 OFFSET 위치
  ```
  - LIMIT 뒤에 종속적인 문법 (OFFSET만 쓸 수 없다!)
  - 각 행들을 배열의 인덱스로 생각하고, 해당 위치부터 출력한다.
  - ex) LIMIT 3 OFFSET 3 -> 위에서부터 4, 5, 6 번째 값 출력
