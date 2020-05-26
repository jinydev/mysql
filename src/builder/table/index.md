---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "Table"
--- 

# 테이블 생성
---
데이터베이스 테이블을 생성합니다.

<br>

## 테이블 기능확장
---
conntection 클래스는 필요한 테이블 데이터 작업을 위해서 클래스를 동적 확장합니다.
table() 메소드는 테이블 객체를 확장하는 플라이웨이트 패턴 입니다. 인자값으로 테이블명을 전달합니다.

```php
$db->table("테이블명");
```

<br>

## tableList() : 테이블 목록
---
스키마의 테이블 목록을 출력합니다. 반환값은 array 입니다.

|예제코드|: table-list.php
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
)
```

<br>

## 테이블생성
---
스키마에 새로운 테이블을 생성합니다. 
테이블은 직접 SQL 쿼리 또는 생성 메소드를 통하여 생성할 수 있습니다.

### Raw 쿼리를 이용한 생성
---
일반적인 sql 쿼리문을 이용하여 데이블을 생성해 봅니다.
`create` 명령은 테이블을 생성하는 쿼리 입니다.

다음과 같이 쿼리문장을 생성하여 전달하면 됩니다.
```php
// 테이블 생성쿼리
$query = "CREATE TABLE `db2020`.`member1` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    primary key(`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;";
$db->query($query); 
```

|예제코드| ./sample/tables/table-rawsql.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 쿼리 예제
// 테이블 생성쿼리
$query = "CREATE TABLE `".$dbinfo['schema']."`.`member1` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    primary key(`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;";

$db->query($query); 

// 테이블 목록출력
print_r($db->table()->list());
```

|실행결과|
```console
$ php table-rawsql.php
Array
(
    [0] => Array
        (
            [Tables_in_db2020] => member1
        )

)
```

<br>

### createEmpty() : 테이블 골력생성
---
`createEmpty` 메소드는 기본 골력의 테이블을 생성합니다.  
테이블 기본 골력은 다음과 같은 필드만 포함합니다.
* id
* created_at
* updated_at

```php
// 테이블 생성
$db->table()->createEmpty("member2");
```

|예제코드| table-empty01.php 
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 생성
$db->table()->createEmpty("members2");

// 테이블 목록출력
print_r($db->table()->list());
```

입력한 인자값으로 테이블을 생성합니다.

|실행결과|
```
$ php table-empty01.php 
Array
(
    [0] => Array
        (
            [Tables_in_db2020] => member1
        )

    [1] => Array
        (
            [Tables_in_db2020] => members2
        )

)
```

또는 먼저 테이블 명을 선택한 후에 빈 테이블을 생성할 수도 있습니다.

```php
// 테이블 생성
$db->table("members3")->createEmpty();
```
|예제코드| table-empty02.php 

<br>


### 구조생성
---
요청한 구조의 테이블을 생성할 수 있습니다.  
테이블은 컬럼명과 필드속성을 한쌍을 가지고 있습니다.  

추가되는 테이블을 연상배열로 설정을 합니다.

|예제코드|: table-05.php

```php
// 테이블 생성
$columns = [
'firstname' => "varchar(50)",
'lastname' => "varchar(100)",
];

$db->table("member4")->create($columns);
```

두번째 인자값으로 컬럼정보의 배열을 전달합니다. 

|예제코드| table-create01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 생성
$columns = [
'firstname' => "varchar(50)",
'lastname' => "varchar(100)",
];

$db->table("members4")->create($columns);

// 테이블 목록출력
print_r($db->table()->list());
```

|실행결과|
```console
$ php table-create01.php 
Array
(
    [0] => Array
        (
            [Tables_in_db2020] => members1
        )

    [1] => Array
        (
            [Tables_in_db2020] => members2
        )

    [2] => Array
        (
            [Tables_in_db2020] => members3
        )

    [3] => Array
        (
            [Tables_in_db2020] => members4
        )

)
```

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

## info
---
테이블의 정보를 확인합니다.

```php
info($name)
```

## rename
---
테이블의 이름을 변경합니다.

```php
rename($old, $new);
```
