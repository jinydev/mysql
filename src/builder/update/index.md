---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
--- 

# 갱신
---

## Raw 쿼리를 이용한 갱신
---

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

if ($rows = $db->select("members4")->fetchObjAll()) {
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

## bind 처리
---

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
$db->update("member5")->bind($query,[
    'id'=>4,
    'firstname'=>"jiny",
    'lastname'=>"lee"
]);

if ($rows = $db->select("members4")->fetchObjAll()) {
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


## update 객체
---


|예제코드| update-03.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터갱신
$db->update("members4")->setFields(['firstname'=>"1234"])->id(5);

if ($rows = $db->select("members4")->fetchObjAll()) {
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


