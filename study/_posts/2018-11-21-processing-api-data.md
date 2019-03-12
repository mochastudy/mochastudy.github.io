---
layout: post
title: Lesson 10 - 네이버 OPEN API 블로그 검색 결과 깔끔하게 가공하기
categories: study
---

이번 강의에서는 지난 강의에서 출력한 네이버 블로그 데이터를 깔끔하게 가공해 출력해본다.

## 지난 강의
![가공되지 않은 데이터](http://mocha.dothome.co.kr/images/9-4.png)
Lesson 9(181114)에서는 네이버 공식 API 기본 틀을 사용하여 응답 값을 출력해봤다. 정규식을 사용해서 이를 가공해도 되지만, 그렇게 하기에는 구조가 너무 복잡하므로 이번 강의에서는 이를 한 번 가공하여 출력해보도록 한다.

## 네이버 API 출력문 가공하기
XML로 넘겨받은 데이터를 가공할 때는 아래의 명령을 사용하게 된다.
~~~html
new SimpleXMLElement($response);
~~~
이를 이용하면, xml로 넘겨받은 데이터를 배열(array) 형태로 변환할 수 있다. 하지만 이렇게만 하면 이 데이터를 어떻게 사용해야 할지 감이 안오기 때문에, 이 가공된 데이터를 변수($변수명)에 담아둔다.
~~~html
$keyma = new SimpleXMLElement($response);
~~~

### 출력하기
위에서 가공해서 담아둔 변수를 출력하기 위해서는 print_r($배열변수); 명령어를 사용한다. 이 명령어를 사용하여 출력하면 아래와 같이 데이터가 출력 됨.
![가공된 데이터](http://mocha.dothome.co.kr/images/10-2.png)

### 배열의 모양을 있는 그대로 출력하기
위에서는 가공된 배열 값이 일렬로 쭉 문단처럼 나와서 한 눈에 살펴보기가 힘들다. 따라서, <pre>라는 html 태그를 이용해서 배열의 모양을 있는 그대로 보여지도록 해본다.
~~~html
echo '<pre>';
print_r($keyma);
echo </pre>';
~~~
![가공한 데이터](http://mocha.dothome.co.kr/images/10-4.png)


### 내가 원하는 데이터에 접근하기
pre 태그를 이용해서 눈에 보기 좋게 배열을 출력했으니, 이제 아래 이미지를 참고하여 내가 원하는 데이터에 접근 해보자. 
![데이터접근](http://mocha.dothome.co.kr/images/10-7.png)


### 배열 출력하기
pre 태그를 사용해서 데이터를 보기 좋게 출력해봤으니 이제 내가 원하는 데이터에 접근해본다.
~~~html
echo $keyma["channel"]["item"][2]["title"];
~~~
$keyma에 현재 가공된 xml 배열이 담겨 있으니 가정 먼저 쓰고, 그 뒷 부분을 순서대로 붙여나간다. 아래 이미지를 참고하자.
![배열](http://mocha.dothome.co.kr/images/10-8.png)
![오브젝트](http://mocha.dothome.co.kr/images/10-9.png)
배열에 꼬리표처럼 붙어 있는 오브젝트(object)를 확인하기

<br/><br/>

![접근지시자](http://mocha.dothome.co.kr/images/10-10.png)


* [channel] => SimpleXMLElement Object에서 배열에 꼬리표처럼 붙어 있는 오브젝트(Object)를 확인하자.
* 오브젝트(object)라는 꼬리표가 붙어 있는 배열은, 하위 접근하려고 할 때 접근지시자 '->'라는 것을 사용해야 한다.
* item[2] 이 부분은 왜 [] 괄호를 썼나? 가공된 배열에서 숫자 [2]의 부모를 찾아보면 array(배열)이라고만 되어 있기 때문! item 배열에는 오브젝트(object)가 붙어있지 않기 때문에 접근지시자가 아닌 괄호를 이용해서 일반 배열처럼 접근하게 된다.

### 순서도
![순서도](http://mocha.dothome.co.kr/images/10-11.png)
![구조](http://mocha.dothome.co.kr/images/10-12.png)

### 실습하기
[네이버 API 출력문을 가공해서 접근/출력하기](http://mocha.dothome.co.kr/practice/naverapi-practice2.php)