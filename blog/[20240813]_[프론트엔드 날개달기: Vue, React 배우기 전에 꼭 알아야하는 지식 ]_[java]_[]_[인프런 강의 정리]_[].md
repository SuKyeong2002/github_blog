# DOM이란?

* 자바스크립트: 웹문서(html) 제어
* 제어법: 브라우저 안에 웹문서 해석할 수 있는 '렌더링 엔진' 존재
* 즉, 한 줄씩 해석 -> 모두 해석하면 문서를 객체화 -> 자바스크립트로 접근 가능
* 문서 객체 모델 (Document Object Model): 브라우저에서 자바스크립트로 html 요소를 제어하는 api
* api: 언어 X, 기능 O 
* 구조: Tree (document (html (head (meta, title), body (h1, p, div)))) 
* Node: Tree 안의 각각의 요소
* CSS Object Model: 자바스크립트로 CSS 조작 가능

# BOM이란?
* 브라우저 객체 모델 (Browser Object Model): 브라우저 자체
* Browser 객체: window, document, history, location, screen, navigator
* window: 모든 객체가 소속된 객체 (= 브라우저 창)
* 예: window.open("url"), window.close("url"), window.alert("메시지")/ 이때, window 생략 가능
* 주의사항: 자바스크립트에서는 함수도 객체, window도 객체
* document: 현재 문서에 대한 정보를 가지고 있는 객체
* 예: document.querySelector('#id값"), document.querySelector('#id값").textContent = "원하는 텍스트"/ 앞에 window 생략 빈번
* history: 현재의 브라우저가 접근했던 URL history 제어
* 예: history.back(), history.forward()
* location: 문서의 주소와 관련된 객체, window와 document 객체의 프로퍼티/ url 변경 또는 정보 수집
* 예: location.host, location.href="url" 
* screen: 사용자의 디스플레이 화면에 대한 다양한 정보를 가지고 있는 객체
* 예: console.log('텍스트'), console.dir(screen) 
* navigator: 실행중인 애플리케이션 (브라우저)에 대한 정보 확인/ 크로스 브라우징 이슈 해결 시 사용
* 예: navigator.geolocation.getCurrentPosition(function (pos) { var crd = pos.cords; console.log(${위치 정보})})

