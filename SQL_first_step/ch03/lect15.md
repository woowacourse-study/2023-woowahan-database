# 목차

1. [CASE 문](#1-CASE-문) <br/>
2. [또 하나의 CASE 문](#2-또-하나의-CASE-문) <br/>
3. [CASE를 사용할 경우 주의사항](#3-CASE를-사용할-경우-주의사항) <br/>

<br/>

# 15강 - CASE 문으로 데이터 변환하기

## 1) CASE 문

- SYNTAX

  ```
  CASE WHEN 조건식1 THEN 식1
  [WHEN 조건식2 THEN 식2]
  [WHEN 조건식3 THEN 식3]
  ...
  [ELSE 식4]
  END
  ```
- if-else문과 동일한 방식으로 보면 된다.

## 2) 또 하나의 CASE 문

위의 방식 외에 단순 CASE 식이라는 형식이 존재하는데, switch 형식으로 이해하면 된다.

```
CASE a
WHEN 1 THEN '남자'
WHEN 2 THEN '여자'
ELSE '미지정'
END
```

## 3) CASE를 사용할 경우 주의사항

CASE 문은 SELECT 구 이외에도 WHERE 구와 ORDER BY 구에서도 사용할 수 있다.\

- ELSE 생략
  ELSE를 생략하면 **ELSE NULL**이 된다
  대응하는 WHEN 이 하나도 없으면 NULL이 반환되니 CASE 문의 ELSE는 생략하지 않는 편이 낫다.
