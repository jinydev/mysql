---
layout: page
title: "table drop - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "table"
    - "drop"
---

# 테이블 삭제
---

## drop() 메소드
---
table 객체의 drop 메소드는 스키마의 테이블을 삭제합니다.

```php
$db->table("테이블명")->drop();
```

|예제코드| table-drop01.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

$db->table("members4")->drop();

// 테이블 목록출력
print_r($db->table()->list());
```

## 삭제할 테이블 지정하기
---
기본적으로 drop() 메소드만 호출할 경우에는 객체에 설정된 기본 테이블을 삭제합니다.
별개의 테이블을 삭제할 경우에는 인자값을 전달할 수 있습니다.

```php
$db->table()->drop("테이블명");
```

|예제코드| table-drop02.php

<br>

## 복수 테이블 삭제하기
---
여러개의 테이블을 한번에 삭제할 경우에는 배열 인자값을 전달 합니다.

```php
$db->table()->drop(["테이블1","테이블2"]);
```

배열 인자값이 전달되면 drop 메소드는 다음과 같은 쿼리를 생성하여 실행을 하게 됩니다.

```sql
DROP TABLES IF EXISTS 테이블1, 테이블2;
```
