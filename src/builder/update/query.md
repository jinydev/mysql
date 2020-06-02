---
layout: page
title: "update builder query- SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
    - "object"
    - "query"
---

# Query 설정
---
빌더는 자동적으로 쿼리를 생성하고 동작을 수행합니다. 하지만, 내부적 쿼리빌더를 사용하지 않고 직접 쿼리를 설정하여 실행을 할 수 있습니다.  

<br>

## setQuery
---
빌더에게 직접 쿼리를 설정합니다.

```php
->setQuery("SQL쿼리");
```

<br>

## clearQuery
---
내부 설정되어 있는 쿼리를 초기화 합니다.

```php
->clearQuery();
```

<br>

## getQuery
---
설정된 쿼리값을 읽어 옵니다.

```php
->getQuery();
```