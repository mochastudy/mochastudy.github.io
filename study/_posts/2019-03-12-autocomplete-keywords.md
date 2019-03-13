---
layout: post
title: Lesson 13 - 정규식 없이 검색엔진 자동완성어 추출하기 (네이버 예시)
categories: study
---

이번 강의에서는 정규식 없이 네이버, 다음, 구글, 줌 등의 검색엔진에서 자동완성어 추출하는 방법을 알아본다.

## 자동완성 호출 주소
* **PC**: https://ac.search.naver.com/nx/ac?of=os&ie=utf8&q=오버워치&oe=utf8
* **모바일**: https://mac.search.naver.com/mobile/ac?of=os&ie=utf8&q=오버워치&oe=utf8

## 호출 주소 찾는 법
검색엔진 창에서 개발자 도구의 네트워크 탭을 켠 뒤, 어디로 통신하는지 확인하면 도착지를 알아낼 수 있다. 검색어창에 타입하면 실시간으로 데이터를 주고 받는 것을 볼 수 있다. 자동완성어이기 때문에 문자 하나 하나를 칠 때마다 응답해야 하니, ajax 같은 비동기통신 방식을 통해 실시간으로 호출하고 응답하고, 가벼운 json 타입으로 무리가지 않도록 구현 됨.
![네이버](http://mocha.dothome.co.kr/images/13-1.png)
![키워드](http://mocha.dothome.co.kr/images/13-2.png)

요청지 주소 값을 눌러보면 요청헤더와 응답헤더, 그리고 쿼리스트링(파라메터)도 확인 가능.
![네트워크](http://mocha.dothome.co.kr/images/13-3.png)


## 자동완성어 주소값을 curl 파싱해서 출력하기
위의 주소의 응답 데이터는 json 타입으로 제공되기 때문에, json을 디코딩 하면 자동으로 배열화(Array) 된다.

### json으로 넘어오는 데이터 디코딩(Decode) 하는 방법
json_decode를 사용해서 디코드 한다.
~~~html
$json = json_decode($response);
~~~

위에서 $response가 디코딩 되면서 배열화가 되었으므로, print_r을 이용해서 배열을 출력할 수 있다.
~~~html
print_r($json);
~~~

추출하고자 하는 부분이 몇 번째 배열인지 확인 후, 배열 번호를 추가한다. 이렇게 하면 키워드가 담겨져 있는 배열만 떨어져 나오게 된다.
~~~html
print_r($json[1]);
~~~

### 배열반복(foreach)를 이용해서 출력하기
위에서 배열로 변환했으므로 배열반복(foreach)를 이용하면 키워드를 간편하게 출력할 수 있다.
~~~html
foreach($json[1] as $keyword){
    echo $keyword . '<br/>';
}
~~~

** 자세한 내용은 드용님이 주석 달아주신 이미지 참고하기 **
