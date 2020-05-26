---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
    - "rawsql"
---

# Raw 쿼리를 이용한 삭제
---
테이블안에 있는 데이터를 삭제하기 위해서는 sql의 delete 명령을 사용합니다. 
직접 raw SQL 문장을 작성하여 mysql 데이터베이스에 전송을 할 수 있습니다.

<br>

## 쿼리문 작성
---
다음과 같이 쿼리 문장을 작성합니다.

```php
$query = "DELETE FROM `db2020`.`members4` where id=1;";
```
<br>

## 쿼리문 전송
---
작성한 쿼리문장을 빌더의 `query()` 메소드를 통하여 전송을 합니다.  

```php
$db->query($query);
```

<br>

## 예제코드
---
예제코드를 통하여 간단한 데이터 삭제를 실습해 봅니다.

|예제코드| delete-sql.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터삭제
$query = "DELETE FROM `db2020`.`members4` where id=1;";
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

raw쿼리를 전송한 후에 테이블의 데이터를 확인 출력합니다.

<br>