---
layout: post
title: Lesson 5 - PHP cURL & 네이버 API 이용 방법 (+ 배열과 foreach) 
categories: study
---

이 강의에서는 PHP의 cURL 기능과 네이버 API를 이용한 연관 검색어 추출 방법, 그리고 배열과 foreach에 대해서 살펴본다.

## PHP cURL
* PHP의 cURL은 'Client URL Library'로, 사용자가 원하는 도착지의 웹페이지 내용을 모두 가져와서 내 서버에서 출력하는 기능이다.
* cURL은 사용되는 곳이 상당히 많은 중요한 기능이다. 실제로 아스라다의 98%는 이 기능을 활용해서 만들어졌다.
* PHP가 설치 되어 있다고 무조건 다 cURL이라는 명령을 쓸 수 있는 것은 아니고, PHP 기능 설정에서 cURL을 허용해 주어야 이용할 수 있다. 
* 단, 무분별한 과도한 cURL 접근, 헤더 없이 접근하는 등, 무작정 접근했다가는 밴 될 수 있으니 유의하자.

## 네이버 API 공식 매뉴얼 사용하기 (블로그 검색 API)
![네이버 API 매뉴얼](http://mocha.dothome.co.kr/images/5-0.png)
링크: [네이버 공식 API 매뉴얼](https://developers.naver.com/docs/search/blog/)

### cURL 기본 코드
~~~php
<?php
	$url = "" // 도착지 주소;
	$post = false;
	$ch = curl_init();
	curl_setopt($ch, CURLOPT_URL, $url);
	curl_setopt($ch, CURLOPT_POST, $post);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
	$response = curl_exec($ch);
	$status_code = curl_getinfo($ch, CURLOPT_HTTP_CODE);
	curl_close($ch);
?>
~~~
* **LINE 3**: 도착지 주소
* **LINE 5**: cURL의 세션을 초기화 해서, ch라는 변수에 담아 두겠다는 의미 (간단하게 말하면 cURL을 시작하겠다는 의미)
* **LINE 6**: cURL의 도착지의 url을 위의 변수에서 가져온다.
* **LINE 7**: cURL POST 방식을 위의 변수에서 가져온다. 변수에는 거짓으로 되어 있으니 GET 방식이 됨. 이 코드를 생략해도 기본적으로 GET 방식으로 접근하게 됨.
* **LINE 8**: 결과를 받을 것인지에 대한 코드로, '참'으로 되어 있으니 응답값을 받겠다는 뜻.
* **LINE 9**: 이 변수에 도착지(파싱 한 곳)의 모든 데이터가 담겨지게 됨.
* **LINE 10**: 도착지의 서버 응답코드가 담겨지게 됨. 정상이면 200.
* **LINE 11**: cURL 종료

### 헤더 값
* 도착지 주소에 'https://search.naver.com/search.naver?query=%검색어'를 넣고 서버의 응답 코드를 출력하면 '403'이 뜨는데, 이 때 결과 값이 담겨있는 $response를 출력하면 네이버의 '검색 서비스 이용이 제한되었습니다.'라는 메세지가 뜬다.
* 이렇게 단순하게 접근하면 프로그램 봇 매크로로 인식해 차단되는데, 이것은 1회성 차단일 뿐이지 밴은 아니다.
* 네이버 기준에서 이를 해결하려면, 네이버 공식 api에 있는 헤더 값을 넣어주면 된따. 헤더 값이 없다며 봇이나 프로그램이 접근한 것으로 간주하기도 하므로, 이 값을 입력하면 해결 됨.

~~~php
$head = array();
$head[] = "X-Naver-Client-Id: naver";
$head[] = "X-Naver-Client-Secret: naver.com";
curl_setopt($ch, CURLOPT_HTTPHEADER, $head);
~~~

이렇게 하면 응답코드는 200이 뜨고, 검색 결과도 제대로 뜨게 된다.

### 네이버 검색 페이지에서 연관 검색어 추출하기
* 네이버 검색 페이지에서 크롬 개발자 도구를 열고 추출할 영역을 찾는다. 그리고 정규식을 사용해서 추출한다.
* 동일한 패턴을 찾을 때 사용하면 PHP의 명령어는 preg_match_all.
* preg_match_all('따옴표 안의 내용을 찾아 주시오', '이 데이터에서', '그리고 그 결과를 여기에 담아 놓으시오');
* preg_match_all('이거 찾아줘', $response, $keyword_list);
* 네이버 연관 검색어를 추출하기 위한 명령어: preg_match_all('/data-area="(.*?">(.*?)<\/a>/', $response, $keyword_list);

## 배열
* 위의 예시에서 preg_match_all 명령어를 사용해서 해당하는 패턴을 모두 찾으면 해당하는 부분은 모두 $keyword_list에 배열의 형태로 저장된다. $keyword_list를 그냥 출력하면 'Array', 즉 '이것은 배열이다~'라고 출력함. 따라서 배열이 구조를 출력해볼 때는 echo가 아닌 print_r($배열이담긴변수);를 사용해서 출력.
* 하지만, 이렇게 출력하면 데이터가 포맷이 안되어 읽기 힘드르다. 이 경우, print_r을 사용하기 전에 echo 'pre';를 사용하면 읽기가 더 간편하다. 이렇게 정렬한 후, 원하는 부분을 찾아 해당 값을 []안에 입력하면 된다.

## foreach
~~~php
foreach($keyword_list[2] as $key){
	echo $key . '<br/';
}
~~~
* 네이버 연관검색어가 업데이트 되고 나서 무조건 최대 10개의 검색어를 출력하지만, 10개가 없을 경우도 있다.
* 단순한 반복문이라면 for을 사용하면 되지만, 배열의 경우 foreach를 사용하는 것이 훨씬 효율적이고 처리 속도도 빠르다. 위의 예시에는 배열이 존재하므로 배열 반복(foreach)를 사용.
* foreach는 배열이 몇개가 있든지 그 배열의 갯수만큼 반복 해달라는 의미 