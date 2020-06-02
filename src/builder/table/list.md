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


# 테이블 정보 및 부가기능
---

<br>

## info
---
테이블의 정보를 확인합니다.

```php
info($name)
```

<br>

## desc() : 테이블 구조
---
테이블의 구조를 확인할 수 있습니다.

|예제코드| table-desc.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 구조
$rows = $db->table("members2")->desc();
print_r($rows);
```

|실행결과|
```console
$ php table-desc.php
Array
(
    [0] => Array
        (
            [Field] => id
            [Type] => int(11)
            [Null] => NO
            [Key] => PRI
            [Default] =>
            [Extra] => auto_increment
        )

    [1] => Array
        (
            [Field] => created_at
            [Type] => datetime
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

    [2] => Array
        (
            [Field] => updated_at
            [Type] => datetime
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

)
```
실행 결괏값은 2차원 배열로 출력됩니다. 1차 index 배열값은 각 컬럼을 의미합니다.
2차 연상배열은 컬럼의 정보값을 의미합니다.

<br>


## 테이블 확인
---
테이블이 존재하는지 확인을 할 수 있습니다.

```php
public is($name) : bool
```

예제코드: table-is.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 목록출력
$name = "members1";
if ($db->table()->is($name)) {
    echo $name. "테이블이 존재합니다.\n";
} else {
    echo $name. "테이블이 없습니다.\n";
}
```

|실행결과|
```console
$ php table-is.php 
members1테이블이 존재합니다.
```

<br>

## 데이터 갯수 확인
---
확장된 테이블 객체를 활용하여 데이터의 갯수를 확인합니다. 데이터의 갯수는 primary key로 설정된 id 컬럼의 갯수를 체크합니다.

```php
/**
 * 데이터 갯수 확인
 */
$count = $db->table("board")->count();
echo "데이터 갯수=".$count;
```

`count()` 메소드는 테이블의 전체 데이터의 갯수를 반환합니다. 

<br>

