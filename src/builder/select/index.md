---
layout: page
title: "select - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "select"
--- 

# 데이터 조회
---
테이블의 데이터를 조회합니다.

* [쿼리설정](query)

<br>

## Raw 쿼리를 이용한 목록출력
---

예제코드: select-raw.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터삽입
$query = "SELECT * FROM `db2020`.`members4`;";
if ($rows = $db->query($query)->fetchObjAll()) {
    foreach($rows as $row) {
        foreach($row as $key => $value) {
            echo $key. "=". $value. "\t";
        }
        echo "\n";
    }
} else {
    echo "데이터목록이 없습니다.";
}
```

|실행결과|
```console
$ php select-01.php 
데이터목록이 없습니다.
```

<br>

## 객체 확장하기
---
connection 객체는 데이터를 조작할 수 있는 select 객체를 확장합니다.
확장된 select 객체는 다양한 조건의 데이터를 조회할 수 있습니다.

<br>
### select 객체 얻기
---
select() 메소드 호출시 객체를 얻을 수 있습니다.

```php
$dataObj = $db->select("테이블명");
```

<br>

## all() : 전체 데이터 조회
---
데이블의 전체 데이터를 조회 합니다.

`SELECT * `와 같은 동작결과를 반환합니다.

```php
$dataObj->all();
```
all 메소드는 테이블의 전체 데이터를 조회 합니다.

예제코드: select-all.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

// select 객체 얻기
$dataObj = $db->select("members4");

if ($rows = $dataObj->all()) {
    foreach($rows as $row) {
        foreach($row as $key => $value) {
            echo $key. "=". $value. "\t";
        }
        echo "\n";
    }
} else {
    echo "데이터목록이 없습니다.";
}
```

|출력결과|
```console
$ php select-all.php 
id=1    firstname=lee   lastname=hojin  created_at=     updated_at=
id=2    firstname=lee   lastname=hojin  created_at=     updated_at=
```

<br>

## 컬럼 선택
---
출력할 컬럼을 선택합니다.

### setFields
---
출력할 필드만 선택할 수 있습니다.

|예제코드| select-fields01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터목록
$select = $db->select("members4")->setFields(["id","firstname"]);
if ($rows = $select->fetchObjAll()) {
    foreach($rows as $row) {
        foreach($row as $key => $value) {
            echo $key. "=". $value. "\t";
        }
        echo "\n";
    }
} else {
    echo "데이터목록이 없습니다.";
}
```

|출력결과|
```console
$ php select-fields01.php 
id=1    firstname=lee
id=2    firstname=lee
```

### 매개변수 전송
---
별도의 setField 메소드를 호출하지 않고, select 메소드의 2번째 인자로도 컬럼을 선택할 수 있습니다.

|예제코드| select-fields02.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터목록
if ($rows = $db->select("members4", ["id","firstname"])->fetchObjAll()) {
    foreach($rows as $row) {
        foreach($row as $key => $value) {
            echo $key. "=". $value. "\t";
        }
        echo "\n";
    }
} else {
    echo "데이터목록이 없습니다.";
}
```

<br>

## 쿼리 빌더하기
---
`select` 클래스에 설정된 값에 의해서 SQL 쿼리를 빌드합니다.
`build()` 메소드를 호출합니다.  

```php
$db->select("members4", ["id","firstname"])->build();
```
`build()`는 단순한 쿼리만을 자동 생성하여 select 객체 내부에 저장합니다.
생성된 쿼리 문장은 `getQuery()` 메소드를 통하여 확인을 할 수 있습니다. 

이렇게 생성된 쿼리는 `run()` 메소드를 실행하면, stmt 값을 얻을 수 있습니다.
stmt 값을 통하여 값을 읽어 올 수 있습니다.

```php
$rows = $db->select("members4", ["id","firstname"])->build()->run()->fetchObjAll();
```

|예제코드|
select-03.php
select-04.php

<br>
