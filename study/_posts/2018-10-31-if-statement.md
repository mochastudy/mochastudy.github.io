---
layout: post
title: Lesson 7 - 웹페이지 처리 구조와 If문 구조
categories: study
---

이번 강의에서는 드용님이 주신 샘플 코드를 바탕으로, 웹페이지가 화면에 보여지기까지의 처리 구조와 if문 구조에 대해 알아본다.

## 방문자 눈에 웹페이지가 보여지기까지의 처리 구조
* 방문자 - 브라우저 실행 - 브라우저 on - http(s) 도메인 입력 - 웹서버 도착 - 서버응답 - 방문자에게 보임
* 항상 웹서버까지 갔다가 최종적으로 방문자 눈에 보여지게 된다. PHP 처리 문구가 없더라도 무조건 웹서버까지 갔다가 오게 됨.
* 여기에 서버 처리 과정이 포함되면, 새로고침이든 접속이든 그 어떤 상황이라도 이 과정을 거치게 된다 (단, 서버캐싱은 예외).

## 샘플 코드 둘러보기
![로그인 페이지](http://mocha.dothome.co.kr/images/7-1.png)
* 방문자가 처음 페이지에 접속하면 브라우저가 서버로 넘겨준 데이터는 존재하지 않음
* $input_pass = $_POST['password']: POST 방식으로 비밀번호를 받게 되는데 처음 페이지를 열면 아무런 데이터가 들어 있지 않아서 '비밀번호를 물어보는 화면'이 나타나게 된다.

연습: [네이버 API 1 - 비밀번호 테스트](http://mocha.dothome.co.kr/practice/password-test.php)

## If문 구조 알아보기
~~~html
if (!start) {
    조건이 만족하면 (즉, 거짓이라면)
}
if ($start) {

} else {
    조건이 만족하지 않는다면 (즉 거짓이라면)
}
~~~
* 위의 두 if문은 같은 결과를 반환한다. '!(느낌표)'는 부정을 의미
* 조건을 만족하기 위해서는 참이라는 결과가 나와야 첫번째 중괄호의 내용이 실행되며, 다른 경우는 else{}를 이용한 거짓 구조까지 만들어야 한다.
* 위의 경우에는 $start 앞에 이를 부정하는 !(느낌표)를 붙여서 거짓이라면 참이 되게 하는 구조이다.

