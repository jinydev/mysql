---
layout: page
title: "Prepared"
---

# Prepared
---
웹과 같이 외부와 공개된 상태에서 데이터 값을 입력받아 삽입 쿼리를 생성을 하는 것은 다소 위험할 수 있습니다. 악의적인 사용자는 데이터의 입력에 SQL쿼리 오류를 발생할 수 있는 코드를 삽입하여 해킹을 시도할 수 있습니다.  

MySQLi는 이러한 안전한 쿼리를 생성할 수 있도록 Prepared라는 SQL 인젝션 공격을 대비할 수 있는 메서드를 제공합니다. prepared 메서드 기능을 사용하기 위해서는 쿼리 의 문장을 생성하는 prepared와 테이터를 연결하는 Bound 매개변수로 구성됩니다.  

또한 한 번 설정한 prepared 기능은 유사한 SQL문을 반복적으로 재사용할 수 있습니다. SQL 쿼리의 오류 및 코드를 효율적으로 작성할 수 있습니다.  

예제 파일 | prepared.php 
```php
<?php
	$servername = "localhost";
	$username = "username";
	$password = "password";
	$dbname = "myDB";

	// Create connection
	$conn = new mysqli($servername, $username, $password, $dbname);

	// Check connection
	if ($conn->connect_error) {
		die("Connection failed: " . $conn->connect_error);
 	}

	// prepare and bind
	$stmt = $conn->prepare("INSERT INTO members (firstname, lastname, email) VALUES (?, ?, ?)");
	$stmt->bind_param("sss", $firstname, $lastname, $email);

	// set parameters and execute
	// 데이터1
	$firstname = "jiny";
	$lastname = "lee";
	$email = "jiny@jinyphp.com";
	$stmt->execute();

	// 데이터2
	$firstname = "hojin";
	$lastname = "lee";
	$email = "hojin@jinyphp.com";
	$stmt->execute();

	$stmt->close();
	$conn->close();
?> 

```

위의 예제에서 데이터 삽입을 위한 기본 쿼리를 생성합니다. 쿼리는 다음과 같습니다.  

```sql
INSERT INTO members (firstname, lastname, email) VALUES (?, ?, ?)
```

쿼리에는 이상한 물음표 (?) 기호가 들어 있습니다. 물음표 기호는 인젝션 공격을 대비하고 실제적인 데이터가 들어가는 자리입니다. 물음표는 정수, 문자열 등 다양한 데이터로 대 체될 수 있습니다.  

prepare를 통하여 쿼리 설정이 되었다면 두 번째로 실제적인 데이터가 들어가는 바인딩 설정을 합니다. bind_param() 함수는 다음과 같이 설정됩니다.  

```php
$stmt->bind_param("sss", $firstname, $lastname, $email); 
```

첫 번째 인자로는 바인딩 데이터의 데이터 타입을 설정합니다. 그 뒤에 바인딩되는 데이 터들을 매개변수 인자로 전달합니다.  

바인딩 함수의 데이터 타입은 약자를 이용하여 사용합니다. 인수 `sss`는 바인딩되는 데이 터의 타입을 지정하는 것입니다. 위의 세 가지 데이터 모두 스트링이기 때문에 sss로 지정 합니다. 바인딩 데이터 타입은 네 가지가 있습니다.  

* i -integer 
* d -double 
* s -string 
* b -BLOB 

