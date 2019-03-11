---
layout: post
title: Lesson 9 - 네이버 OPEN API 블로그 검색 결과 깔끔하게 가공하기
categories: study
---

이번 강의에서는 지난 강의에서 출력한 네이버 블로그 데이터를 깔끔하게 가공해 출력해본다.


## 네이버 API 출력문 가공하기
![가공되지 않은 데이터](http://mocha.dothome.co.kr/images/9-4.png)
정규식을 이용해서 내가 원하는 구간만 떼어내서 사용해도 되지만, 그렇게 하기에는 구조가 너무 복잡하기 때문에, 위와 같이 출력된 데이터를 가공해 보도록 한다.

~~~html
$keyma = new SimpleXMLElement($response);
~~~
![가공된 데이터](http://mocha.dothome.co.kr/images/10-2.png)
* 드용님이 제공해주신 예시에서는 XML 형식으로 네이버에 데이터를 요청했음
* 위의 코드는 XML 형식으로 넘겨 받은 데이터를, 배열 형태로 가공해주는 명령이며 그 값을 다시 $keyma에 담아 두겠다는 뜻
* 위 코드를 사용하면 가공된 XML 데이터가 출력된다.

~~~html
echo '<pre>';
print_r($keyma);
echo </pre>';
~~~
가공된 배열 값이 일렬로 쭉 문단처럼 나와서 보기 힘드니, 'pre'라는 html 태그를 이용해서 배열의 모양을 다듬어보자.

<br/><br/>

![가공한 데이터](http://mocha.dothome.co.kr/images/10-4.png)
가공한 XML 배열을 pre 태그를 이용해서 보기 좋게 출력한 모습

## 배열 출력하기
pre 태그를 사용해서 데이터를 보기 좋게 출력해봤으니 이제 내가 원하는 데이터에 접근해본다.
~~~html
echo $keyma["channel"]["item"][2]["title"];
~~~
~~~html
echo $keyma -> channel -> item[2] -> title;
~~~
* [channel] => SimpleXMLElement Object에서 배열에 꼬리표처럼 붙어 있는 오브젝트(Object)를 확인하자.
* 오브젝트(object)라는 꼬리표가 붙어 있는 배열은, 하위 접근하려고 할 때 접근지시자 '->'라는 것을 사용해야 한다.
* item[2] 이 부분은 왜 [] 괄호를 썼나? 가공된 배열에서 숫자 [2]의 부모를 찾아보면 array(배열)이라고만 되어 있기 때문! item 배열에는 오브젝트(object)가 붙어있지 않기 때문에 접근지시자가 아닌 괄호를 이용해서 일반 배열처럼 접근하게 된다.




* 네이버 개발자 센터 등록하기 ([바로가기](https://developers.naver.com/main/))
* 네이버 애플리케이션 등록하기

## 애플리케이션 등록하기
* 애플리케이션 이름: 아무거나
* 사용할 API: 검색
* 사용할 환경: Web
* 사용할 주소: 내 랜딩 페이지 주소

생성 후에는, Client ID와 Client Secret 키가 발급되는데, 시크릿키는 기본적으로 숨김 처리 되어 있으므로 사용하고자 할 때 '보기'를 눌러서 복사하면 된다.

## 네이버 검색 API 기본 설명서 살펴보기
네이버 검색 API ([링크](https://developers.naver.com/docs/search/blog/))
![API 기본 정보](http://mocha.dothome.co.kr/images/9-1.png)
* XML 타입으로 결과 값을 받을 것인가?
* JSON 타입으로 결과 값을 받을 것인가?
<br/><br/>
![요청 변수](http://mocha.dothome.co.kr/images/9-2.png)
* query(쿼리)는 '문자열(string, 스트링)' 형태이며 필수이다. 쿼리문을 요청할 때는 문자 인코딩을 해야 함 (ex. urlencode).
* display(디스플레이)의 타입은 '정수(integer)'로, 보내는데 필수는 아님. 생략해도 문제 없다. 기본 출력 갯수는 10개.
* start(스타트)는 '정수(integer)' 타입이며 필수가 아님. 기본값은 1 (1페이지를 뜻함).
* sort(솔트)는 '문자열(string, 스트링)으로 보내야 한다. 기본은 sim(유사도) 정렬 방식인데, date(날짜)를 선택할 수 있음.
<br/><br/>
![호출](http://mocha.dothome.co.kr/images/9-3.png)
* cURL 타입으로 호출하고 요청하려면 헤드에 내가 앞서 발급받은 API KEY를 입력해야 함

## 네이버 API 기본 값 출력하기
네이버 API 공식 가이드에서는 PHP 섹션을 보면, 주석문과 불필요한 출력문, 조건 등이 포함되어 있으므로 이 프로젝트에서는 더 간단한 구조를 사용한다.

★ 드용님 코드 참고 ★

![결과 출력](http://mocha.dothome.co.kr/images/9-4.png)
네이버 오픈 API 검색에 '히비스커스'라는 쿼리(검색)문을 인코딩해서 전송하고, 응답 값을 단순히 출력(echo)만 해본 결과.

## 참고! 닷홈에서 응답 없을 때
키마님께서 이와 관련해서 프로젝트방에 남겨주신 내용 참고하기
* 닷홈 서버의 아이피를 확인해야 함
