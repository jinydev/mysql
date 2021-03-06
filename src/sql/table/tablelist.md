---
layout: page
title: "Table LIST - learn Mysql | JinyDev"
keyword: "coulumes, table, sql"
description: "테이블 리스트를 확인합니다."
breadcrumb:
    - "sql"
    - "table"
    - "list"
--- 

# 테이블 리스트
---
1개의 데이터베이스 이름 그룹 안에는 다수의 테이블을 포함하고 있습니다. 데이터베이 스 안에 있는 테이블의 목록을 SQL 명령을 통해서 확인할 수 있습니다.  

<br>

## 테이블 목록 
---
현재 선택된 데이터베이스 이름 그룹 안에 들어 있는 모든 테이블명을 출력합니다. 실행 명령은 `SHOW TABLES;`입니다. 

| 쿼리 문법 | 
```sql
SHOW TABLES;
```

| 콘솔 실습 화면 | 
```sql
mysql> show tables;
+----------------+
| Tables_in_jiny |
+----------------+
| members        |
+----------------+
1 row in set (0.00 sec) 
```

위와 같이 콘솔로 확인해 보면 생성된 테이블의 목록을 확인할 수 있습니다.  

<br>

## 목록 출력 
---
PHP를 통하여 데이터베이스명 그룹 안에 있는 테이블의 목록을 출력하도록 하겠습니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 
```php
// 데이터베이스 목록을 읽어 옵니다
public function showTables()
{
            $queryString = "show tables";
            $this->msgEcho($queryString);

            if ($result = mysqli_query($this->dbcon, $queryString)) {
                $rowss = "";
                $row_cnt = mysqli_num_rows($result);
                for ($i=0;$i<$row_cnt;$i++) {
                    $rowss[$i] = mysqli_fetch_object($result);
                }

                $result->free();
                return $rowss;
            } 
}
```

예제 파일 | sql-12.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 현재 데이터베이스 이름을 확인합니다.
	$dbname = $db->currentDatabase();
	echo "현재 데이터베이스 = ". $dbname . "<br>";
	$key = "Tables_in_".$dbname;

	if($rowss = $db->showTables()){
		echo "tables Count = ". count($rowss) . "<br>";

		for($i=0;$i<count($rowss);$i++){
			echo $i."=";            
			echo $rowss[$i]->$key;
			echo "<br>";

			print_r($rowss[$i]);
			echo "<br>";
		}
	}    

?>

```

화면 출력 
```
mysql connected!
SELECT DATABASE()
현재 데이터베이스 = jiny
show tables
tables Count = 5
0=members
stdClass Object ( [Tables_in_jiny] => members )
1=members1
stdClass Object ( [Tables_in_jiny] => members1 )
2=members5
stdClass Object ( [Tables_in_jiny] => members5 )
3=orders1
stdClass Object ( [Tables_in_jiny] => orders1 )
4=products
stdClass Object ( [Tables_in_jiny] => products ) 

```

<br>

## 테이블 상세 정보 
---
SHOW TABLES 명령은 데이터베이스의 테이블의 이름 목록을 출력합니다. 각각의 테이 블의 상세한 정보를 알고 싶을 경우에는 뒤에 STATUS 명령을 함께 사용합니다.  

| 쿼리 문법 | 
```sql
SHOW TABLE STATUS; 
```

`SHOW TABLE STATUS;` 쿼리 명령은 테이블 목록과 더불어 테이블의 상세 정보도 같 이 출력합니다.  

| 콘솔 실습 화면 | 
```sql
mysql> show table status;
+-------------+--------+---------+------------+------+----------------+-------------+-----------------+--------------+-----------+----------------+---------------------+---------------------+---------------------+-----------------+----------+--------------------+---------+
| Name        | Engine | Version | Row_format | Rows | Avg_row_length | Data_length | Max_data_length | Index_length | Data_free | Auto_increment | Create_time         | Update_time         | Check_time          | Collation       | Checksum | Create_options     | Comment |
+-------------+--------+---------+------------+------+----------------+-------------+-----------------+--------------+-----------+----------------+---------------------+---------------------+---------------------+-----------------+----------+--------------------+---------+
| board       | InnoDB |      10 | Compact    |    2 |           8192 |       16384 |               0 |            0 |         0 |              7 | 2017-06-11 15:07:15 | NULL                | NULL                | utf8_general_ci |     NULL |                    |         |
| mem_view    | NULL   |    NULL | NULL       | NULL |           NULL |        NULL |            NULL |         NULL |      NULL |           NULL | NULL                | NULL                | NULL                | NULL            |     NULL | NULL               | VIEW    |
| members     | MyISAM |      10 | Dynamic    |    7 |             45 |         316 | 281474976710655 |         2048 |         0 |            101 | 2017-06-07 17:26:47 | 2017-06-07 17:27:46 | 2017-06-11 14:47:08 | utf8_general_ci |     NULL |                    |         |
| members1    | MyISAM |      10 | Dynamic    |   19 |             23 |         448 | 281474976710655 |         2048 |         0 |             20 | 2017-06-01 14:53:34 | 2017-06-06 18:03:45 | NULL                | utf8_general_ci |     NULL | row_format=DYNAMIC |         |
| members3    | MyISAM |      10 | Dynamic    |    0 |              0 |           0 | 281474976710655 |         1024 |         0 |              8 | 2017-06-06 18:55:10 | 2017-06-06 18:55:10 | NULL                | utf8_general_ci |     NULL | row_format=DYNAMIC |         |
| members_1   | MyISAM |      10 | Dynamic    |    6 |             48 |         288 | 281474976710655 |         2048 |         0 |              8 | 2017-06-01 23:55:05 | 2017-06-02 00:20:22 | NULL                | utf8_general_ci |     NULL |                    |         |
| members_all | InnoDB |      10 | Compact    |    0 |              0 |       16384 |               0 |            0 |         0 |           NULL | 2017-06-02 16:59:01 | NULL                | NULL                | utf8_general_ci |     NULL |                    |         |
| orders      | InnoDB |      10 | Compact    |   10 |           1638 |       16384 |               0 |            0 |         0 |             11 | 2017-05-22 15:33:25 | NULL                | NULL                | utf8_general_ci |     NULL |                    |         |
| products    | InnoDB |      10 | Compact    |    2 |           8192 |       16384 |               0 |            0 |         0 |              4 | 2017-05-21 12:50:22 | NULL                | NULL                | utf8_general_ci |     NULL |                    |         |
+-------------+--------+---------+------------+------+----------------+-------------+-----------------+--------------+-----------+----------------+---------------------+---------------------+---------------------+-----------------+----------+--------------------+---------+
9 rows in set (0.06 sec)
```

목록과 출력되는 테이블의 상세 정보는 다음과 같습니다.  
* Name 
* Engine 
* Version 
* Row_format 
* Rows 
* Avg_row_length 
* Data_length 
* Max_data_length 
* Index_length 
* Data_free 
* Auto_increment 
* Create_time 
* Update_time 
* Check_time 
* Collation 
* Checksum 
* Create_options 
* Comment 

또는 셸 명령창에서 `mysqlshow -- status` DB명으로 확인할 수도 있습니다.  

| 터미널 화면 | 
```
C:\Bitnami\wampstack-5.6.30-0\mysql\bin>mysqlshow -u root -p --status jiny
Enter password: ********
Database: jiny
…….
…….
C:\Bitnami\wampstack-5.6.30-0\mysql\bin>
```

셸 명령을 이용하면 직접 콘솔로 접속하여 SQL 쿼리 명령을 실행하지 않아도 되는 편리함이 있습니다.  