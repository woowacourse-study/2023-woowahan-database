# 목차

1. [SELECT * FROM 테이블명;](#1-select--from-테이블명) <br/>
2. [예약어와 데이터베이스 객체명](#2-예약어와-데이터베이스-객체명) <br/>
3. [SELECT 명령의 실행 결과 = 표](#3-select-명령의-실행-결과--표) <br/>
4. [값이 없는 데이터 = NULL](#4-값이-없는-데이터--null) <br/>

<br/>

# 4강 - SELECT

## 1) SELECT * FROM 테이블명;

- **SELECT** : 명령의 종류 **(예약어)**
- **\* (애스터리스크)** : **'모든 열'** 을 의미하는 메타문자 **(예약어)**
  - 찾고싶은 컬럼이 따로 있다면, 애스터리스크 대신 해당 컬럼들만 적어주면 된다.
- **FROM** : 처리 대상 테이블을 지정하는 키워드 **(예약어)**

즉, **해당 테이블의 모든 컬럼을 찾는다는 명령**이다.

<br/>

## 2) 예약어와 데이터베이스 객체명

- **데이터베이스 객체** : 테이블과 뷰 등등 다양한 데이터를 저장하거나 관리하는 '어떤 것'.

SQL문에는 예약어가 존재하는데, **SELECT**와 **FROM**이 그 예이다. <br/>

**예약어와 데이터 베이스 객체 명의 규칙** 

1. 데이터베이스 객체명은 **'이미 존재하는 객체의 이름과 같은 이름'** 혹은 **'예약어'** 로 생성할 수 없습니다.
2. 예약어와 데이터 베이스 객체명은 대소문자를 구별하지 않습니다.
   - 사용 가능한 형태들
     - select * from sample
     - Select * From Sample
     - SELECT * FROM SAMPLE

<br/>

## 3) SELECT 명령의 실행 결과 = 표

SELECT 명령을 실행하면 표 형식의 데이터가 출력 되는데, **표(레코드)**와 **역(컬럼/필드)**로 구성됩니다.

ex) SELECT로 검색할 땐, 항상 행과 열로 구성된 표 형식으로 나온다는 것을 인지하자.

| no   | name   | birthday   | address |
| ---- | ------ | ---------- | ------- |
| 1    | 홍길동 | NULL       | 서울시  |
| 2    | 철수   | 1995-08-24 | 인천시  |

- **수치형** 데이터 : 위의 no 컬럼처럼 숫자만으로 구성된 데이터
- **문자열형** 데이터 : 위의 name 컬럼처럼 임의의 문자로 구성된 데이터
- **날짜시간형** 데이터 : 위의 birthday 컬럼처럼 날짜와 시각의 데이터로 구성된 데이터

**각 컬럼은 하나의 자료형만 가질 수 있습니다.**

<br/>

## 4) 값이 없는 데이터 = NULL

위 예시에서 홍길동의 birthday 가 NULL로 적혀있는데, 이것은 NULL 이라는 문자열 데이터가 아니라 **'아무것도 저장 되어 있지 않은 상태'** 를 뜻합니다.
