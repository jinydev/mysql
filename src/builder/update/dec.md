---
layout: page
title: "update builder dec- SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
    - "object"
    - "dec"
---

## dec
---
컬럼타입이 int형인경우 일정 단위로 값을 감소할 수 있습니다.

```php
// 숫자증가
$db->update("members3")->dec("click")->id(1);
```

id=1 인 row의 click 필드값을 `-1` 감소합니다.
만일 다른 값을 감소하고자 할때에는 두번째 인자에 값을 설정합니다.

```php
// 숫자증가
$db->update("members3")->dec("click", 3)->id(1);
```

`-3`씩 값을 감소합니다.