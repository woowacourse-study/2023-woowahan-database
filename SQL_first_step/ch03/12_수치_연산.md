# 목차

1. [사칙 연산](#1-사칙-연산) <br/>
2. [SELECT 구로 연산하기](#2-SELECT-구로-연산하기) <br/>
3. [열의 별명](#3-열의-별명) <br/>
4. [WHERE 구에서 연산하기](#4-WHERE-구에서-연산하기) <br/>
5. [NULL값의 연산](#5-NULL값의-연산) <br/>
6. [ORDER BY 구에서 연산하기](#6-ORDER-BY-구에서-연산하기) <br/>
7. [함수](#7-함수) <br/>
8. [ROUND 함수](#8-ROUND-함수) <br/>

<br/>

# 12강 - 수치 연산

## 1) 사칙 연산

SQL문법에서도 연산자를 사용해 여러 가지 연산을 할 수 있다!

- 연산자의 우선순위
  - 일반 사칙연산과 같이 * / % 이 + - 보다 우선시 된다.

## 2) SELECT 구로 연산하기

- SELECT 구에 연산식을 기술할 수 있다.
  - 이는 **명령이 실행될 때 연산을 할 수 있다**는 것을 의미한다.
    Table sample_12


    | no | price | quantity |
    | ---- | ------- | ---------- |
    | 1  | 100   | 10       |
    | 2  | 230   | 24       |
    | 3  | 1980  | 1        |


    ```
        SELECT price * quantity
        FROM  sample_12
    ```


    | price * quantity |
    | ------------------ |
    | 1000             |
    | 5520             |
    | 1980             |

## 3) 열의 별명

- price * quantity 와 같이 열 이름이 길고 알아보기 힘든 경우 별명을 지정할 수 있다.
- 열 이름 뒤에 **AS**를 붙이면 해당 열의 별명이 지정된다. (AS를 생략해도 똑같이 지정된다.)

  ```
    SELECT price * quantity AS amount
  ```


  | amount |
  | -------- |
  | 1000   |
  | 5520   |
  | 1980   |
- **별명 이름에 ASCII 문자 이외의 것을 포함할 경우는 더블쿼트("")로 둘러싸서 지정한다!**

  - ex) SELECT price * quantity AS "별명"

## 4) WHERE 구에서 연산하기

연산식은 SELECT문 이외에도 WHERE 구에서 적용할 수 있다.!


| no | price | quantity | amount |
| ---- | ------- | ---------- | -------- |
| 1  | 100   | 10       | 1000   |
| 2  | 230   | 24       | 5520   |
| 3  | 1980  | 1        | 1980   |

- WHERE 구에서의 연산식 적용

  ```
      SELECT *, price * quantity AS amount
      FROM sample_12
      WHERE price * quantity >= 2000
  ```
- 결과값


  | no | price | quantity | amount |
  | ---- | ------- | ---------- | -------- |
  | 2  | 230   | 24       | 5520   |
- WHERE 구와 SELECT 구의 내부 처리 순서

  - DB내에서 쿼리믄의 처리 순서는 **WHERE -> SELECT 순**으로 이루어진다.
  - 하지만 별명은 SELECT문의 내부 처리 단계에서 지정되기 떄문에 **SELECT 구에서 지정한 별명은 WHERE 구 안에서 사용할 수 없다!**

## 5) NULL값의 연산

데이터베이스에서의 NULL값 연산은 타 프로그래밍 언어와 다르다.

- NULL +1
- 1 + NULL
- 2 * NULL
- 1 / NULL

위의 연산 모두 결과는 NULL로 처리된다. 따라서 **NULL로 연산하면 결과는 무조건 NULL이 된다!**

## 6) ORDER BY 구에서 연산하기

ORDER BY 구에서도 연산할 수 있고 그 결괏값들을 정렬할 수 있다.


| no | price | quantity | amount |
| ---- | ------- | ---------- | -------- |
| 1  | 100   | 10       | 1000   |
| 2  | 230   | 24       | 5520   |
| 3  | 1980  | 1        | 1980   |

- ORDER BY에 연산식을 적용한 쿼리

  ```
      SELECT *, price * quantity AS amount
      FROM sample_12
      ORDER BY price * quantity DESC
  ```
- 결과


  | no | price | quantity | amount |
  | ---- | ------- | ---------- | -------- |
  | 2  | 230   | 24       | 5520   |
  | 3  | 1980  | 1        | 1980   |
  | 1  | 100   | 10       | 1000   |
- **ORDER BY 구문에서는 SELECT문에서 지정한 별명을 사용할 수 있다.**

  - 처리 순서가 SELECT 구문 이후에 적용되기 때문에 사용 가능하다.

## 7) 함수

연산자 이외에 지정된 함수를 이용해 연산할 수도 있다.

- 10 % 3 대신 MOD(10, 3)을 이용해도 결과는 같다.

## 8) ROUND 함수

반올림 하는데 사용하는 함수

```
SELECT amount, ROUND(amount) FROM sample_12;
```


| amount  | round(amount) |
| --------- | --------------- |
| 5961.60 | 5962          |
| 2138.40 | 2138          |
| 1080.00 | 1080          |

- ROUND의 두 번째 인자에 반올림 자릿수를 지정할 수 있다.
  소수점 둘째 자리에서 반올림
  ```
  SELECT amount, ROUND(amount, 1) FROM sample_12;
  ```
  결과
  | amount  | round(amount) |
  | --------- | --------------- |
  | 5961.60 | 5961.6        |
  | 2138.40 | 2138.4        |
  | 1080.00 | 1080.0        |

    - 음수를 이용해 소수점 아래 단위가 아닌 10의자리 단위의 반올림도 가능하다.

- 이 외에도 SIN, COS 등의 삼각함수나 루트를 계산하는 SQRT 등 다양한 함수가 존재한다.
