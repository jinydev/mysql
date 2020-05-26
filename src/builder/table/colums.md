---
layout: page
title: "table colums- SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "table"
    - "colums"
---

# 테이블 컬럼
---


## addColums() : 테이블 필드 추가
---
생성한 테이블에 필드를 추가할 수 있습니다.

|예제코드| colum-add.php
```php
<?php
require "../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = include("../dbinfo.php");

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 생성
$addFields = [
    'age' => "int(10)",
    'address' => "varchar(100)",
];

$db->table("members1")->addColums($addFields);

// 테이블 구조
$rows = $db->tableDesc("member1");
print_r($rows);
```

|출력결과|
```console
$ php colum-add.php
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
            [Field] => age
            [Type] => int(10)
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

    [2] => Array
        (
            [Field] => address
            [Type] => varchar(100)
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

)
```

<br>

## modify() : 테이블 컬럼 변경
---
예제코드: colum-modify.php

```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 생성
$fields = [
'age' => "int(6)",
'address' => "varchar(250)",
];

$db->table("members1")->modifyColums($fields);

// 테이블 구조
$rows = $db->table()->desc("members1");
print_r($rows);
```

|실행결과|
```console
$ php colum-modify.php 
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
            [Field] => age
            [Type] => int(6)
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

    [2] => Array
        (
            [Field] => address
            [Type] => varchar(250)
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

)
```
`age`와 `address`의 컬럼 정보가 변경이 된 것을 확인할 수 있습니다.

<br>

## 테이블 컬럼 수정
---
예제코드: colum-change.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 컬럼정보 변경
$fields = [
    'age'=>['birth'=>"date"]
];

$db->table("members1")->changeColums($fields);

// 테이블 구조
$rows = $db->table("members1")->desc();
print_r($rows);
```

|실행결과|
```console
$ php colum-change.php 
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
            [Field] => birth
            [Type] => date
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

    [2] => Array
        (
            [Field] => address
            [Type] => varchar(250)
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

)
```

<br>

## 컬럼 삭제
---

예제코드: colum-drop.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 삭제 컬럼 (index array)
$fields = ['birth' ,'address'];

$db->table("members1")->dropColums($fields);

// 테이블 구조
$rows = $db->table()->desc("members1");
print_r($rows);
```

