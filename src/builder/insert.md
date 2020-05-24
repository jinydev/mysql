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

## 데이터 삽입
---
예제코드: insert-03.php



```php
public function insert($query)
```


## bind 데이터 삽입

예제코드: insert-02.php






