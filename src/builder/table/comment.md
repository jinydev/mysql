---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "Table"
---

# 테이블 코멘트
---
테이블 코멘드를 작성합니다.

<br>

## comment()
---
테이블의 설명문구를 설정합니다.

```php
$db->table("members2")->comment("Hello");
```

|예제코드|
table-comment01.php

<br>

## getComment()
---
선택한 테이블의 코멘트 정보를 출력합니다.

```php
$db->table("members2")->getComment();
```

만일 테이블이 선택되지 않는 경우, 모든 테이블의 코멘트가 출력됩니다.

|예제코드|
table-comment02.php
