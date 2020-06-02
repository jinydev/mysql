---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "table"
    - "create"
---

# 테이블 생성
---
스키마에 새로운 테이블을 생성합니다. 
테이블은 직접 SQL 쿼리 또는 생성 메소드를 통하여 생성할 수 있습니다.

<br>

## Raw 쿼리를 이용한 생성
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

## createEmpty() : 테이블 골력생성
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

> alias : empty() 메소드로도 호출이 가능합니다.

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

## 구조생성
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

## 필드설정
---
Table 클래스의 create 메소드는 전달받은 컬럼정보를 이용하여 객체를 생성합니다.
또는 외부 setter 메소드를 톻하여 설정된 컬럼필드 배열값을 이용하여 테이블을 생성할 수 있습니다.

키-값 형태로 컬럼필드를 설정합니다.
```php
setField($name, $value);
```

복수의 컬럼필드를 설정할때에는 복수형 setter 메소드를 사용할 수 있습니다.

```php
setFields($fields);
```

설정한 컬럼필드를 삭제할 수 있습니다.

```php
unsetField($name);
```

전체 컬럼 필드 초기화

```php
clearFields();
```

설정된 컬럼필드가 있는경우 `create()`메소드를 인자값 없이 호출하면 됩니다.



## rename
---
테이블의 이름을 변경합니다.

```php
rename($old, $new);
```

<br>

## 테이블 생성조건 설정
---

### 엔진설정
---
create와 empty 메소드는 자동적으로 테이블을 생성합니다. 테이블 생성시 적용되는 DB엔진의 종료를 설정할 수 있습니다.

```php
engine("종류");
```

`engine()`메소드는 전달받은 인자값을 객체의 내부 프로퍼티로 값을 설정하는 setter 메소드 입니다.

엔진 설정값이 없는 경우에는 기본적으로 `InnoDB`값으로 설정됩니다.

> engin() 메소드는 table 클래스에 선언이 되어 있습니다.

<br>

### 문자셋
---
테이블에 적용되는 문자셋을 설정합니다. 기본값은 `utf-8`입니다.
`charset()` 메소드를 이용하여 기본 문자셋을 변경할 수 있습니다.

```php
charset("설정값");
```

> charset() 메소드는 table 클래스에 선언이 되어 있습니다.

<br>

## 컬럼필드 매칭
---
`save()` 메소드는 전달받은 매개변수 배열정보에 따라 데이터를 자동 삽입합니다. 

insert-auto01.php

컴럼 정보가 불일치 하게 되면, Exception을 통하여 오류를 보고합니다.

### auto
컬럼필드가 매칭이 되지 않는 경우 자동으로 필드를 맞추어 생성합니다.

```php
auto();
```
