---
layout: post
title: PHP Basics - Booleans
description: >
image: 
categories: notes
---

기본 배열과 연관 배열의 구조와 사용 방법 등에 대해 알아보기.

## 배열

배열을 선언하는 방법은 변수를 선언하는 방법과 비슷하다. 하지만, 등호의 우편에 '[]'를 추가하게 되는 것이 다르다.
~~~php
$names = []; // 빈 배열 (Empty array)
$cafes = [
    'Starbucks',
    'Second Cup',
    'Tim Hortons'
]
~~~

### 배열을 쓰는 이유?
~~~php
$cafeOne = 'Starbucks';
$cafeTwo = 'Second Cup';
$cafeThree = 'Tim Hortons'
~~~
주어진 데이터를 위와 같이 변수 선언해도 되지만, 매번 새로운 데이터를 추가하기 위해 변수를 새로 생성하는 것은 비효율적이며 코드만 쓸데없이 길어지게 하고 관리 또한 힘들다. 배열을 사용하면 데이터를 깔끔하게 관리할 수 있으며 배열과 관련된 다양한 기능(ex. foreach)을 사용할 수 있어서 편리하다. 

### 배열 기능 예시 (foreach 반복문)
~~~php
foreach ($cafes as $cafe) { 
    echo $cafe . " "; // Starbucks Second Cup Tim Hortons
}
~~~
foreach는 배열에 대해 사용할 수 있는 반복문 중 하나이다. 위 코드에서는, $cafes 배열 안의 데이터를 하나씩 순차적으로 출력하라는 뜻. 여기서 $cafes는 해당 배열의 이름이어야 하지만, 뒷 부분의 $cafe는 아무 이름이나 붙여도 된다. 하지만 상황에 맞는 이름을 붙이면 코드 읽는 것이 수월해짐.

### HTML로 리스트 생성하기
~~~html
<ul>
<li>Starbucks</li>
<li>Second Cup</li>
<li>Tim Hortons</li>
</ul>
~~~
HTML로 리스트를 생성하면 위와 같은 형태가 된다. 이것을 PHP로 다이나믹하게 바꿔보자!

### php로 다이나믹한 리스트 생성하기
~~~php
<ul>
    <?php 
        foreach ($cafes as $cafe) {
            echo "<li>$cafe</li>"; // 리스트가 생성된다.
        }
    ?>
</ul>
~~~
위와 같이 작성해도 되지만, 이렇게 쓰면 때때로 가독성이 떨어질 수 있다. 아래 방법도 한번 사용해보자.

~~~php
<ul>
    <?php foreach ($cafes as $cafe) : ?>
        <li><?= $cafe; ?></li> // <?= 는 화면에 출력하기 위한 명령어
    <?php endforeach; ?>
</ul>
~~~
첫 번째 방법과 두 번째 방법 중 아무거나 사용해도 되지만, HTML 코드가 복잡해지면 두 번째 방법이 조금 더 깔끔하다고 한다. 중요한 것은 내가 잘 알아볼 수 있도록 코드를 작성하는 것.

### 참고
* [PHP 기초 문법 (echo로 화면에 출력하기)](https://mochastudy.github.io/study/php-echo/)
* [PHP cURL & 네이버 API 이용 방법 (+ 배열과 foreach)](https://mochastudy.github.io/study/php-curl-naver-api/)

## 연관 배열
위에서는 기본적인 배열의 형태를 알아봤는데, 연관 배열(Associative Array)이라는 것도 있다. 이 배열은 키(Key)와 값(Value)을 사용한다.

~~~php
$person = [
    'age' => 28,  // 키는 'age', 값은 31
    'hair' => '갈색', // 키는 'hair', 값은 '갈색'
    'height' => 163 // 키는 'height', 값은 163
];
~~~

~~~php
<ul>
    <?php foreach ($person as $feature) : ?>
        <li><?= $feature; ?></li>
    <?php endforeach; ?>
</ul>
~~~ 
위의 코드를 실행하면 28, 갈색, 163이 출력된다. 아래 코드로 Key까지 함께 출력해보자.

~~~php
<ul>
    <?php foreach ($person as $feature => $value) : ?>
        <li><strong><?= $feature; ?></strong>: <?= $value; ?></li>
    <?php endforeach ?>
</ul>
~~~

### 연관 배열에 데이터 추가하기
배열 괄호 안에 직접 데이터를 추가해도 되지만, 항상 내가 직접 만든 배열을 사용하는 것이 아니고 API 등 외부에서 데이터를 가져오는 경우도 많다. 이럴 때는, 아래와 같은 방법을 이용해서 배열에 데이터를 추가한다.
~~~php
$person['name'] = "모카";
~~~

### 연관 배열에서 데이터를 삭제하려면?
~~~php
unset(person['age']);
~~~
[unset 함수](http://php.net/manual/en/function.unset.php)를 사용하면 연관 배열에서 해당 키를 삭제할 수 있다.


### 기본적인 배열에 데이터를 추가하려면?
연관 배열이 아닌 기본적인 배열에 데이터를 추가해야 한다면, [] 안에 넣을 key가 없으므로 그냥 []만 사용한다.
~~~php
$animals = ['dog', 'cat'];
$animals[] = 'elephant';
~~~


### 배열 출력하기
배열 안의 값 하나를 화면에 출력하려면 아래 방법을 사용하게 된다.
~~~php
echo $person['age'];
~~~

하지만 배열 전체를 출력할 때는, echo를 사용할 수 없다. echo를 사용하면 'Array to string conversion...'이라는 에러 문구를 보게 됨. echo는 출력할 문자열을 찾고 있는데, $person은 배열이기 때문. 따라서, 배열을 출력하려면 다른 명령어를 사용하게 된다.
~~~php
echo '<pre>';
var_dump($person);
echo '</pre>'

echo '<pre>';
print_r($person);
echo '</pre>'
~~~
var_dump와 print_r은 함수(function)
* [PHP.NET: var_dump](http://php.net/manual/en/function.var-dump.php)
* [PHP.NET: print_r](http://php.net/manual/en/function.print-r.php)

### 출력하고 바로 
~~~php
die(print_r($person)); 

print_r($person);
die();
~~~
[die](http://php.net/manual/en/function.die.php) 역시 함수로, 전체 코드를 실행하는 것이 아니라 확인하고 싶은 부분만 출력해보고 바로 실행을 종료하고 유용하고 싶을 때 쓰인다.
