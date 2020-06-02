---
layout: page
title: "schema is - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "schema"
    - "is"
---

# 스키마 확인
---
mysql에 지정한 스키마가 존재하는지 확인 합니다.

<br>

## is()
---
`is()` 메소드는 데이터베이스에서 인자값으로 전달한 스키마가 존재하는지를 확인 합니다.

```php
$schemaObj->is("db2020");
```

<br>

## 예제코드
---

|예제코드| ./samples/schema/schema-04.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 스키마 목록
$schemaObj = $db->schema();
$name = "db2020";
if ($schemaObj->is($name)) {
    echo $name. "스키마가 존재합니다.\n";
} else {
    echo $name. "스키마가 없습니다.\n";
}
```

|실행결과|
```console
$ php schema-04.php
db2020스키마가 존재합니다.
```