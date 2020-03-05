---
layout: page
title: "02.2.콘솔"
---  
대부분의 DBMS는 서버형으로 클라이언트와 연동하여 동작하게 됩니다. 하지만 데이터 를 조작하기 위해서 처음부터 프로그램을 개발하기에는 어렵습니다.  

MySQL은 기본적으로 직접 데이터의 조작 명령을 입력하고 실행할 수 있도록 콘솔 입력 모드를 제공합니다. 콘솔 입력 모드를 이용하여 SQL 명령을 입력하고 데이터 조작 명령 을 실행하게 됩니다.  

## 02.2.1 접속 
MySQL의 콜솔 명령을 입력하기 위해서는 터미널 창에서 mysql을 실행해야 합니다. 먼 저 운영체제에서 터미널 창을 실행합니다. 실행 후 mysql이 설치된 경로를 찾아서 이동 합니다. 대부분 mysql 실행 프로그램은 ~경로\mysql\bin 폴더 안에 위치해 있습니다.  

터미널 창에서 mysql 실행 파일로 데이터베이스를 실행합니다. 다음과 같이 입력하면 mysql을 실행할 수 있습니다.  

|명령| 
```sql
mysql -u계정명 -p 
```

|터미널 화면| 
```bash
C:\Bitnami\wampstack-5.6.30-0\mysql\bin>mysql -uroot -p
Enter password: ********
```
터미널에서 mysql 명령을 입력하면 이전에 설정한 패스워드를 물어보게 됩니다. 설정한 패스워드를 정확히 입력합니다.  

계정과 패스워드가 일치하면 다음과 같이 성공 화면이 출력됩니다. 

| 콘솔 실습 화면 | 
```sql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.6.35 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

`mysql>` 프롬프트가 뜨면 실행이 성공한 것입니다. 이곳에 SQL 조작 명령을 입력하면 데이터베이스는 작업을 하여 결과를 화면에 출력할 것입니다.  

또는 패스워드를 바로 같이 
입력하여 접속할 수도 있습니다.  

|명령| 
```sql
mysql -u 계정명 -p패스워드 
```

여기서 주의할 점은 -p와 패스워드 사이는 공백이 들어가면 안 됩니다. 하지만 -u와 계 정명 사이에는 공백을 추가해도 됩니다.  

보다 자세한 mysql의 사용법은 --help 옵션으로 상세하게 사용법을 알아볼 수 있습 니다.  

## 02.2.2 종료 
콘솔을 통하여 모든 데이터 작업이 완료하면 실행된 mysql 프로그램을 종료해야 합니다. 
콘솔 접속 종료는 exit 명령어를 입력하면 됩니다. 

|콘솔| 
```
mysql> exit
Bye
C:\Bitnami\wampstack-5.6.30-0\mysql\bin>
```

exit는 MySQL 접속 콘솔을 종료하는 것입니다. 콘솔을 실행시킨 윈도우 커맨드 창 또는 리눅스/맥의 터미널 창과는 다릅니다.  

## 02.2.3 포트 
MySQL은 기본적으로 3306 포트를 이용합니다. 만일 설치할 때 포트번호를 변경했을 경 우 mysql 접속 시 포트명도 같이 입력해야 합니다. 

