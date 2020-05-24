---
layout: page
title: "connection - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "connection"
--- 

# 데이터베이스 연결
---
데이터베이스 접속을 하는 방법에 대해서 설명을 합니다.  

<br>

## 드라이버
---
`jinydb`는 `PDO` 방식을 응용하여 데이터베이스에 접속을 합니다.  
PHP에서 PDO에 접속을 하기 위해서는 PDO 드라이버 활성화 해주어야 합니다. 
php.ini 파일, 912 라인줄 근처에서 다음과 같이 주석(`;`)을 제거합니다.   

```
extension=php_pdo_mysql.dll
```

드라이버가 활성화 되지 않으면, 코드에서 다음과 같은 오류를 출력 합니다.

```php
if (extension_loaded("PDO") && extension_loaded("pdo_mysql")) {
    // 접속코드
    // ...      
} else {
    echo "PDO 드라이버가 활성화 되어 있지 않습니다.\n";
    exit(1); // 오류 종료
}
```

<br>

## 초기화 방법1 : 메서드
---
`Connection` 객체의 메소드를 통하여 데이터 접속 정보를 설정할 수 있습니다.

예제코드: samples/conn/conn-01.php
```php
<?php
require "../../loading.php"; // 오토로딩

$db = new \Jiny\Mysql\Connection();

// 메서드 체인으로 DB정보 설정
$db->setUser("db2020");
$db->setPassword("123456");
$db->setSchema("db2020");
$db->setCharset();
$db->setHost(); // 기본값 사용

// 데이터베이스 연결
$conn = $db->connect();
if ($conn) {
    echo "데이터베이스 접속 성공\n";
} else {
    echo "데이터베이스 접속 실패\n";
}
```

<br>

## 초기화 방법2 : 메서드 체인
---
`Connection` 객체의 setter 메소드는 `$this`를 반환함으로써 메서드 체인 연결을 통하여 DB접속 정보를 설정할 수 있습니다.

예제코드: samples/conn/conn-02.php
```php
<?php
require "../../loading.php"; // 오토로딩

$db = new \Jiny\Mysql\Connection();

// 메서드 체인으로 DB정보 설정
$db->setUser("db2020")->setPassword("123456")->setSchema("db2020")->setCharset()->setHost(); // 기본값 사용

// 데이터베이스 연결
$conn = $db->connect();
if ($conn) {
    echo "데이터베이스 접속 성공\n";
} else {
    echo "데이터베이스 접속 실패\n";
}
```

<br>

## 초기화 방법2
---
초기화1 및 2방법은 소스코드상에서 직접 DB설정값을 입력하는 방법으로 접속을 하였습니다.  
DB접속 정보를 외부 파일로 분리하여 데이터베이스 접속을 처리할 수 있습니다.

별도의 설정파일을 만듭니다.

예제코드: samples/dbinfo.php
```php
<?php
return [
    'user'=>"db2020",
    'password'=>"123456",
    'schema'=>"shop",
    'host'=>"localhost",
    'charset'=>"utf8"
];
```

설정파일은 연상배열 형태로 DB접속 정보를 작성하여 전달 합니다. 또한, 베열값은 return 구문을 통하여 반환됩니다.
이렇게 분리된 php 설정파일은 include 구문을 통하여 값을 읽어 올 수 있습니다.

```php
// 데이터베이스 설정값
$dbinfo = include("../dbinfo.php");
```

이를 이용하여 데이터베이스 접속을 처리하는 코드 예제는 다음과 같습니다.

예제코드: samples/conn/conn-03.php
```php
<?php
require "../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = include("../dbinfo.php");

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터베이스 연결
$conn = $db->connect();
```

<br>

## 헬퍼함수
---
DB설정파일은 외부의 php파일입니다. db설정파일을 보다 쉽게 읽어올 수 있도록 별도의 헬퍼함수를 제공합니다.
> 헬퍼 함수는 `src/Helpers/Helper.php`에 선언이 되어 있습니다.

`dbinfo()` 헬퍼함수는 배열을 반환하는 php파일을 include하여 값을 반환합니다. 인자로 `파일명`을 전달합니다. 

```php
if (!function_exists("dbinfo")) {
    function dbinfo($path="../dbinfo.php")
    {       
        return include($path);
    }
}
```

함수의 인자값이 없는 경우 초기값으로 `상위`디렉토리의 `dbinfo.php`을 읽어 옵니다.

헬퍼함수를 통한 DB접속 처리를 실습해 보도록 합니다.

```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 데이터베이스 연결
$conn = $db->connect();
if ($conn) {
    echo "데이터베이스 접속 성공\n";
} else {
    echo "데이터베이스 접속 실패\n";
}
```
