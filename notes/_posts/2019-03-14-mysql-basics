---
layout: post
title: PHP 101 - MySQL 시작하기 
description: >
categories: notes
---

Boolean과 조건문 알아보기.

## Boolean
~~~php
$task = [
    'title' =>  'PHP 공부하기',
    'due'   =>  '오늘',
    'assigned_to' => '모카',
    'completed' => false // Boolean 사용 (true/false)
]
~~~
이 코드에서는 'completed'에 false(Boolean)이 사용되었다. Boolean은 true와 false 두 가지이며, 반복문 등 다양하게 사용된다. 'yes'나 'no'를 사용하지 않는 이유는 둘 다 문자열이며 true 값을 가지고 있기 때문이다.

~~~php
<ul>
    <?php foreach($task as $heading => $value) : ?>
        <li>
            <strong><?= $heading; ?>: </strong> <?= $value; ?>
        </li>
    <?php endforeach ?>
</ul>
~~~

### 단어의 첫 번째 레터 대문자로 바꾸기
배열에서 직접 문자를 변경해도 되지만, 외부에서 가져온 데이터의 경우에는 직접 변경할 수 없다. 이럴때는 PHP의 여러 함수들을 유용하게 사용할 수 있다. 
~~~php
<strong><?= ucwords($heading); ?>: </strong> <?= $value; ?>
<?= ucwords('Hello my name is mocha'); ?> // Hello My Name Is Mocha
~~~

[ucwords](http://php.net/manual/en/function.ucwords.php)는 'Uppercase Words'를 줄인 것으로, 각 단어의 첫 번째 레터를 대문자로 바꿔주는 기능이다.

더 많은 PHP 함수에 대해 알고 싶다면, stackoverflow나 php.net 도큐멘트를 참고하면 된다. 모든 함수를 다 알고 있어야 하는건 아니지만, 자주 쓰이는 것은 어느정도 익혀두는 것이 좋다.

### Ke 부분을 좀 더 상세하게 출력하기
위에서 본 것과 같이 키와 값을 모두 반복문을 사용해서 출력해도 되지만, 키를 다르게 입력하고자 하는 경우에는 HTML과 PHP를 섞어서 사용하면 데이터를 조금 더 자유롭게 커스터마이즈 할 수 있다.

~~~php
<ul>
    <li><strong>Name: </strong> <?= $task['title']; ?></li>
    <li><strong>Due Date: </strong> <?= $task['due']; ?></li>
    <li><strong>Person Responsible: </strong> <?= $task['assigned_to']; ?></li>
    <li><strong>Status: </strong> <?= $task['completed']; ?></li>
</ul>
~~~
이 코드에서 마지막 줄 'Status: ' 부분은 값이 출력되지 않는데, 값을 출력하기 위해 아래와 같이 삼항 연산자(Ternary Operator)를 사용해서 조건을 추가해보자.
~~~
<?= $task['completed'] ? '완료' : '미완료';>
~~~
앞 부분의 조건을 만족한다면 '완료'가 출력되고, 만족하지 않는다면 '미완료' 출력.

## 조건문 (Conditionals)
위에서 삼항 연산자를 사용한 조건문을 살펴봤는데, 기본적인 조건문의 모양은 아래와 같다.
~~~php
if (조건) {

} else {

}
~~~

~~~php
if ($task['completed']) {
    echo '완료'; // 값이 true면 '완료' 출력
} else {
    echo '미완료'; // 값이 false면 '미완료' 출력
}
~~~
기본적인 조건문으로 다시 작성한 코드. 더 복잡한 코드라면 이 방법을 사용하지만, 간단한 문자열을 출력할 때는 삼항 연산자를 사용하면 코드가 더 간결해진다.

~~~php
<?php if ($task['completed']) : ?>
    <span class="icon">&#9989;</span>
<?php else : ?>
    <span class="icon">Incomplete</span>
<?php endif; ?>
~~~
foreach문과 마찬가지로 if문도 이런 식으로 작성할 수도 있음.

### 값이 거짓인지 확인하기
조건문에서 값이 거짓인지 확인하려면 '!(느낌표)'를 사용하면 된다. 
~~~php
if (!true) {
    echo 'Incomplete';
}

if (!$task['completed']) {
    echo 'Incomplete';
}
~~~

## 함수 (Functions)
지금까지의 강의에서 htmlspecialchars(), ucwords() 등 몇 가지 함수를 알아보고 PHP.NET의 doc에서 함수 리스트 또한 살펴봤다. 이미 PHP에 내장된 함수도 있지만, 직접 함수를 만들 수도 있다.

$animals = ['dog', 'cat'];
~~~php
echo '<pre>';
die(print_r($animals));
echo '</pre>';
~~~
위의 print_r과 die는 배열을 가공할 때 자주 사용되는데, 테스트 할 때마다 일일이 치려면 번거롭기 때문에 function으로 만들어서 사용하면 간편하다.

### 함수 선언하기
~~~php
require 'functions.php'; // functions 파일을 분리했다면 사용
$animals = ['dog', 'cat'];

function dd($val) {
    echo '<pre>';
    die(print_r($one, $two, $three));
    echo '</pre>';
}

dd($animals);
~~~
dd는 die & dump의 약자로 흔히 쓰인다. $val은 어떤 이름을 넣어도 괜찮지만, 되도록이면 상황에 맞는 변수를 사용하면 코드를 읽기가 더 쉬워진다.

