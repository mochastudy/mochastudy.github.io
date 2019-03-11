---
layout: post
title: Lesson 6 - 바뀌는 키워드에 대한 네이버 연관 검색어 추출하기
categories: study
---

이번 강의에서는 지난 강의(고정 키워드로 연관 검색어 추출)에 이어, 입력하는 키워드에 따라 연관 검색어가 다르게 출력되도록 해본다.

## 고정된 주소로 고정된 값 출력 (지난 강의)
~~~html
<body>

	$url = "https://search.naver.com/search.naver?query=%EB%A6%AC%EB%8B%88%EC%A7%80";
	
	$post = false;
	$ch = curl_init();
	curl_setopt($ch, CURLOPT_URL, $url);
	curl_setopt($ch, CURLOPT_POST, $post);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
	
	$head = array();
	$head[] = "X-Naver-Clienet-Id: naver";
	$head[] = "X-Naver-Client-Secret: naver.com";
	curl_setopt($ch, CURLOPT_HTTPHEADER, $head);
	
	$response = curl_exec($ch);
	$status_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
	curl_close($ch);
	
	preg_match_all('/data-area="(.*?)">(.*?)<\/a>/', $response, $keyword_list);
	
	foreach($keyword_list[2] as $key){
		echo $key . '<br/'>;

</body>
~~~

지난 강의에서 배운 것은 고정된 주소(네이버 특정 키워드 검색 결과)를 이용해서 항상 고정된 값만 출력하게 했었다. 이번 강의에서는 키워드 입력창을 만들어서 키워드를 입력할 때마다 그에 맞는 값이 나옫도록 해볼 것.

### Form을 사용하여 값을 받아서 출력하기
~~~html
<body>
★★★★★ 여기에 form 삽입 ★★★★★
<?php 
	url = "https://search.naver.com/search.naver?query ...
~~~

* 지난번의 실습 내용에 form을 추가하는데, form을 추가할 때는, body 안쪽에 출력문보다 위에 삽입하면 된다. 출력문보다 뒤에 넣어도 상관 없지만, 입력창이 리스트보다 위에 있는 것이 보기가 편하다.
* url의 쿼리 부분은 실제 검색어가 되는 부분인데, '%EB%A6%AC'와 같은 알아보기 힘든 문자열로 나타난다. 한국어 특성상 바로 인식이 안되기 때문에 urlencode라는 명령어를 이용해서 인코딩 한 경우이다 (참고: [PHP.NET - urlencode](http://php.net/manual/kr/function.urlencode.php)
* form에서 메소드를 포스트 방식(method="POST")으로 전송 했으므로 서버에서 해당 값을 받을 때도 포스트 방식($_POST['name'])으로 받아야 함.
* form은 해킹에도 많이 사용되는 요소이기 때문에, 액션에 다양한 옵션을 사용하기도 하지만, 강의에서 다루는 내용과는 약간 거리가 있으니 이 부분은 개인적으로 살펴볼 것! (참고: [MDN - form](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) / [Sending form data](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)


