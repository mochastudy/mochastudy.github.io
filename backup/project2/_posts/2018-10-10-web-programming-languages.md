---
layout: post
title: Lesson 1 - 서버 언어(PHP)와 클라이언트 언어(HTML) 
description: >
image: 
categories: project2
---

이 강의에서는 서버 언어와 클라이언트의 종류와 차이점에 대해 알아본다.

## 서버 언어와 클라이언트 언어
서버 언어(PHP, JSP, ASP 등)는 서버가 해석하고 처리하며, 클라이언트 언어(HTML)는 웹브라우저가 해석하고 처리한다.
* **PHP**: 서버 언어. 클라이언트(웹 브라우저)가 전혀 해석하지 못함.
* **HTML**: 클라이언트 언어. 브라우저에 웹페이지를 출력하기 위해 사용하며, 서버 언어(PHP)를 해석하지 못함.

### 웹브라우저는 서버의 언어를 해석하지 못하는데 어떻게 화면에 출력하는가?
웹서버는 서버 언어를 해석하고 처리한 후, 이것을 HTML화 시켜서 브라우저에 전송함. 따라서, 서버 언어로 작성된 데이터들도 웹브라우저가 받아서 출력할 수 있음.

### HTML와 PHP를 둘 다 사용하는 이유
혼자서 모든 것을 처리하는게 아니라, 둘이서 일정한 부분을 나눠서 분할하여 처리하게 해서 코드 작성의 효율과 속도 및 자원 관리에서 이점이 있다.

## 실습하기
닷홈 호스팅에 index.php 파일을 올린 후, 구글과 네이버 웹마스터 도구에서 사이트 인증하기

* 서버 설정에 따라 값을 바꿀 수는 있지만, 보통 index라는 파일 이름이 메인 주소가 된다. 웹호스팅에서 기본적으로 index(.html 또는 .php)를 기본 메인으로 인식함.
* 웹서버 공간에 index.php와 index.html 두 파일이 모두 존재할 경우, index.html이 우선 순위가 높아서 index.php 파일은 무시된다.

