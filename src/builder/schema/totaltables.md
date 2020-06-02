---
layout: page
title: "schema totalTables - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "schema"
    - "totaltables"
---

# 테이블 갯수
---
선택한 스키마의 테이블 갯수를 확인 합니다.

<br>

## totalTables()
---
`totalTables()` 메소드는 스키마에 포함된 테이블의 갯수를 반환합니다.

```php
$db->schema()->totalTables("스키마명");
```

<br>

## 예제코드
---

|예제코드| ./samples/shcema/schema-03.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 스키마 목록
$schemaObj = $db->schema();
$rows = $schemaObj->list();
foreach ($rows as $name) {
    echo $name. "=";
    echo $schemaObj->totalTables($name). "\n";
    //print_r($row);
}
```

|실행결과|
```console
$ php schema-03.php 
db2020=3
information_schema=67
```

<br>
