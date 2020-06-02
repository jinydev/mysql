---
layout: page
title: "update builder execute - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
    - "object"
    - "execute"
---

# 실행
---
빌더를 통하여 자동생성된 쿼리를 실행합니다.

<br>

## id 선택
---
update 쿼리의 단점은 조건과 일치하는 모든 데이터를 갱신하게 됩니다. 잘못 실수로 자신이 원하지 않는 데이터 까지 수정을 하게 됩니다.
이를 방지하기 위해서 id를 선택하여 해당 row 데이터만 수정을 하게 합니다.

이를 처리하기 위해서 `id()` 메소드를 제공합니다.

```php
uptate("members", ['firstname'=>"1234"])->id(5);
```

쿼리빌더로 설정된 값을 id=5인 조건으로 쿼리를 실행하게 됩니다.

<br>

### id 갱신작업
---
update 예제코드를 통하여 데이터를 갱신해 보도록 합니다.

|예제코드| update-03.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터갱신
$db->update("members4")->setFields(['firstname'=>"1234"])->id(5);

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

## all
---
전체 데이터를 갱신합니다.

```php
->all();
```