# 목차

1. [DELETE로 행 삭제하기](#1-delete로-행-삭제하기)
2. [DELETE 명령 구](#2-delete-명령-구)

# 17강 - 삭제하기 DELETE

## 1. DELETE로 행 삭제하기

```SQL
DELETE FROM 테이블명 WHERE 조건식;
```

- 위와 같은 명령으로 조건식에 맞는 행을 삭제한다.
- WHERE 구를 지정하지 않으면 해당 테이블의 모든 행이 삭제된다.

💡 DELETE 명령은 WHERE 조건에 일치하는 '모든 행'을 삭제한다!

## 2. DELETE 명령 구

WHERE 구에서 대상이 되는 행을 검색하는 것은 SELECT 명령에서도 DELETE 명령에서도 똑같다. <br />
DELETE 명령에서는 조건에 맞는 행이 삭제된다는 점만 다르다.

실행 예시 )

```SQL
DELETE FROM sample41 WHERE no = 1 OR no = 2;
```

위의 명령은 no 열이 1 이거나 2인 행을 모두 삭제한다.

- DELETE 명령에서 ORDER BY 구는 사용할 수 없다. (어떤 행부터 삭제할 것인지는 중요하지 않기 때문)
- MySQL에서는 가능!! - ORDER BY 구와 LIMIT 구를 사용해 행을 지정할 수 있음
