---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "Table"
    - "list"
---

# 테이블 목록
---
스키마의 테이블 목록을 확인합니다.

<br>

## rawSQL
---
스키마의 테이블 목록을 확인하기 위해서는 `SHOW TABLES` 쿼리를 전달해야 합니다. 

```sql
SHOW TABLES;
```

현재 스키마의 모든 테이블의 목록을 출력합니다.

<br>

## list() : 테이블 목록
---
table 클래스의 list메소드는 `show tables`쿼리를 대신 전송하여 결과값을 배열로 반환을 합니다.

```php
$db->table()->list();
```
테이블 팩토리메소드를 호출한 후에, list() 메소드를 호출하면 됩니다.

|예제코드|: table-list01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 목록출력
print_r($db->table()->list());
```

|실행결과|
```console
$ php table-list.php 
Array
(
    [0] => Array
        (
            [Tables_in_db2020] => members2
        )

)
```

결과값는 2차원 배열로 출력됩니다.
첫번째 배열은 indexed 배열입니다. 각각의 배열은 다시 연상배열값을 가지게 됩니다.
연상배열의 컬럼명은 `Tables_in_스키마`로 자동 설정 됩니다.

<br>

## 컬럼명 없애기
---
불필요한 컬럼명을 indexed 배열로 변경하여 출력을 할 수 있습니다.

`list()` 메소드의 인자값으로 `false`를 전달합니다.

|예제코드| table-list02.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 목록출력
$list = $db->table()->list(false);
print_r($list);
```

|출력결과|
```console
$ php table-list02.php 
Array
(
    [0] => members2
)
```

