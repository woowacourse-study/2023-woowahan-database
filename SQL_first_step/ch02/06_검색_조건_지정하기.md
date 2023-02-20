# 목차

1. [SELECT 구에서 열 지정하기](#1-select-구에서-열-지정하기) <br/>
2. [WHERE 구에서 행 지정하기](#2-where-구에서-행-지정하기) <br/>
3. [NULL값 검색](#3-null값-검색) <br/>
4. [비교 연산자](#4-비교-연산자) <br/>

<br/>

# 6강 - 검색 조건 지정하기

많은 행과 열이 저장된 테이블에선 본인이 원하는 특정 데이터만을 참조하고 싶을 때가 존재한다. 그럴 때 사용하는 방법을 알아봅시다.

## 1) SELECT 구에서 열 지정하기

- **SELECT 열1, 열2 ... FROM 테이블명**

위의 명령처럼 콤마를 통해 열을 구분지어서 지정할 수 있습니다.

<br/>

ex) 명령 : **SELECT no, name FROM sample**

| no   | name   |
| ---- | ------ |
| 1    | 홍길동 |
| 2    | 철수   |

열을 지정할 땐 중복된 열을 쓰든 순서를 거꾸로 쓰든 아무런 상관 없습니다.

ex) SELECT no, no, no FROM sample

ex) SELECT name, no FROM sample

<br/>

## 2) WHERE 구에서 행 지정하기

테이블의 수많은 행과 열 안에서, 필요한 데이터만 검색하기 위해 필요한 WHERE 구에 대해 알아봅시다.

- **SELECT** 열 **FROM** 테이블명 **WHERE** 조건식

  - 참고로 예약어 구의 순서는 정해져 있기 때문에 바꿀 수 없습니다.

  - **SELECT 구 -> WHERE 구 -> FROM 구**

  - WHERE 구처럼 생략 가능한 구도 있습니다.

    <br/>

**조건식이란?**

**열과 연산자, 상수로 구성되는 식**입니다. WHERE구의 간단한 예를 들어봅시다.

- **SELECT no, name FROM sample WHERE no = 2;**
- **SELECT no, name FROM sample WHERE name = '철수';**
- **SELECT no, name FROM sample WHERE birthday= '1995-08-24';**
  - **문자열형**을 통해 조건식을 작성할 경우 싱글쿼트(' ')로 둘러싸 표기해야 합니다.
  - **날짜시간형** 상수 또한 싱글쿼트로 둘러싸 표기해야 합니다.

| no   | name |
| ---- | ---- |
| 2    | 철수 |

즉, 위의 명령을 해석해보자면, **'no 컬럼의 값이 2인 행의 데이터 중 no, name 컬럼의 데이터만 보여줘'** 입니다.

<br/>

## 3) NULL값 검색

NULL 을 검색할 땐, 일반 연산자로 검색할 수 없습니다. 딱 2가지 형태로 검색이 가능합니다.

- SELECT * FROM sample WHERE **birthday IS NULL**
  - birthday 가 NULL 인 행을 가져오기
- SELECT * FROM sample WHERE **birthday IS NOT NULL**
  - birthday 가 NULL 이 아닌 행을 가져오기

NULL 검색은 **'IS NULL', 'IS NOT NULL'** 을 사용합니다.

<br/>

## 4) 비교 연산자

1. **= 연산자**
   - 좌변과 우변의 값이 같을 경우 참
2. **!=, <> 연산자**
   - 좌변과 우변의 값이 같지 않을 경우 참
3. **\> 연산자**
   - 좌변 값이 우변 값보다 클 경우 참
4. **>= 연산자**
   - 좌변 값이 우변의 값보다 크거나 같을 경우 참
5. **< 연산자**
   - 좌변 값이 우변 값보다 작은 경우 참
6. **<= 연산자**
   - 좌변 값이 우변 값보다 작거나 같을 경우 참