---
layout: page
title: "insert - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "insert"
--- 

# 데이터삽입
---
insert 쿼리를 이용하여 데이터를 삽입할 수 있습니다.

<br>

## Raw 쿼리를 이용한 직접입력
---

|예제코드| insert-raw.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터삽입
$query = "INSERT `db2020`.`members4` SET firstname = 'lee', lastname='hojin';";
$db->query($query); 

if ($id = $db->conn->lastInsertId()) {
    echo "데이터 삽입 성공 = ".$id;
} else {
    echo "데이터 삽입 실패";
}
```

|실행결과|
```
$ php insert-raw.php 
데이터 삽입 성공 = 1
```

<br>

## bind 데이터 삽입
---
SQL과 삽입되는 데이터를 bind 하여 쿼리를 전송할 수 있습니다.
bind를 같이 사용하면, 안전하게 데이터를 삽입할 수 있습니다.

SQL 쿼리를 bind합니다. bind는 PDOStatement를 반환합니다.


|예제코드| insert-bind.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// bind 데이터삽입
$query = "INSERT `db2020`.`members4` SET firstname=:firstname, lastname=:lastname;";
$data = [
    'firstname' => "이", 
    'lastname' => "호진"
];

$stmt = $db->binds($query, $data);
$stmt->execute();
if ($id = $db->conn()->lastInsertId()) {
    echo "데이터 삽입 성공 = ".$id;
} else {
    echo "데이터 삽입 실패";
}
```

데이터를 삽입한 후에, 마지막 id 값을 읽어 올 수 있습니다.
PDO의 `lastInsertId()`를 호출할 수 있습니다. 

<br>

## 데이터 삽입
---
쿼리빌더 `insert` 클래스를 통하여 데이터를 삽입합니다.

```php
$db->insert("members4", $data)->save();
```

또는

```php
$db->insert("members4")->save($data);
```

예제코드: insert-save.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터삽입
$data = [
    'firstname' => "이"
];

if ($id = $db->insert("members4", $data)->save()) {
    echo "데이터 삽입 성공 = ".$id;
} else {
    echo "데이터 삽입 실패";
}
```

<br>

### save()
---
sql 쿼리를 생성하여 배열 데이터를 입력 할 수 있습니다.
save 메소드는 입력된 배열에 따라 sql insert 쿼리를 생성합니다. 

성공적으로 데이터가 삽입이 되면, 마지막에 삽입된 id값을 반환 합니다.

<br>

### created_at, updated_at
---
쿼리빌더를 이용하여 데이블을 생성하면, row 데이터의 이력을 추적하기 위한 `created_at`, `updated_at` 필드가 같이 생성이 됩니다.  
데이터 삽입시 `insert` 객체의 save 메소드를 이용하면, created_at 과 updated_at을 자동으로 입력할 수 있습니다.

<br>

## setFields
---
삽입할 배열 데이터를 지정할 수 있습니다.

|예제코드| insert-field.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터삽입
$data = [
    'lastname' => "호진"
];

$last = $db->insert("members4")->setFields($data)->save();
echo "마지막 삽입=".$last;
```

<br>

## 마지막 id
---
`last()` 메소드는 데이터삽입후 마지막 id 값을 확인할 수 있습니다.

last 메소드는 PDO의 `lastInsertId()` 메소드의 브리지 입니다.







