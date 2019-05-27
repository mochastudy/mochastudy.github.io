---
layout: post
title: Lesson 9 - 네이버 검색 API 기본 설명서 살펴보기
categories: project2
---

이번 강의에서는 네이버 검색 API 기본 설명서를 살펴보고 간단하게 실습 해본다.

## 네이버 검색 API 기본 설명서 살펴보기
네이버 검색 API ([링크](https://developers.naver.com/docs/search/blog/))

![API 기본 정보](http://mocha.dothome.co.kr/images/9-1.png)
* XML 타입으로 결과 값을 받을 것인가?
* JSON 타입으로 결과 값을 받을 것인가?

<br/><br/>

![요청 변수](http://mocha.dothome.co.kr/images/9-2.png)
* query(쿼리)는 '문자열(string, 스트링)' 형태이며 필수이다. 쿼리문을 요청할 때는 문자 인코딩을 해야 함 (ex. urlencode).
* display(디스플레이)의 타입은 '정수(integer)'로, 보내는데 필수는 아님. 생략해도 문제 없다. 기본 출력 갯수는 10개.
* start(스타트)는 '정수(integer)' 타입이며 필수는 아님. 기본값은 1 (1페이지를 뜻함).
* sort(솔트)는 '문자열(string, 스트링)으로 보내야 한다. 기본은 sim(유사도) 정렬 방식인데, date(날짜) 정렬도 선택할 수 있음.

<br/><br/>

![호출](http://mocha.dothome.co.kr/images/9-3.png)
* cURL 타입으로 호출하고 요청하려면 헤드에 내가 앞서 발급받은 API KEY를 입력해야 한다.

## 네이버 API 기본 값 출력하기
[네이버 API 공식 가이드](https://developers.naver.com/docs/search/blog/)의 PHP 섹션을 보면, 여러가지 불필요한 주석, 출력문, 조건 등이 포함되어 있으므로 이 프로젝트에서는 코드를 정리해서 조금 더 간단한 구조를 사용한다.

**2018년 11월 14일자 코드 참고** (grap 또는 dev 폴더)

~~~php
<?php
    $id = "클라이언트 아이디"; // 개발자센터에서 발급받은 키
    $secret = "클라이언트 시크릿"; // 개발자센터에서 발급받은 키
    $url = "https://openapi.naver.com/v1/search/blog.xml?query=".urlencode('리니지');
    $post = false;
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_POST, $post);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    $head = array();
    $head[] = "X-Naver-Client-Id: ".$id;
    $head[] = "X-Naver-Client-Secret: ".$secret;
    curl_setopt($ch, CURLOPT_HTTPHEADER, $head);
    $response = curl_exec($ch);
    $status_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
    curl_close($ch);

    echo $response;
?>
~~~
### 코드 구조 설명
![구조](http://mocha.dothome.co.kr/images/9-5.png)

### 결과 출력
![결과 출력](http://mocha.dothome.co.kr/images/9-4.png)
네이버 오픈 API 검색에 '히비스커스'라는 쿼리(검색)문을 인코딩해서 전송하고, 응답 값을 단순히 출력(echo)만 해본 결과.

실제 결과 예시 [[바로가기](http://mocha.dothome.co.kr/practice/naverapi-practice1.php)]

### 참고! 닷홈에서 응답 없을 때
키마님께서 이와 관련해서 프로젝트방에 남겨주신 내용 참고하기
* 닷홈 서버의 아이피를 확인해야 함
