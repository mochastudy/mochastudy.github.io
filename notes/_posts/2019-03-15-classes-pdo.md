---
layout: post
title: PHP 101 - 클래스, PDO 기초
description: >
categories: notes
---

지난 강의에서 MySQL 기본 사용법에 대해 알아봤는데, PHP와 MySQL을 연동하는 법을 배우기 전에 한 가지 더 배울 것이 있다. 오늘은 클래스에 대해 간단히 살펴보고 데이터베이스 연동으로 넘어가도록 한다.

## 클래스
클래스의 기본 형태는 아래와 같다. 
~~~php
class Task {}
// Todo, Comment, User, Task...
~~~
클래스명을 지을 때는 보통 명사를 사용하며 복수가 아닌 단수를 사용하면 간편하다. 그리고 첫 글자는 대문자로 한다.

### 변수 추가하기

변수를 클래스에 추가할 때 어떤 요소를 추가할지 조금 더 쉽게 생각할 수 있는 방법에는 MySQL 데이터베이스 테이블의 칼럼들을 참고하는 방법이 있다. 이전 강의에서 'description'과 'completed'를 테이블에 추가 했는데, 여기서는 클래스에 이 두 가지 변수를 추가해본다.

참고! 클래스 안의 함수(function)은 보통 함수라 부르지 않고 메소드(method)라 부르고 클래스 안에서 정의되지 않은 함수를 함수라 부르는데, 이 둘은 그냥 같은 것이라 보면 된다.

~~~php
class Task {
    protected $description; // properties protected from outside world
    protected $completed;

    public function __construct($description)
    {
        // Automatically triggered on installation
        $this->description = $description;
    }

    public function complete()
    {
        $this->completed = true;
    }

    public function isComplete()
    {
        return $this->completed;
    }

}

$task = new Task('Go to the store'); // 새로운 task 오브젝트
$task -> complete(); // task 마치기
~~~
* 새로운 Instance는 오브젝트 타입이다.
* $this는 Task instance(오브젝트 타입)이며, description은 property. 
* 여기서 description의 값은 매번 다를 수 있다. 반면에 completed의 값은, 새로운 할 일을 생성하면 항상 '미완료'이므로 __construct의 파라미터에 이를 포함하지 않고 false 값을 넣었다.
* protected와 public은 visibility를 결정하는 부분이다. protected를 사용하면 외부에서 $task->description 이런식으로 접근할 수 없다. $description이 public이면 외부에서 접근할 수 있다.
* 함수의 이름을 지을 때는 문장으로 생각해본다.

### 배열 사용하기
~~~php
$tasks = [
    new Task('Go to the store'),
    new Task('Write a new post'),
    new Task('Learn PHP')
];
~~~
클래스는 블루프린트와 같은 개념이며, 각 각의 인스턴스는 다른 값, 다른 property를 포함한다. 

### View에 불러오기
~~~php
<ul>
    <?php foreach ($tasks as $task) : ?>
        <li>
            <?php if ($task->completed) : ?>
                <strike>
            <?php endif; ?>

            <?= $task->description; ?>

            <?php if ($task->completed) : ?>
                </strike>
            <?php endif; ?>
        </li>
</ul>
~~~
description이 protected이기 때문에 $task->description을 사용할 수 없다. 여기에서는 이 부분에 대해 깊게 들어가지는 않을 것이므로 단순히 protected를 public으로 바꿔준다. 

클래스에 대한 내용은 좀 길고 복잡하므로 이해될때까지 반복해서 볼 것!
