---
layout: page
title: "schema - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "schema"
--- 

# 스키마 데이터베이스
---
mysql은 다수의 스키마를 생성하여 관리를 할 수 있습니다. 
`Connection` 객체를 통하여 mysql 데이터베이스와 연결을 하게 되면, 
`schema()` 메소드를 통하여 스키마 객체와 관계를 설정할 수 있습니다. 

```php
// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);
$schemaObj = $db->schema();
```

`schema()` 메소드는 schema 클래스의 객체를 반환합니다.
> [소스코드](code) 학습하기
<br>

## list() : 스키마 목록
---
사용자 계정의 스키마 목록을 확인합니다.

예제코드: ./sample/schema/schema-01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 구조
$rows = $db->schema()->list();
print_r($rows);
```

|출력결과|
```console
$ php schema-01.php 
Array
(
    [0] => db2020
    [1] => information_schema
)
```

<br>

## create() : 스키마 생성
---
`create()` 메소드는 새로운 스키마를 생성합니다. 인자값으로 생성할 스키마명을 전달하면 됩니다.

```php
$name = "jinyshop";
// 스키마 생성
$db->schema()->create($name);
```

|예제코드| ./sample/schema/schema-02.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 스키마 생성
$name = "jinyshop";
// 스키마 생성
$db->schema()->create($name);

// 스키마 목록
$rows = $db->schema()->list();
print_r($rows);
```

하지만 위의 코드를 실행하면 다음과 같은 오류가 발생합니다.
```console
$ php schema-02.php
PHP Fatal error:  Uncaught PDOException: SQLSTATE[42000]: Syntax error or access violation: 1044 Access denied for user 'db2020'@'%' to database 'jinyshop' in E:\01.jiny\mysqlAdmin\vendor\jiny\mysql\src\Connection.php:131
Stack trace:
#0 E:\01.jiny\mysqlAdmin\vendor\jiny\mysql\src\Connection.php(131): PDO->query('create database...')
#1 E:\01.jiny\mysqlAdmin\vendor\jiny\mysql\src\Schema.php(28): Jiny\Mysql\Connection->query('create database...')
#2 E:\01.jiny\mysqlAdmin\vendor\jiny\mysql\sample\schema\schema-02.php(13): Jiny\Mysql\Schema->create('jinyshop')
#3 {main}
  thrown in E:\01.jiny\mysqlAdmin\vendor\jiny\mysql\src\Connection.php on line 131
```

새로운 스키마를 생성하기 위해서는 스키마 생성을 위한 `접근 권한`이 있어야 합니다. 
DB사용자 계정에 접근권한을 추가한 후에 코드를 다시 실행합니다.

<br>
