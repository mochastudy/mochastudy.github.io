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

## PDO (PHP Data Object)
PDO를 배우기 위해 알아야 할 것은 MySQL와 클래스의 기초 내용이다. 이 두 개념이 잘 이해 되지 않는다면 다시 한번 복습하고 올 것!

### 데이터베이스 연결하기 (MAMP 사용)
~~~php
require  'index.view.php';

try {
    new PDO('mysql:host=localhost;dbname=mytodo', 'root', 'root');
} catch (PDOException $e) {
    die('연결 할 수 없습니다.');
}
~~~
* 데이터베이스에 연결하기 위해서 PDO 클래스 인스턴스를 사용한다. PDO는 PHP Data Object를 의미하며, 데이터베이스 연결을 위한 인터페이스를 제공한다. 
* constructor를 통해 DSN을 넣는데, 어떤 데이터베이스(sqlite, mysql 등)를 사용할지 넣는 부분이다. 그리고 호스트를 넣는다. 그리고 어떤 데이터베이스를 사용할지 넣는다. 그리고 MySQL의 username과 password를 넣는데, 로컬에서는 대충 아무렇게나 세팅해도 되지만, 실제 서비스에서는 보안 문제가 발생할 수도 있으므로 복잡하게 정하는 것이 좋다.
* try와 catch를 사용해서 mysql이 컴퓨터에 깔려있지 않아서 불가능한 상황을 잡는다. new PDO... 줄을 시도하고 만약 에러가 난다면 die... 줄을 실행.

### 데이터베이스 내용 출력하기
~~~php
$statement = $pdo->prepare('select * from todos');
$statement->execute();

echo <pre>;
print_r($statement->fetchAll());
echo </pre>;
~~~
![배열](http://mocha.dothome.co.kr/images/190315-1.png)

### 중복 데이터 없애기
~~~php
echo '<pre>';
print_r($statement->fetchAll(PDO::FETCH_OBJ));
~~~
오브젝트로 fetch 하기

### 원하는 데이터 출력하기
~~~php
$tasks = $statement->fetchAll(PDO::FETCH_OBJ);
var_dump($tasks[0]->description);
~~~
접근지시자를 이용해서 출력하고자 하는 데이터에 접근한다.

### 순서 정리
'prepare' -> 'execute' -> fetchAll(PDO::fetchAll) 
* fetchAll은 메모리의 모든 데이터를 불러오는 것이기 때문에 데이터의 양이 많을때는 비효율적이므로 fetch(single call)가 사용되기도 한다. 하지만 여기에서는 일단 fetchAll을 사용한다.


### 데이터베이스 커넥션 에러
무슨 이유인지 모르겠지만 터미널에서 실행한 데이터베이스는 연결이 안되고 'SQLSTATE[HY000] [2002] No such file or directoryCould not connect.', 'SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client'라는 에러가 뜬다. 퍼미션 오류일 것 같긴한데 지금 당장은 해결 방법이 없으니 일단은 MAMP를 사용하고, 터미널은 명령어 익히는 용도로만 사용하자. 에러 메시지를 확인하는 법은 아래 코드를 참고!
~~~php
catch (PDOException $e) {
    $error = $e->getMessage(); 
    die('Could not connect.' . $error);
}
~~~

### 참고
인터넷에서 PHP 관련 자료를 찾아볼 때, 'mysql_connect();' 같은 명령어를 소개하는 블로그나 웹사이트들이 있을텐데 이러한 명령어들은 더이상 지원되지 않기 때문에 해당 자료가 얼마나 오래전에 쓰여진 것인지 확인하고, 되도록이면 최신 자료를 참고해야한다.

