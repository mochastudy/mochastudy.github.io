---
layout: post
title: Lesson 8 - 네이버 OPEN API 사용해서 블로그 검색 결과 출력하기
categories: study
---

이번 강의에서는 네이버의 OPEN API를 사용해서 가공되지 않은 검색 결과를 간단히 출력해 본다.

네이버의 OPEN API를 사용하기 위해서는 네이버 개발자 센터에 등록한 후, 애플리케이션을 등록해야 한다. 네이버의 OPEN API에서 제공하는 API 종류는 다양하므로 만들고자 하는 프로그램에 맞춰서 종류를 선택해야 하는데, 일반적으로 키워드 관련 프로그램은 '검색'을 선택하면 된다.

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