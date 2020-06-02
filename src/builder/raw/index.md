---
layout: page
title: "SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
--- 

# query 설정 및 실행하기
---
빌더 connection에 raw쿼리를 별도로 설정하고 실행을 할 수 있습니다.

```php
$query = "SHOW DATABASES";
$db->setQuery($query);
```

`setQuery`는 쿼리를 실행가능한 준비상태를 설정합니다. 

<br>

## 설정된 쿼리 실행하기
---
설정된 쿼리를 실행하기 위해서는 별도의 `run`메소드를 실행하여야 합니다.

```php
$db->run();
```

<br>

## bind 설정
---
설정된 쿼리에 값을 바인드 해야 되는 경우 setBind 메소드를 실행합니다.  

```php
$data = [
    'firstname' => "이", 
    'lastname' => "호진"
];
$stmt = $db->setBinds($data);
```

설정한 bind된 쿼리를 실행합니다.

```php
$db->run();
```
예제코드 ./sample/sql/raw-bind01.php

또는 run() 메소드의 인자값으로 bind를 처리 할 수 있습니다.

```php
// bind 데이터삽입
$query = "INSERT `db2020`.`members4` SET firstname=:firstname, lastname=:lastname;";
$db->setQuery($query);

$data = [
    'firstname' => "이", 
    'lastname' => "호진"
];
$db->run($data);
```

예제코드 ./sample/sql/raw-bind02.php


