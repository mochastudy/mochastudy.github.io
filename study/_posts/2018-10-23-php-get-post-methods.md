---
layout: post
title: Lesson 4 - PHP 기초 문법 (Form, POST & GET)
categories: study
---

이 강의에서는 html form 태그와 GET, POST 방식 및 사용 방법에 대해 알아본다.

* 클라이언트는 서버로 데이터를 보낼 때, **form**이라는 html 태그를 사용한다 (동일 서버 내에서 직접 데이터를 주고 받을 때, 외부 서버의 경우 ajax 등의 동기, 비동기 방식의 통신이나, 웹소켓 등의 통신방식을 사용하게 됨.
* **form, input, name**은 정말 중요한 부분이고 필수요소! 이게 없다면 서버로 데이터를 보내고 서버가 데이터를 받아서 처리하는 과정이 불가능하진다.

## Form 태그
일반적인 Form 구조
~~~html
<form action="" method="POST">
	<input type="text" name="mocha">
	<input type="submit" value="서버야 받아라">
</form>
~~~

### form에 입력한 값 화면에 출력하기
~~~php
<form action="" method="POST">
	<input type="text" name="mocha">
	<input type="submit" value="서버야 받아라">
</form>

<?php echo $_POST['mocha']; ?>
~~~
* **LINE 1**: form 태그를 이용해서 서버로 데이터를 보낼 것이다 & 데이터를 보내는데, **POST**라는 방식으로 보낼 것이다.
* **LINE 2**: **input**은 텍스트 타입의 입력창 & 이 입력창의 데이터를 서버가 확인할 때, **mocha**라는 이름표를 찾아서 확인하라.
* **LINE 3**: **submit**으로 서버에 전송
* **LINE 6**: **echo**를 사용해서 화면에 출력 & 브라우저가 POST 방식으로 보낸 데이터 중, **mocha**라는 꼬리표를 찾아서 출력
* 참고: [MDN form elemeent (action 부분)](https://developer.mozilla.org/docs/Web/HTML/Element/form)

## 메소드 방식 (POST & GET)
* 메소드 방식에는 **POST** 또는 **GET**이라는 방식이 있음.
* GET 방식의 결과에는 URL 뒷 부분에 쿼리스트링('?'의 뒷 부분)이 붙는다.
* POST 방식의 결과에는 쿼리스트링이 붙지 않는다.
* GET 방식보다 POST 방식이 보안에 조금 더 좋음.          
* GET이든 POST든, 어떤 데이터를 보내는지는 둘 다 외부에서 파악할 수 있지만, 실제 브라우저를 보는 사람의 눈에는 POST 방식이 더 깔끔해보이고, 어떤 데이터를 주고 받는지에 대한 예측을 바로 할 수 없다.
* 하지만 브라우저는 두 경우 모두, 쿼리스트링 정보를 가지고 있음.

### 메소드 방식: POST 
~~~html
<form action="" method="POST">
~~~
![POST 방식](http://mocha.dothome.co.kr/images/4-post.png)
주소: mocha.dothome.co.kr

### 메소드 방식: GET
~~~html
<form action="" method="GET">
~~~            
![GET 방식](http://mocha.dothome.co.kr/images/4-get.png)
주소: mocha.dothome.co.kr/?mocha=모카

### GET을 사용하는 이유?
GET을 사용하는 이유는 다양하지만, 포털 사이트의 경우는 리퍼러(검색 경로)를 남기기 위해 사용하며, 자바스크립트를 이용해서 현재 브라우저의 URL을 확인하는 경우 등이 있다.

프로젝트에서는 주로 POST 방식을 사용할 예정!
