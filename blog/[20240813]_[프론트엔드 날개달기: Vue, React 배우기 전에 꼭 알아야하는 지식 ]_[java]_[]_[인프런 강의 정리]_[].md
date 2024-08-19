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
* 예: document.querySelector('#id값"), document.querySelector('#id값").textContent="원하는 텍스트"/ 앞에 window 생략 빈번
* history: 현재의 브라우저가 접근했던 URL history 제어
* 예: history.back(), history.forward()
* location: 문서의 주소와 관련된 객체, window와 document 객체의 프로퍼티/ url 변경 또는 정보 수집
* 예: location.host, location.href="url" 
* screen: 사용자의 디스플레이 화면에 대한 다양한 정보를 가지고 있는 객체
* 예: console.log('텍스트'), console.dir(screen) 
* navigator: 실행중인 애플리케이션 (브라우저)에 대한 정보 확인/ 크로스 브라우징 이슈 해결 시 사용
* 예: navigator.geolocation.getCurrentPosition(function (pos) { var crd = pos.cords; console.log(${crd.latitude});}), navigator.appName, navigator.appVersion, navigator.userAgent
* 자세한 기능: location.mdnb 검색 후 사이트 참고

# script 태그 defer, async
* 주의: 파싱 전 script 만나는 경우 에러 발생
* 자바그스크립트 효과적으로 가져오는 법: body 최하단에서 script 로드, load 이벤트 리스너 등록(window.onload, DOMContentLoaded) 
* window.onload: HTML 파싱 DOM 생성 그리고 외부 콘텐츠 로드 후 발생 (콘텐츠가 많을 시 비효율적)
* DOMContentLoaded: HTML 파싱 DOM 생성 후 발생 (콘텐츠가 많을 시 효율적)
* defer 속성: HTML 파싱과 함께 비동기로 javascript 파일 불러옴 (효율적)
* ㄴ 즉, HTML 파싱 완료된 후 javascript 코드 실행
* async 속성: HTML 파싱과 함께 비동기로 javascript 파일 불러옴 (꼭 필요 시)
* ㄴ 즉, HTML 파싱 완료 X 시에도 먼저 로딩되는 javascript 코드부터 실행
* ㄴ 즉, javascript 파일 실행 시 HTML 파싱 중단

# this란 무엇인가?
* this: 객체 (= 호출하는 놈, 즉 대부분 함수를 호출하는 방법에 의해 결정)
* this의 기본값: window 객체
* 예: person.printThis; console.log("this === person", this === person); console.log("this === window", this === window); // true false 출력
* 예: printThis; console.log("this === person", this === person); console.log("this === window", this === window); // false true 출력
* 예외1: ESS bind-this 설정 (* 한 번만 사용 가능!)
* ㄴ 예: function printThis () {
    console.log(this) // default this == window
}
let person1 = {
    name: '홍길동',
};
let peintThis1 = printThis.bind(person1);
printThis1()' // {name: '홍길동'} 출력
let person2 = {
    name: '김길동',
};
let peintThis1 = printThis.bind(person2);
printThis1()' // {name: '홍길동'} 출력



# API란 무엇인가?


# 동기와 비동기란?


# 프론트엔드&백엔드란?



# 이벤트 전파, 버블링&캡쳐링


# 자바스크립트 유용한 Array APIs


# JavaScript 모듈 시스템


# NPM 기초 강좌


# Webpack 기초 강좌 

