---
layout: page
title: "update builder inc- SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
    - "object"
    - "inc"
---

## inc
---
컬럼타입이 int형인경우 일정 단위로 값을 증가할 수 있습니다.

```php
// 숫자증가
$db->update("members3")->inc("click")->id(1);
```

id=1 인 row의 click 필드값을 `+1` 증가합니다.
만일 다른 값을 증가하고자 할때에는 두번째 인자에 증가값을 설정합니다.

```php
// 숫자증가
$db->update("members3")->inc("click", 10)->id(1);
```

`+10`씩 값을 증가합니다.