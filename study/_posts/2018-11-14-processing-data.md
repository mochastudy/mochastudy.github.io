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