---
layout: post
title: 190312 - PHP Basics
description: >
image: 
categories: notes
---

PHP 설치, 구동 방법과 기초 문법에 대해 알아보기.

## PHP 설치 (Mac OS X)
Mac OS에 PHP 환경을 구성하는 방법은 여러가지가 있다.
1. Homebrew 설치 후, 터미널에서 PHP 패키지를 찾아서 설치
2. MAMP(Macintosh, Apache, MySQL, PHP)를 설치

### 설치된 PHP 버전 확인
시스템에 설치된 PHP의 버전을 확인하려면 터미널에서 'php -v'를 입력.

### 서버 구동하기
PHP 서버를 구동하려면 MAMP를 실행하거나, 터미널에서 'cd'를 사용해서 해당 디렉토리로 이동 후, 'php -S localhost:8888'를 입력한다. (모든 php 명령어를 보려면 php -h)


## PHP 시작
php 파일은 .php 확장자를 추가해야 함.

### 화면에 출력하기
~~~php
echo 'Hello World'
~~~
<?php로 시작해야 함.
100% php로 이루어진 파일이면 ?>로 닫아주지 않아도 된다. (good practice)
하지만 php로 끝나는 파일이 아니면 ?>로 닫아주어야 함.

echo 화면 출력
string(문자열)은 '', ""로 감싼다
모든 명령어는 ;로 끝낸다.


## 변수
변수를 선언하는 방법은 $을 붙이고 
~~~php
$greeting = 'Hello World';
echo $greeting; // Hello World
~~~


~~~php
$name = 'Mocha';
echo 'Hello, $name'; // Hello $name
echo "Hello, $name"; // Hello Mocha
echo 'Hello, ' . $name; // Hello Mocha
echo "Hello, {$name)"; // Hello Mocha
~~~
''에는 변수를 넣을 수 없음
""에는 변수를 넣을 수 있음

## php와 html 함께 사용하기
php는 웹 프로그래밍 언어이기 때문에 html과 함께 사용된다.

~~~html
<header>
    <h1>
        <?php 
            $greeting = "Hello World';
            echo $greeting;
        ?>
    </h1>
</header>
~~~

localhost:8888?order=name
order은 키, name은 값
~~~html
<header>
    <h1>
        <?php 
            $name = $_GET['name']; // Jeff
            echo "Hello, $name";
        ?>
    </h1>

    <h1><?php echo "Hello, $_GET['name']; ?></h1>
    <?= "Hello, $_GET['name']; ?>
        <?= "Hello, htmlspecialchars($_GET['name']); ?>

</header>
~~~
주소 부분에 있는 이름을 바꾸면 echo 되는 내용도 같이 바뀜

보안 문제
localhost:8888/?name=<a href="https://google.com">Mocha</a> 
이런식으로 삽입하게 되면 페이지에도 반영이 된다.
따라서, htmlspecialchars라는 function을 사용하게 된다.
사용하면 html이 반영이 되는게 아니라 html entity로 변환하여 넣은 그대로를 화면에 출력한다.

Separation of Concerns
코드가 길어지면 복잡해지므로 PHP와 HTML을 목적에 따라 최대한 분리하는 것이 좋음.
데이터 생성 파일과 화면에 출력하기 위한 html 파일
index.view.php / index.tmpl.php (어떤 이름도 좋지만 be consistent!) 뷰또는 템플릿이라고 부름

~~~php
<?php
    $greeting = 'Hello, World';
    require 'index.view.php';
~~~
~~~html
<header>
    <h1><?= $greeting ?></h1>
</header>
~~~

데이터를 위한 파일 하나와, 그 데이터를 화면에 렌더링 하는 파일 하나로 나뉘어짐
