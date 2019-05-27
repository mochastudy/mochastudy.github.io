---
layout: post
title: Lesson 12 - AJAX 시작하기
categories: project2
---

이번 강의에서는 AJAX에 대해 알아본다.

## ajax?
* 자바스크립트에서 ajax를 사용할 때 xhr라고 하는데, xhr은 ajax를 생성해주는 자바스크립트의 API이다.
* XMLHttpRequest = xhr (XML HTTP 요청)

### 크로스 도메인 정책
* ajax는 기본적으로 크로스 도메인(도메인 출처 정책)을 허용하지 않기 때문에 아무곳에나 ajax 요청을 날린다고 응답이 돌아오는 것이 아니다.
* 크로스 도메인 정책은 아무곳이나 막 접근 못하도록 하기 위한 '동일 출처 도메인'에 관련한 정책으로, 동일 출처(동일한 메인 도메인 내부)에만 접근을 허용하도록 되어있다.
* 따라서, ajax를 요청하는 곳(클라이언트)와 응답해줄 곳(서버)의 도메인 주소가 같거나, 서버에서 내 도메인이 아닌 '다른 도메인에서 요청이 오더라도 응답해주어라'라는 옵션을 넣으면 데이터를 전송하고 받을 수 있다.
* **참고** 똥생성기 플러그인 코드에 있던 asrdconan...도메인은 서버단에서 어떤 도메인도 다 접근 가능하게 설정해 놓은 것. 기본 값은 차단.

## 실습
1. TLS 통신의 경우는 무조건 TLS로 데이터를 주고 받아야 하니, 이번 실습에서는 TLS 구성을 하지 않은 상황을 기준으로 함.
2. 명령을 사용할 요청 주소가 HTTP로 시작하는 웹페이지 아무거나 띄우기 (로컬호스트, 닷홈 등...)
3. 웹페이지에서 콘솔을 띄운 뒤, 주어진 코드를 넣고 엔터
4. '언제나 화이팅입니다.'라는 문구가 출력됨.

### ajax 응답 값 출력 예시
~~~html
var xhr=new XMLHttpRequest();
var post_value = "포스트로 보낼 네임+값";

xhr.open("POST", "domain", true);
xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhr.onreadystatechange=function(){
    if(xhr.readyState==XMLHttpRequest.DONE && xhr.status==200){
        console.log(xhr.responseText);
    }
}, xhr.send(post_value);
~~~
* LINE 1: 명령어를 짧게 쓰기 위해, xhr 변수에 XML 요청을 담아둠.
* LINE 2: form 데이터 전송할 때, name(꼬리표) 붙여서 값을 전송하는 것과 같은 역할. 파라메터(쿼리스트링) 방식으로 사용됨 (ex. keyword=mocha&type=latte - keyword라는 꼬리표에는 mocha라는 값을, password라는 꼬리표에는 latte라는 값을 담아 보내는데, 이 때 keyword와 password는 input에서 name과 같다).
* LINE 4: POST 방식으로 요청, 그리고 어디에 요청할 건지 주소를 입력
* LINE 5: 요청 헤더. 헤더에 콘텐츠 타입과 여러가지 타입을 함께 전송 (타입에는 애플리케이션 xml 데이터 json 기타 등등 많은데, 일반적인 응답 서버 요청시 일반데이터(html)는 위 방식을 이용하면 모두 응답을 받을 수 있다)
* LINE 6-8: 정상적인 응답이 돌아왔다면, 그 내용물은 xhr.responseText에 담기게 된다.
* LINE 9: 요청을 보내라는 명령. 요청을 보낼건데, 보낼 때 위의 키워드와 패스워드가 담겨진 값을 함께 보내라는 뜻.

## 서버 구성 예시
~~~html
<?php 
    header("Content-Type: text/html; charset=UTF-8");
    header("Access-Control-Allow-Origin: *");
    header("Allow-Control-Allow-Origin: *");

    echo "언제나 화이팅입니다.";
?>
~~~
* '*(와일드카드/유니버셜)'은 그 어떤 주소로 요청이 오더라도 허용하겠다는 뜻.
* 내 도메인 외의 다른 도메인은 차단시키고 싶다면, 별 대신 내 도메인 주소를 넣으면 된다.
* 기본이 차단이니, 다른 도메인을 다 차단하게 된다면 LINE 2-3은 안 넣어도 됨.
