# 목차

1. [INSERT로 행 추가하기](#1-insert로-행-추가하기)
2. [값을 저장할 열 지정하기](#2-값을-저장할-열-지정하기)
3. [NOT NULL 제약](#3-not-null-제약)
4. [DEFAULT](#4-default)

# 16강 - 행 추가하기 INSERT

## 1. INSERT로 행 추가하기

```SQL
INSERT INTO 테이블명 VALUES(값1, 값2, ...);
```

- 행의 데이터는 `VALUES` 구를 사용해 지정한다.
- 값을 지정할 때는 해당 열의 데이터 형식에 맞도록 지정해야 한다.

실행 예시)

```SQL
INSERT INTO sample41 VALUES(1, 'ABC', '2023-02-20');
```

결과 )
| no | a | b |
| -- | --- | ----|
| 1 | ABC | 2023-02-20 |

## 2. 값을 저장할 열 지정하기

```SQL
INSERT INTO 테이블명 (열1, 열2, ...) VALUES(값1, 값2, ...);
```

- INSERT 명령으로 행을 추가할 경우 **값을 저장할 열을 지정**할 수 있다.
- 별도의 값을 지정하지 않은 열에는 기본값(default 값)이 들어간다.

실행 예시)

```SQL
INSERT INTO sample41(a, no) VALUES('XYZ', 2);
```

결과)
| no | a | b |
| -- | --- | ----|
| 1 | ABC | 2023-02-20 |
| 2 | XYZ | NULL|

## 3. NOT NULL 제약

행을 추가할 때 유효한 값이 없는 상태(NULL)로 두고 싶을 경우에는 VALUES 구에서 NULL로 값을 지정할 수 있다.

실행 예시)

```SQL
INSERT INTO sample41(no, a, b) VALUES(NULL, NULL, NULL);
```

하지만 앞의 명령을 실행하면 에러가 발생한다. ⛔️ <br />
-> no 열에 대해 NULL 값을 허용하지 않는 **NOT NULL 제약**이 걸려있기 때문이다.

## 4. DEFAULT

먼저 DESC 커맨드로 sample411의 열 구성을 살펴보자.

```SQL
DESC sample411;
```

| Field | Type    | Null | Key | Default | Extra |
| ----- | ------- | ---- | --- | ------- | ----- |
| no    | int(11) | NO   |     | NULL    |       |
| d     | int(11) | YES  |     | 0       |       |

Default는 **명시적으로 값을 지정하지 않았을 경우 사용하는 초깃값**이다.

```SQL
INSERT INTO sample411(no, d) VALUES(2, DEFAULT);
```

- 값 지정 시 DEFAULT 키워드로 지정할 수 있다.

```SQL
INSERT INTO sample411(no) VALUES(2);
```

- 저장할 열을 별도로 지정하지 않을 수 있다. (암묵적으로 디폴트 저장)
- 열을 지정하지 않으면 디폴트값으로 행이 추가된다.

위의 두 명령 모두 결과는 아래와 같다.
| no | d |
| -- | --- |
| 1 | 1 |
| 2 | 0 |
