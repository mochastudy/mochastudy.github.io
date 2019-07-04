---
layout: post
title: Lesson 3 - PHP 기초 문법 (변수와 if문) 
categories: project2
---

이 강의에서는 변수의 정의와 PHP에서 변수 선언하는 방법, 그리고 if문에 대해 알아본다.

## 변수와 상수를 선언하는 이유?
~~~php
<?php
	$mocha = '모카';
	$latte = '안녕하세요.';
	
	echo $latte . '저는 ' . $mocha . '입니다 - ' . $mocha;
?>
~~~
* 어떠한 데이터를 반복해서 사용해야 할 때, 변수 이름만 불러내면 언제든지 그 속의 값을 계속 재활용해서 사용할 수 있다.
* 변수명은 내가 기억하기 편한 것으로!

### 변수 선언
PHP에서는 변수명 앞에 $(달러)를 붙여서 선언한다.
~~~php
$mocha = 1; // $mocha가 1이라는 뜻이 아니라, 1을 $mocha라는 변수에 담아둔다는 뜻
~~~

~~~php
<?php
	$mocha = 1;
	$mocha = $mocha + 1; // 2
	$latte = 2;
	echo $mocha + $latte; // 4
?>
~~~

~~~php
<?php
	$mocha = 1;
	echo $mocha . '<br>'; // 1
	$mocha = $mocha + 1;
	echo $mocha . '<br>'; // 2
	$latte = 2;
	echo $mocha + $latte; // 4
?>
~~~

변수는 '변하는 수'이므로, 그 속에 담긴 값을 얼마든지 다시 선언해서 변경할 수 있다. 

### 상수 선언
* 상수는 변하지 않는 수(값)이다. PHP에서는 'const'를 사용. (const $변수명 = 1;
* 이 변수에 들어 있는 값은 고정 된 값으로, 다시 assign하려고 하면 에러가 나게 됨.
* 참고 자료: [PHP.NET - 상수](http://php.net/manual/kr/language.constants.php "PHP")



## if문 구조
~~~php
<?php
	if (조건식이 참이면) {
		// 여기에 있는 내용이 실행 됨
	} else {
		// 조건식이 거짓(조건이 만족되지 않으면)이면 여기에 있는 내용이 실행 됨
?>
~~~
~~~php
	$num1 = 1;
	$num2 = 2;
	
	if ($num == $num2) {
		echo '값이 일치합니다.';
	} else {
		echo '일치 하지 않습니다.';
	}
?>
~~~
이 예시에서는 $num1과 $num2가 다른 값이므로 '일치하지 않습니다'가 출력된다.

#### 기억해둬야 할 것!
* A == B // A와 B는 같다.
* A !== B // A와 B는 같지 않다.
* A > B // A가 B보다 크다.
* A < B // A가 B보다 작다.
* A >= B // A가 B보다 크거나 작다.
