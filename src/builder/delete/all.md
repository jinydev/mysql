---
layout: page
title: "delete all- SQL빌더"
keyword: "delete, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
    - "all"
---

# 전체삭제
---
테이블의 전체 데이터를 삭제합니다.

기본적으로 sql의 `DELETE` 쿼리는 검색조건을 지정하지 않는 경우, 테이블의 모든 데이터를 삭제하게 됩니다. 
이러한 실수를 방지하기 위해서 대부분 id값 또는 조건지정을 필수로 합니다.

빌더에서는 전체 데이터를 삭제할 수 있는 기능을 별도의 `all()` 메소드로 제공을 합니다.

```php
// RawSQL 데이터삭제
$delete = $db->delete("members4")->all();
```

<br>

## 예제코드
---

|예제코드| delete-all.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// RawSQL 데이터삭제
$delete = $db->delete("members4")->all();

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

