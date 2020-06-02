---
layout: page
title: "delete id- SQL빌더"
keyword: "delete, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
    - "id"
---

# 특정 id 삭제
---
테이블은 고유의 primaryKey인 id값을 가지고 있습니다. 고유한 id값을 이용하여 데이터를 삭제할 수 있습니다. 

특정 id값을 가지는 테이블을 삭제할 경우 다음과 같이 `id()` 메소드를 호출합니다.

```php
$delete = $db->delete("members4");
$delete->id(22); //22번 id를 삭제합니다.
```

<br>

## 예제코드
---
실습 예제 코드를 통하여 데이터를 삭제해 보도록 하겠습니다.

|예제코드| delete-id.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

$delete = $db->delete("members4");
$delete->id(3); // 삭제할 id

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