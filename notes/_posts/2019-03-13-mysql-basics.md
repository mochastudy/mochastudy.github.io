---
layout: post
title: PHP 101 - MySQL 시작하기 
description: >
categories: notes
---

PHP와 함께 가장 많이 사용되는 데이터베이스 중 하나인 MySQL 설치법과 사용법 간단히 살펴보기.


## MySQL 시작
MySQL은 세계에서 가장 많이 쓰이는 오픈 소스 관계형 데이터베이스 관리 시스템이다.

## MYSQL 설치 및 실행하기
~~~
iMac:~ mocha$ brew install mysql // homebrew를 통해 mysql 설치하기
iMac:~ mocha$ mysql.server start // mysql 서버 구동하기
iMac:~ mocha$ mysql -uroot // mysql 시작
iMac:~ mocha$ mysql -uroot -ppassword // 비밀번호가 있으면 뒤에 -ppassword 추가
~~~

![데이터베이스](http://mocha.dothome.co.kr/images/190313-1.png)
mysql -uroot 명령어를 실행하면 위와 같이 'mysql>'가 뜬다.

### MySQL 종료하기
'ctr' + 'd'로 종료한다.

## MySQL 명령어
SQL은 PHP와는 다른 언어로 문법이 다르기 때문에 따로 공부해야 한다. 아래 자료들을 참고하여 시간 날때마다 틈틈히 보고 연습해두도록 하자.
* [TCPSchool](http://tcpschool.com/mysql/mysql_basic_syntax)
* [OpenTutorials](https://opentutorials.org/course/195)
* [HackerRank](https://www.hackerrank.com/domains/sql)
* [w3resource](https://www.w3resource.com/sql-exercises/)
* [w3schools](https://www.w3schools.com/sql/default.asp)
* [SQLBolt](https://sqlbolt.com/)
* [SQLZoo](https://sqlzoo.net/)
* [Codecademy](https://www.codecademy.com/learn/learn-sql)
* [Youtube - MySQL Beginner Tutorial](https://www.youtube.com/watch?v=nN4Kjdverzs&t=45s)

### 데이터베이스 목록 보기
~~~
mysql> show databases;
~~~

### 데이터베이스 생성하기
~~~
mysql> create database mytodo
~~~
데이터베이스는 테이블로 이루어져 있다. 테이블은 엑셀의 스프레드시트와 비슷한 개념. 위의 예시에서는 'mytodo'라는 이름의 데이터베이스를 생성한다.

### 데이터베이스 열기
~~~
mysql> use mytodo;
~~~
디렉토리(폴더)를 여는 것 같은 개념이라고 생각하면 된다. 

### 테이블 목록 보기
~~~
mysql> show tables;
~~~
데이터베이스를 처음 생성하면 테이블이 없어서 생성해야 한다.

### 테이블 생성하기
~~~
mysql> create table todos (description, completed); // Syntax 에러
mysql> create table todos (description text, completed boolean);
~~~
첫 번째 명령어에서 에러가 나는 이유는, description과 completed에 대해 어떤 데이터 형태를 사용할 것인지 입력하지 않았기 때문. 따라서, 두 번째 명령어에서는 description에는 text 타입, 그리고 completed에는 boolean 타입을 넣어줬다.

### 테이블 내용 보기
~~~
mysql> describe todos;
~~~
![테이블](http://mocha.dothome.co.kr/images/190313-2.png)
여기서 'Null' 값이 'yes'라는 것은, description과 completed의 값을 설정하지 않아도 된다는 것이다. 필수로 입력하는 값이 아니라는 것. 따라서, 테이블을 생성할 때 이 값까지 설정해주어야 한다.

### 테이블 지우기
~~~
mysql> drop table todos;
~~~

### 테이블에 Null 값 포함해서 생성하기
~~~
mysql> create table todos (description text NOT NULL, completed boolean NOT NULL);
~~~
![데이터베이스](http://mocha.dothome.co.kr/images/190313-3.png)

### id 설정하기
~~~
mysql> create table todos (id integer PRIMARY KEY AUTO_INCREMENT,description text NOT NULL, completed boolean NOT NULL);
~~~
id는 데이터에 대한 고유 번호로, 이 예시에서는 자동 증가(Auto Increment)하는 정수(integer) 형태이다. Description은 같은 내용으로 중복될 수 있어서 구분하기가 힘든데, 이를 구분 가능하게 하는 것이 ID Primary Key이다.
![테이블](http://mocha.dothome.co.kr/images/190313-4.png)


### 테이블에 데이터 추가하기
~~~
mysql> insert into todos (description, completed) values('포스팅 하기', false);
~~~

### 테이블 데이터 보기
~~~
mysql> select * from todos;
~~~
![데이터](http://mocha.dothome.co.kr/images/190313-5.png)


## MySQL GUI 툴
터미널에서 MySQL 명령어를 사용하다보면 아무래도 GUI 환경보다는 불편하고 번거로울 수 있다. 하지만, 명령어를 익혀두는 것도 도움이 되니, 후에 프로그램을 사용할거라면 터미널에서 명령어들을 충분히 연습해서 익히면 프로그램으로 넘어가도록 하자. 맥용 프로그램을 몇 가지 추리자면 아래와 같다.
* SequelPro
* Querious
* Navicat


## 간단 정리
~~~
mysql> show databases // 데이터베이스 목록
mysql> show tables // 테이블 목록 보기
mysql> use databases // 데이터베이스 선택
mysql> create table // 테이블 생성
mysql> drop table todos; // 테이블 삭제
mysql> insert into tablename // 테이블에 데이터 추가하기
~~~