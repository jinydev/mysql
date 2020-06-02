---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
---

# raw 쿼리
---
직접 작성한 sql 쿼리를 전송하여 `갱신`작업을 실행합니다.

쿼리는 크게 2가지 타입으로 실행을 할 수 있습니다. 
첫번째는 `connection` 클래스의 `query` 메소드를 이용하는 방법과 
두번째는 빌더의 `setQuery` 메서드를 활용하는 방법입니다.

<br>

## query 메소드
---
`connection`의 `query` 메소드를 활요하여 rawSQL을 전송합니다.


예제코드: update-01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터갱신
$query = "UPDATE `db2020`.`members4` SET firstname='lee', lastname='hojin' where id=3;";
$db->query($query);

if ($rows = $db->select("members4")->runObjAll()) {
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

## raw 쿼리에 데이터 bind 하기
---
직접 작성한 raw쿼리에 데이터를 bind 할 수 있습니다.



예제코드: update-02.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터갱신
$query = "UPDATE `db2020`.`members4` SET firstname=:firstname, lastname=:lastname where id=:id;";
$db->update("member5")->binds($query,[
    'id'=>4,
    'firstname'=>"jiny",
    'lastname'=>"lee"
]);

if ($rows = $db->select("members4")->runObjAll()) {
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