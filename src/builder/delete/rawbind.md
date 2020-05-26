---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
    - "rawbind"
---

# Raw 쿼리에 데이터 bind 하기
---
삭제를 위한 raw SQL 쿼리에 데이터를 bind하여 실행을 할 수 있습니다.

<br>

## 쿼리문 작성
---
다음과 같이 쿼리문장과 bind를 위한 키를 같이 작성합니다.

```php
$query = "DELETE FROM `db2020`.`members4` where id=:id;";
```

삭제를 위한 조건 id값을 `:id` 키로 작성을 하였습니다.

<br>

## 데이터 바인딩
---
작성한 쿼리문에 데이터를 바인딩 처리합니다. 데이터 바인딩은 `Connection` 객체의 `binds()` 메소드를 이용하면 됩니다.  

다음과 같이 bind를 처리합니다. 첫번째 인자값으로는 쿼리문장을 두번째 인자값으로 데이터값을 전달 합니다.

```php
$data = ['id'=>2];
$stmt = $db->binds($query, $data);
```

바인딩 하는 데이터는 연상배열 형태로 작성을 합니다. 연상배열의 키값은 bind의 키값과 동일하게 지정을 합니다.
`binds()` 메소드는 입력된 연상배열이 키값과 쿼리의 키값을 비교하여 bind 처리를 합니다.

<br>

## bind된 쿼리 실행하기
---
일반적인 쿼리는 `Connection` 객체의 `query()` 메소드만 호출을 함으로서 실행을 할 수 있습니다. 
하지만, bind된 쿼리는 별도의 실행 명령을 입력해 주어야 됩니다.

```php
$stmt->execute();
```

<br>

## 예제코드
---
rawSQL에 데이터를 바인딩하여 쿼리를 실행해 보도록 합니다.

예제코드: delete-bind.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터삭제
$query = "DELETE FROM `db2020`.`members4` where id=:id;";
$data = ['id'=>2];

$stmt = $db->binds($query, $data);
$stmt->execute();

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