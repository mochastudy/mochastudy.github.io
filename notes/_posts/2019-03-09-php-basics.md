---
layout: post
title: PHP Basics - PHP 설치 및 기초 문법 
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
php 파일의 확장자는 '.php'

### 화면에 출력하기
~~~php
echo 'Hello World'
~~~
* PHP 코드는 '<?php'로 시작해야 한다. 내용이 100% PHP로만 이루어진 파일이면 굳이 '?>'로 닫아주지 않아도 되지만, 다른 언어와 섞여있다면 PHP 부분을 닫아주어야 한다.
* 모든 명령어는 ';'로 마친다.
* 문자열은 '' 또는 ""로 감싸준다.


### 변수
변수를 선언하기 위해서는 변수명 앞에 '$'를 붙인다.
~~~php
$greeting = 'Hello World';
echo $greeting; // Hello World
~~~

주의할 점은, '' 안에는 변수를 포함할 수 없지만 "" 안에는 변수를 포함할 수 있다.
~~~php
$name = 'Mocha';
echo 'Hello, $name'; // Hello $name
echo "Hello, $name"; // Hello Mocha
echo 'Hello, ' . $name; // Hello Mocha
echo "Hello, {$name)"; // Hello Mocha
~~~

### php와 html 함께 사용하기
PHP는 웹프로그래밍 언어이기 때문에 HTML과 함께 사용된다.
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

### 쿼리
'localhost:8888?name=mocha'에서 order은 '키', name은 '값'이다. $_GET['name']을 사용하면 주소의 쿼리 부분이 바뀌는대로 그 값을 불러올 수 있으며, 아래와 같이 화면에 출력되는 부분도 실시간으로 바뀐다.

~~~html
<header>
    <h1>
        <?php 
            $name = $_GET['name']; // Mocha
            echo "Hello, $name";
        ?>
    </h1>

    <h1><?php echo "Hello, $_GET['name']; ?></h1>
    <?= "Hello, $_GET['name']; ?>
        <?= "Hello, htmlspecialchars($_GET['name']); ?>
</header>
~~~


### 보안 문제
'localhost:8888/?name=<a href="https://google.com">Mocha</a>'
주소에 태그를 삽입하면 페이지에도 태그가 반영된다. 위의 경우, 화면에 출력되는 'Mocha'에 구글 링크가 걸리게 된다. 사이트의 이용자가 이를 스크립팅으로 악용할 수 있는데, htmlspecialchars라는 function을 사용하면 문자들을 HTML 엔티티로 변환해준다.

### 코드 분리하기
코드가 길어지면 HTML과 PHP 구분이 힘들어질 수 있으므로, 이 언어들을 최대한 분리하는 것이 좋다. 파일은 데이터 생성을 위한 index.php와 화면에 렌더링 하기 위한 index.view.php(이름은 마음대로 지어도 됨)로 나눌 수 있으며 렌더링을 위한 파일은 뷰 또는 템플릿으로 불린다.
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