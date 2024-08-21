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
* let person2 = {
    name: '김길동',
};
let peintThis1 = printThis.bind(person2);
printThis1()' // {name: '홍길동'} 출력
* 예외2: 전역 스코프에서 this: window 객체
* 예외3: 화살표 함수(ES6)에서 this
* ㄴ 즉, 자신을 포함하고 있는 외부 Scope에서 this 계승 받음
* ㄴ 즉, 자신을 감싼 정적 범위
* ㄴ 주의사항1: 객체 메서드 선언 시 사용 X
* ㄴ 주의사항2: addEventListener 함수의 콜백 함수에서 사용하면 this가 상위 컨텍스트 (window 객체) 가리킴
* ㄴ 이전에는, that 사용
* Strict Mode에서 this
* ㄴ 즉, 기본값: undefined (엄격함)

# API란 무엇인가?
* API (Application Programming Interface): 응용 프로그램에서 사용할 수 있도록 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있도록 만든 인터페이스 (즉, 애플리케이션에서 데이터를 읽거나 쓰기 위해 사용하는 인터페이스)
* Interface: 상호 간의 소통을 위한 방법
* ㄴ 예: 사람이 저녁을 먹기 위해 스마트키(인터페이스)를 눌러 자동차 염
* ㄴ 예: 사람이 폰에 있는 배달의 앱(인터페이스)을 통해 저녁을 먹음 
* ㄴ 예: 앱에서 기상청에게 Request(예: http://api.data.go.kr/weather/list)하고 Response(예: {"today": "2021-04-09", "weather": "맑음"}) 받음
* HTTP API: 인터넷상 API/ 프로토콜 = 소통방법 = 통신방법 = 통신규약
* 날씨정보앱 (프론트엔드(클라이언트(요청자))) <-> API/DB서버 (백엔드(서버(제공자)))
* IoT 애플리케이션: 창문 <- (창문개방 API) <- (제어) <- 미세먼지 데이터 읽는 기기 <- (값 수신) <- (미세먼지 농도전달 API) <- 미세먼지 측정 기기
* ㄴ 위의 경우, HTTP 보다는 MQTT/CoAP API (저사양/저전력) 사용이 효과적
* Class API: 통신 프로토콜 레벨 X 소스 코드 레벨 O
* ㄴ 예: console API, Java API 등
* 종류: Private API (비공개) <-> Public API (공개/ 예: 카카오, 네이버 등)
* UI (User Interface): 사용자가 소통하기 위한 접점

# 동기와 비동기란?
* 동기(Blocking): 답변(결과)을 기다리는 것 (비효율적/단순)
* ㄴ 예: 수박을 트럭 앞 사람에게 전달하고 잘 실었다는 답변 기다리고 받은 후 다음 일 수행
* ㄴ 예: 택배기사가 1호에게 물건 전달 후 잘 받았다는 답변 기다리고 받은 후 다음 일 수행
* ㄴ 결과가 다음 행동에 지장을 주는 경우 사용
* 비동기(Non-blocking): 답변(결과)을 기다리지 않는 것 (효율적/복잡)
* ㄴ 예: 수박을 트럭 앞 사람에게 전달하고 잘 실었다는 답변 기다리지 않고 다음 일 수행
* ㄴ 예: 택배기사가 1호에게 물건 전달 후 잘 받았다는 답변 기다리지 않고 다음 일 수행
* ㄴ 프로세스 추가 예: 비동기식으로 일하되, 배송도착 사진을 촬영해서 받는 사람에게 전송
* 프로그래밍적 동기: A계좌에서 인출하기 -> B계좌로 송금하기

# 프론트엔드&백엔드란?
* 프론트엔드(클라이언트: 요청) 개발자: 사용자가 사용하는 화면과 같은 앞단 개발자
* 백엔드 개발자(서버: 응답, 서버 위에 있는 애플리케이션 개발): 눈에 보이지 않는 영역으로 API와 같은 뒷단 개발자 
* ㄴ 예: 프론트엔드 (API 확인 후 HTML/CSS/JAVAScript와 같은 웹 언어를 사용하여 일반적인 사용자가 볼 수 있도록 사용자 인터페이스 개발) <-> 백엔드 (프론트엔드에서 포켓몬 목록을 가져갈 수 있도록 자바/파이썬/노드JS와 같은 서버측 언어를 사용하여 API 개발, API 호출 시 결과값 반환하는데 이때 URL/API 명세서를 프론트엔드에게 제공)
* ㄴ 서버 개발자 예: 매일 포켓몬을 가장 많이 등록한 유저 추첨 기능 추가 
* ㄴ 즉, 서버측에서 매일 하루에 한 번씩 자동으로 DB에 접근하여 정기적으로 배치프로그램 수행
* ㄴ 대박날 경우: 안드로이드와 ios 어플 론칭 
* ㄴ 즉, 클라이언트: 자바/코틀린과 같은 언어 사용해 안드로이드 앱 개발 & Object-C/Swift와 같은 언어 사용해 ios 앱 개발
* 웹: 프론트엔드 <-> 백엔드
* ㄴ 과거: JSP/PHP와 같은 템플릿엔진 기반 개발 많이 진행 -> 웹 개발자
* ㄴ 현대: React/Vue/Angular와 같은 강력한 웹 개발 프레임워크 등장 & 브라우저와 html5 기술 발전하면서 좀 더 파워풀한 웹 개발 미션 발생 -> 프론트엔드/백엔드 개발자 
* 앱: 클라이언트 개발자 <-> 모바일 개발자 또는 안드로이드 개발자 <-> ios 개발자


# 이벤트 전파, 버블링&캡쳐링
* 캡쳐링(capturing): body(최상위) -> main -> div -> p -> span(최하위)
* ㄴ 예: Event.eventPhase()
* ㄴ 이벤트 전파 막기: Event.stopPropagation()
* 버블링(bubbling): span(최하위) -> p -> div -> main -> body(최상위)
* ㄴ 예: Event.addEventListener()
* ㄴ 이벤트 전파 막기: Event.stopPropagation()/ Event.preventDefault()


# 자바스크립트 유용한 Array APIs
* map(): 배열 내의 모든 요소에 대하여 주어진 함수를 호출한 결과를 모아서 새로운 배열을 반환
* ㄴ 배열 예: const numbers = [1, 2, 3, 4, 5, 6, 7]; 
const result= numbers.map(function (number) {
    return number * 2;
});
console.log(result); // {2, 4, 6, 8, 10, 12, 14} 출력
* ㄴ 단순화: const numbers = [1, 2, 3, 4, 5, 6, 7]; 
const result= numbers.map((number) => number * 2;);
console.log(result); // {2, 4, 6, 8, 10, 12, 14} 출력
* 객체 예: class Student (
    constructor(name, koreanLanguage, english, mathmatics) {
        this.name = name;
        this.koreanLanguage = koreanLanguage;
        this.english = english;
        this.mathmatics = mathmatics;
    }
)
const student1 = new Student("홍길동", 95, 87, 75);
const student2 = new Student("김길동", 67, 80, 100);
const student3 = new Student("고길동", 89, 75, 80);
const student4 = new Student("최길동", 48, 52, 98);
const students = [student1, student2, student3, student4];
console.log("이름", student.map((student)=>student.name)); // ['홍길동', '김길동', '고길동', '최길동'] 출력
* some(): 배열 안의 어떤 요소라도 주어진 판별 함수 통과하는지  참/거짓 테스트
* ㄴ 예: const fluits = ["사과", "딸기", "배", "참외", "딸기", "수박"];
const result = fluits.some((fluit)=>fluit==="수박");
console.log(result); // true 출력
* ㄴ 인덱스도 가져올 경우: fluits.some(fluit, index)
* every(): 배열 안의 모든 요고사 주어진 판별 함수 통과하는지 참/거짓 테스트
* ㄴ 예: const fluits = ["사과", "딸기", "배", "참외", "딸기", "수박"];
const result = fluits.every((fluit)=>fluit==="수박");
console.log(result); // false 출력
* filter(): 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환
* ㄴ 예: const numbers = [1, 2, 3, 4, 5, 6, 7];
const result = numbers.filter((number)=>number%2===0);
console.log(result); // [2, 4, 6] 출력
* reduce(): 배열의 각 요소에 대하여 주어진 리듀서 함수 실행 후 하나의 결과값 반환
* ㄴ 리듀서 함수 종류: acc(누적 값), cut(현재 값), idx(현재 인덱스), src(원본 배열) 
* ㄴ 예: const numbers = [1, 2, 3, 4, 5, 6, 7];
const result = numbers.reduce((acc, cur)=>acc+cur);
console.log(result); // 28 출력
* ㄴ 예: const fluits = ["사과", "딸기", "배", "참외", "딸기", "수박"];
const result = fluits.reduce((acc, cur)=>{
    console.log("acc: ", acc, "cur: ", cur);
    if (acc.includes(cur) === false) {
        acc.push(cur);
    }
    return acc;
}, []);
console.log(result); // acc: [] cur: 사과 acc: ['사과'] cur: 딸기 ... acc: ['사과', '딸기', '배', '참외', '수박'] 출력



# JavaScript 모듈 시스템
* 모듈: 분리된 파일 (예. main.js, a.js 등)
* ㄴ 클래스 하나 또는 특정한 목적을 가진 여러 함수를 포함하는 라이브러리로 구성
* 장점:
* ㄴ 1. 유지보수용이: 의존성 감소 -> 기능 개선, 수정 용이
* ㄴ 2. 네임스페이스화: 전역스코프에 존재하는 변수명 겹침 문제 해결
* ㄴ 3. 재사용성: 같은 코드 반복 X, 재활용 가능
* 종류: 
* ㄴ 1. AMD: 가장 오래된 모듈 시스템 중 하나, require.js 라이브러리 처음 개발
* ㄴ 2. CommonJS: NodeJS 환경 위해 개발
* ㄴ 3. UMD:AMD와 CommonJS와 같은 다양한 모듈 시스템 함께 사용하기 위해 개발
* ㄴ 4. ES Module: ES6(ES2015)에 도입
* ES Module 방식: 
* ㄴ <script type="module"> 속성 추가 시 해당 파일은 모듈로서 동작
* ㄴ export/default export: 외부에서 모듈을 사용할 수 있도록 내보내기 
* ㄴ import: 외부에서 모듈을 불러오기
* 내보내기:
* ㄴ 1. named export 사용하여 함수/변수 내보내기
* ㄴ 2. default export 사용하여 하나 기본 함수 내보내기 (모듈당 하나만 가능)

# NPM 기초 강좌
* NPM(Node Package Manger): 모듈 저장소에서 모듈을 쉽게 다운로드 받을 수 있게 하는 것
* ㄴ 예: npm install <모듈명>
* npm: Node.js 설치 시 자동 설치
* Node.js: Chrome VB JavaScript 엔진으로 빌드된 JavaScript 런타임
* ㄴ node -v: 노드 버전 확인
* ㄴ npm -v: npm 버전 확인
* ㄴ npm install dayjs: const 변수명 = require('dayjs');
* package.json (직접 작성 또는 npm init으로 자동 생성):
* ㄴ name: 프로젝트 이름 (필수)
* ㄴ version: 프로젝트 버전 
* ㄴ description: 프로젝트 설명
* ㄴ keywords: 프로젝트 검색할 때 참조되는 키워드
* ㄴ private: true로 설정 시 npm 게시 거부
* ㄴ main: 프로그램 기본 진입점
* ㄴ scripts: 프로젝트에서 자주 실행하는 명령어를 scripts로 작성 시 npm 가능
* ㄴ author: 제작자의 이름
* ㄴ license: 패키지 사용 방법과 제한 사항 명시 
* ㄴ * dependencies: 프로젝트 사용하는 모듈 기술
* ㄴ * devDependencies: 개발할 때만 의존하는 모듈 관리
* ㄴ 참고: https://www.npmjs.com/ 
* node_modules: 설치된 모듈뿐만 아니라 의존하고 있는 모듈 전부 설치된 디렉토리
* package-lock.json: 모듈들의 의존성 트리 기록 (node_modules 디렉토리 안에 모듈 다운)
* npm 명령어:
* ㄴ npm init: 새로운 프로젝트(패키지) 시작 시 사용
* ㄴ npm init -y: -y 옵션 사용하여 기본값 자동 설정
* ㄴ npm install <패키지명>: 패키지 설치 명령어
* ㄴ npm install <패키지@버전>: 특정 버전 설치
* ㄴ npm install --save(또는 -S): dependencies에 추가
* ㄴ npm install --save-dev(또는 -D): devDepencencies에 추가
* ㄴ npm install <패키지명1> <패키지명2>: 여러 개 패키지 설치
* ㄴ npm install -g <패키지명>: 전역 설치 
* ㄴ npm uninstall <패키지명>: 로컬 패키지 삭제
* ㄴ npm uninstall -g <패키지명>: 전역 패키지 삭제
* ㄴ npm update <패키지명>: 설치한 패키지 업데이트
* ㄴ npm root: 로컬 패키지 설치 디렉토리 확인
* ㄴ npm root -g: 전역 패키지 설치 디렉토리 확인
* ㄴ npm ls: 로컬 설치된 패키지 확인
* ㄴ npm is -g: 전역 설치된 패키지 확인
* ㄴ npm start:m package.json 파일의 script 속성의 start 실행
* ㄴ npm run <script-name>: package.json 파일의 script 속성의 start와 스크립트 실행
* 버전: MAJOR, MINOR, PATCH
* ㄴ MAJOR: 주요 변화, 기존 API와 추가/변경/삭제 등, 이전 버전과 호환이 안될 수 있음
* ㄴ MINOR: 기능 추가, 이전 버전과 호환된
* ㄴ PATCH: 버그 수정, 이전 버전과 호환됨
* 틸드(~): 현재 지정한 버전의 마지막 자리 내의 범위 내에서만 자동 업데이트
* ㄴ 0.0.1: >=0.0.1<0.1.0
* ㄴ 0.1.1: >=0.1.1<0.2.0
* ㄴ 0.1: >=0.1.0<0.2.0
* ㄴ 0: >=0.0<1.0
* 캐럿(^): Node.js 모듈이 SemVer의 규약을 따른다는 것을 신뢰한다는 가정 하에 등장
* ㄴ MINOR, PATCH 버전은 하위호환성 보장되어야 하므로 업데이트

# Webpack 기초 강좌 
* 특정 코드 자주 사용 -> 재사용/유지보수 -> 파일을 여러 개로 분리해서 개발
* 모듈: 분리된 파일 (예. main.js, a.js 등)
* 개발의 편의성 -> 모듈 분리 증가 -> 브라우저에서 서버에 요청하는 개수 증가 -> 네트워크 비용 증가 -> 페이지 로딩시간 증가 -> 좋지 않은 사용자 경험
* 해결방안: 모듈로 나누어 개발하되, 배포 전 하나의 파일로 압축 (모듈 번들러)
* ㄴ 예: 웹팩(Webpack)
* ㄴ export/import 활용
* ㄴ 방법1: 
* ㄴ npm init -y // package.json 초기화
* ㄴ npm install --save-dev webpack webpack-cli // 로컬 환경에 웹팩 설치
* ㄴ npx webpack --entry ./src/index.js --output-path ./dist --node development
* ㄴ 방법2:
* ㄴ webpack.config.js 파일 추가: 실행 시 자동 참고
* ㄴ npx webpck 실행: dist 폴더 안 bundle.js 파일 생성
* ㄴ 유용: package.json 안 "build": "webpack" 추가 -> npm run build -> dist 폴더 안 bundle.js 파일 생성

