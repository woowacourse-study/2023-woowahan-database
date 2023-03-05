# 목차

1. [ORDER BY로 검색 결과 정렬하기](#1-ORDER-BY로-검색-결과-정렬하기) <br/>
2. [ORDER BY DESC로 내림차순으로 정렬하기](#2-ORDER-BY-DESC로-내림차순으로-정렬하기) <br/>
3. [대소관계](#3-대소관계) <br/>
4. [ORDER BY는 테이블에 영향을 주지 않는다](#4-ORDER-BY는-테이블에-영향을-주지-않는다) <br/>

<br/>

# 9강 -정렬 - ORDER BY

## 1) ORDER BY로 검색 결과 정렬하기
- SYNTAX
  ```
    SELECT 열명 
    FROM 테이블명 
    WHERE 조건식 
    ORDER BY 열명
  ```
  - 지정된 열의 값에 따라 **행 순서가 오름차순으로 정렬된다.**
  - WHERE구가 없는 경우에는 FROM의 뒤에 위치한다.
    
<br/>

## 2) ORDER BY DESC로 내림차순으로 정렬하기
- SYNTAX
  ```
    SELECT 열명 
    FROM 테이블명 
    WHERE 조건식 
    ORDER BY 열명 DESC
  ```
  - ORDER BY 열명 뒤에 DESC(Descendant- 하강)를 붙여 내림차순으로 설정한다.
  - DESC 가 없을 때에는 오름차순으로 정렬되었는데 사실은 ASC(Ascendant-상승)라는 구문이 생략된 모습이다.

<br/>

## 3) 대소관계
**수치형과 문자열형 데이터는 대소관계의 계산 방법이 다르다!**

a열이 수치형(INTEGER), b행이 문자열형(VARCHAR) 인 테이블 

| a   | b   |
|-----|-----|
| 2   | 2   |
| 1   | 1   |
| 11  | 11  |
| 10  | 10  |

- a열로 정렬하기
    ```
    SELECT * 
    FROM T 
    ORDER BY a
  ```

| a   | b   |
|-----|-----|
| 1   | 1   |
| 2   | 2   |
| 10  | 10  |
| 11  | 11  |
- b열로 정렬하기
    ```
    SELECT * 
    FROM T 
    ORDER BY b
  ```

| a   | b   |
|-----|-----|
| 1   | 1   |
| 10  | 10  |
| 11  | 11  |
| 2   | 2   |
**문자열형 데이터의 대소관계는 사전식 순서에 의해 결정된다!**

## 4) ORDER BY는 테이블에 영향을 주지 않는다
ORDER BY는 SELECT문에 종속적인 예약어.

즉 검색한 결과값에 대한 정렬을 진행하기 때문에 데이터의 참조만 이뤄지고 **실제 테이블의 위치 변경은 하지 않는다.**
