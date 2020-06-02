---
layout: page
title: "select fetch- SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "select"
    - "fetch"
---

# 값 읽어오기
---
`select` 쿼리는 반환 값을 가지고 있는 타입입니다.

결과값은 `배열` 또는 `객체`로 읽어 올 수 있습니다.

<br>

## 패치타입
---
* PDO::FETCH_NUM : 숫자 인덱스 배열 반환
* PDO::FETCH_ASSOC : 컬럼명이 키인 연관배열 반환
* PDO::FETCH_BOTH : 위 두가지 모두
* PDO::FETCH_OBJ : 컬럼명이 프로퍼티인 인명 객체 반환

<br>

## pdo fetch
---
jinyMysql은 PDO를 통한 데이터 컨넥션을 처리합니다. PDO는 기본적으로 데이터를 읽이 위한 두가지 타입의 fetch를 제공합니다. 
내부적으로 fetch 동작을 수행할 수 있도록 2개의 brige 메소드를 제공합니다.

```php
public function fetch($type=PDO::FETCH_OBJ)
{
    return $this->stmt->fetch($type);
}

public function fetchAll($type=PDO::FETCH_ASSOC)
{
    return $this->stmt->fetchAll($type);
}
```

<br>

## 객체 읽기
---
생성된 쿼리를 실행하고 fetchObj() 메소드를 호출하는 동작을 수행합니다.
* runObj() : 객체로 읽기

### 복수값 데이터
---
데이터가 여러개가 있을 경우 반복적인 읽기 작업이 필요합니다.
이를 쉽게 처리하기 위해서 복수의 결과값을 읽어 올 수 있도록 전용 메소드를 제공합니다.

생성된 쿼리를 실행하고 fetchObjAll() 메소드를 호출하는 동작을 수행합니다.
* runObjAll()

<br>

## 배열 읽기
---
생성된 쿼리를 실행하고 fetchAssoc() 메소드를 호출하는 동작을 수행합니다.
* runAssoc() : 배열로 읽기

<br>

### 복수값 데이터
---
생성된 쿼리를 실행하고 fetchAssocAll() 메소드를 호출하는 동작을 수행합니다.
* runAssocAll()

<br>

## 데이터 갯수 조회
---
테이블에 있는 데이터의 갯수를 조회할 수 있습니다.

```php
$count = $db->select("members4")->count();
```
